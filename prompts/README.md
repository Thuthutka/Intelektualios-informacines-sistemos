# Lab 1.4 — End-to-end AI agent for C# unit test generation

The agent coordinates the thesis workflow described in [Lab 1.3](../data/lab1.3.md). It receives **X**, which contains the C# source code, the expected behavior, and settings such as the test framework. It returns **y**, a C# file containing generated xUnit tests. The host can also retain build, execution, and coverage results as validation metadata.

| Stage | What the agent does |
| --- | --- |
| Data understanding | Identify the public API, expected behavior, and dependencies in X. |
| Inference | Derive expected results for representative inputs and boundary values. |
| Reasoning | Choose test cases and assertions that distinguish the expected behaviors. |
| Output generation | Generate a C# xUnit test file. If the host exposes .NET tooling, build and run the tests and use actual diagnostics or coverage results to revise them within the configured attempt limit. |

## Prompt examples

Both prompts use the same new observation, `OrderQuantityValidator`. It admits an order only when the quantity is positive and within both the available stock and the per-order limit. Both prompts request a single xUnit test file. Keeping X and the output format fixed makes the effect of reference examples easier to examine.

| Prompt | Context provided to the model |
| --- | --- |
| [Zero-shot](zero_shot.md) | Agent instructions and the new X. |
| [Few-shot](few_shot.md) | The same instructions and X, plus three reference pairs from [Lab 1.2](../data/examples.csv). |

The few-shot examples expand rows 1–3 of the Lab 1.2 CSV into illustrative C# code and xUnit tests. The CSV specifies the behaviors and expected test scenarios. The code listings are concrete examples created for this lab.

## Colab comparison

Send each prompt in a separate request with the same model and generation settings. Record which scenarios each result covers, including zero quantity, the stock boundary, and the maximum per order. When a .NET runner is available, compare build status, test results, and coverage. The prompt files define the generation tasks. The Colab execution and comparison belong to Lab 1.5.
