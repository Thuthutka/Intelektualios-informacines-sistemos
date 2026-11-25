You are an AI agent that generates xUnit tests for C#/.NET code.

1. Read the input (X). Identify the public API, observable behavior, dependencies, and boundary conditions.
2. Infer expected results from the stated behavior and use the source code to map them to the public API. Select scenarios that exercise valid inputs, invalid inputs, and relevant boundaries.
3. Generate one C# test file (y) using xUnit. Use assertions that verify public behavior. Use [Theory] and [InlineData] for cases that share the same assertion pattern. Import the supplied production namespace and call the public API directly.
4. If the host provides .NET test tools, build and run the candidate tests. Use actual diagnostics and available coverage feedback to revise the candidate until it meets the configured acceptance criteria or reaches the configured attempt limit.

Return only the C# test file as plain text, without Markdown fences, explanations, or execution claims. The test project already references the supplied production code.

## Reference examples from Lab 1.2

Use these examples to see how source behavior maps to xUnit cases. Generate tests only for the new observation that follows.

### Example 1 — PasswordValidator (data/examples.csv, id 1)

X — A password must have at least eight characters, a digit, an uppercase letter, and a non-whitespace special character.

```csharp
using System.Linq;

namespace Lab14.Examples;

public static class PasswordValidator
{
    public static bool IsValid(string password)
    {
        return password.Length >= 8
            && password.Any(char.IsDigit)
            && password.Any(char.IsUpper)
            && password.Any(c => !char.IsLetterOrDigit(c) && !char.IsWhiteSpace(c));
    }
}
```

y — xUnit tests for a valid password and one case that violates each requirement.

```csharp
using Lab14.Examples;
using Xunit;

public class PasswordValidatorTests
{
    [Theory]
    [InlineData("Abcdef1!", true)]
    [InlineData("Abcd1!", false)]
    [InlineData("Abcdefg!", false)]
    [InlineData("abcdef1!", false)]
    [InlineData("Abcdef12", false)]
    public void IsValid_ReturnsExpectedResult(string password, bool expected)
    {
        Assert.Equal(expected, PasswordValidator.IsValid(password));
    }
}
```

### Example 2 — EmailValidator (data/examples.csv, id 2)

X — An email must have a local part, an @, and a domain with a dot. This example uses a simplified format check.

```csharp
using System.Text.RegularExpressions;

namespace Lab14.Examples;

public static class EmailValidator
{
    public static bool IsValid(string? email)
    {
        return !string.IsNullOrEmpty(email)
            && Regex.IsMatch(email, @"^[^@\s]+@[^@\s]+\.[^@\s]+$");
    }
}
```

y — xUnit tests for valid, malformed, empty, and null addresses.

```csharp
using Lab14.Examples;
using Xunit;

public class EmailValidatorTests
{
    [Theory]
    [InlineData("student@example.com", true)]
    [InlineData("student@example", false)]
    [InlineData("", false)]
    [InlineData(null, false)]
    public void IsValid_ReturnsExpectedResult(string? email, bool expected)
    {
        Assert.Equal(expected, EmailValidator.IsValid(email));
    }
}
```

### Example 3 — UsernameService (data/examples.csv, id 3)

X — Save a username only if it contains at least three characters and is not empty or whitespace.

```csharp
using System;

namespace Lab14.Examples;

public sealed class UsernameService
{
    private readonly Action<string> save;

    public UsernameService(Action<string> save)
    {
        this.save = save;
    }

    public bool TrySave(string username)
    {
        if (string.IsNullOrWhiteSpace(username) || username.Length < 3)
        {
            return false;
        }

        save(username);
        return true;
    }
}
```

y — xUnit tests verify acceptance and persistence for a valid name and rejection without persistence for empty, whitespace, and short names.

```csharp
using System.Collections.Generic;
using Lab14.Examples;
using Xunit;

public class UsernameServiceTests
{
    [Fact]
    public void TrySave_ValidUsername_SavesUsername()
    {
        var savedNames = new List<string>();
        var service = new UsernameService(savedNames.Add);

        Assert.True(service.TrySave("ada"));
        Assert.Equal("ada", Assert.Single(savedNames));
    }

    [Theory]
    [InlineData("")]
    [InlineData("   ")]
    [InlineData("ad")]
    public void TrySave_InvalidUsername_DoesNotSave(string username)
    {
        var savedNames = new List<string>();
        var service = new UsernameService(savedNames.Add);

        Assert.False(service.TrySave(username));
        Assert.Empty(savedNames);
    }
}
```

## New observation (X)

Test framework: xUnit.
Production namespace: Lab14.Target.
Expected behavior: An order quantity is allowed if it is positive, does not exceed available stock, and is at most 10 items per order. A quantity equal to either upper limit is allowed.

```csharp
namespace Lab14.Target;

public static class OrderQuantityValidator
{
    public const int MaxPerOrder = 10;

    public static bool IsAllowed(int quantity, int availableStock)
    {
        return quantity > 0
            && quantity <= availableStock
            && quantity <= MaxPerOrder;
    }
}
```

Generate y for the new observation.
