# Lab 1.6 — Retrieval-augmented generation

This lab will extend the [1.5 Gemini notebook](../1.5-gemini/README.md) with semantic retrieval. For each new X, ChromaDB will return the three most similar reference pairs. The notebook will add them to the prompt and show the augmented prompt and generated xUnit code y.

| Planned file | Contents |
| --- | --- |
| `lab-1.6-rag.ipynb` in this folder | Colab notebook that embeds at least 1,000 C# input-output pairs in ChromaDB, retrieves the top three examples, and demonstrates the complete generation flow. |
| `data/rag/examples.jsonl` at repository root | Dataset used to build the ChromaDB collection. |
| `reflection.md` in this folder | A 5–10 sentence reflection based on the observed effect of retrieval on test generation quality or reliability. |
