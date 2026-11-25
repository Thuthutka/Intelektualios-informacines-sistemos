# Lab 1.6 — Retrieval-augmented generation

This lab extends the [Lab 1.5 Gemini notebook](../1.5-gemini/README.md) with semantic retrieval. ChromaDB indexes 1,000 synthetic C# and xUnit pairs. For a new C# input, the notebook displays the three retrieved pairs in the augmented prompt and compares Gemini's generated tests with and without retrieval.

- [Notebook](lab-1.6-rag.ipynb)
- [Open in Google Colab](https://colab.research.google.com/github/Thuthutka/Intelektualios-informacines-sistemos/blob/main/notebooks/1.6-rag/lab-1.6-rag.ipynb)
- [Dataset of 1,000 example pairs](../../data/rag/examples.jsonl)
- [Reflection](reflection.md)

In this run, the baseline covered five of the six selected scenarios and the RAG output covered all six. The comparison used inspection of the generated code.
