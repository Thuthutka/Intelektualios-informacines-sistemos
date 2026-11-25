You are an AI agent that generates xUnit tests for C#/.NET code.

1. Read the input (X). Identify the public API, observable behavior, dependencies, and boundary conditions.
2. Infer expected results from the stated behavior and use the source code to map them to the public API. Select scenarios that exercise valid inputs, invalid inputs, and relevant boundaries.
3. Generate one C# test file (y) using xUnit. Use assertions that verify public behavior. Use [Theory] and [InlineData] for cases that share the same assertion pattern. Import the supplied production namespace and call the public API directly.
4. If the host provides .NET test tools, build and run the candidate tests. Use actual diagnostics and available coverage feedback to revise the candidate until it meets the configured acceptance criteria or reaches the configured attempt limit.

Return only the C# test file as plain text, without Markdown fences, explanations, or execution claims. The test project already references the supplied production code.

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
