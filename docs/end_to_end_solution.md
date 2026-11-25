# End-to-End AI Solution Description

My thesis project focuses on a GenAI-based method for generating unit tests with improvement iterations.

The system works as an end-to-end AI solution where the input X is a piece of source code, such as a C# method, service class, or API endpoint. The output y is a generated unit test class, for example an xUnit test file.

The proposed system first analyzes the input code and prepares its context. Then it retrieves similar examples from a knowledge base using a Retrieval-Augmented Generation approach. These examples are added to the prompt and sent to a generative AI model. The model generates an initial unit test. After that, the generated test is executed automatically. If compilation or execution errors are detected, the system uses this feedback to repair and improve the test in another iteration.

Therefore, the complete pipeline is:

Input source code X → code context preparation → RAG context retrieval → prompt construction → GenAI-based test generation → automatic test execution → feedback-based test repair → final unit test y.

The goal of the system is to improve the reliability, executability, and practical usefulness of automatically generated unit tests.