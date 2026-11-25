# Lab 1.2 — End-to-end solution

The thesis proposes a method for generating xUnit tests for C#/.NET code and improving them using execution feedback. The input **X** contains the C# class or method, its relevant dependencies, and the expected behavior. The output **y** is a C# unit test suite. Build diagnostics, test outcomes, and coverage indicate how well the candidate meets the validation criteria.

The [input-output examples](../../data/examples.csv) describe five scenarios. For `PasswordValidator`, X is a validator that checks length, digit, uppercase letter, and special character requirements. The expected y is an xUnit suite that verifies a valid password and tests each validation rule independently.

## Preliminary process model

1. Select the C# code to test and prepare its source context.
2. Retrieve relevant reference code and tests using RAG.
3. Pass the source context and examples to the GenAI model to generate an xUnit candidate.
4. Build the candidate and, when the build succeeds, run the tests and measure coverage.
5. If the candidate meets the criteria, return the test suite and validation results. Otherwise, use the actual diagnostics or coverage gaps to revise the candidate. Stop at the configured attempt limit and report the latest validation status.

Save the scanned or photographed hand-drawn version in this folder as `hand_drawn_process_model.png`. The text above is the preliminary flow for the drawing.

## Colab examples from the assignment

The [Colab explanation draft](colab_explanation.md) needs to be checked against the original two notebooks. The pasted assignment gives their labels without the notebook links.
