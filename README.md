# Advanced RAG Pipeline Optimization & Evaluation with TruLens

This repository demonstrates a complete engineering workflow for building, benchmarking, and optimizing a Retrieval-Augmented Generation (RAG) system. Moving beyond naive vector search setups, this project implements advanced retrieval architectures—specifically **Sentence Window Retrieval** and **Auto-merging Retrieval**—and systematically evaluates them using the **TruLens RAG Triad** framework.

The pipeline serves as an expert AI Career Mentor bot, answering complex professional queries using Andrew Ng's 41-page eBook, *"How to Build Your Career in AI: A Simple Guide"*, as its proprietary knowledge corpus.

---

##  Tech Stack & Core Libraries

*   **RAG Orchestration:** `LlamaIndex` (Document ingestion, node parsing, hierarchical index management)
*   **Evaluation Engine:** `TruLens Eval` (LLM-as-a-judge recording and RAG Triad metric tracking)
*   **Large Language Model:** OpenAI (`gpt-3.5-turbo` with a deterministic temperature of 0.1)
*   **Embedding Model:** Local HuggingFace embeddings (`BAAI/bge-small-en-v1.5`)[cite: 1]
*   **Database backend:** SQLite (for local TruLens evaluation logging)[cite: 1]
*   **UI/Analytics Dashboard:** Streamlit (via TruLens built-in dashboard utility)[cite: 1]

---

##  The RAG Triad Evaluation Framework

To scientifically measure system upgrades, every iteration was tested against a baseline question bank (`eval_questions.txt`) across three key dimensions[cite: 1]:

1.  **Context Relevance:** Assesses whether the retrieved document snippets are highly specific and free of noise[cite: 1].
2.  **Groundedness:** Validates whether the LLM's final response is strictly derived from the retrieved context to eliminate hallucinations[cite: 1].
3.  **Answer Relevance:** Measures how directly and completely the final output addresses the user's initial prompt[cite: 1].

---

##  Empirical Performance Comparison

Below are the audited, recorded metrics pulled directly from our evaluation pipeline's leaderboard[cite: 1]:

| Retrieval Strategy | Context Relevance | Answer Relevance | Groundedness | Latency (avg/sec) | Total Cost (avg) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Sentence Window Query Engine**[cite: 1] | 0.4800[cite: 1] | 1.0[cite: 1] | 0.6267[cite: 1] | 1.3636[cite: 1] | $0.000805[cite: 1] |
| **Automerging Query Engine**[cite: 1] | **0.7214**[cite: 1] | **1.0**[cite: 1] | **0.6905**[cite: 1] | 2.3636[cite: 1] | $0.000863[cite: 1] |

### Key Architectural Takeaways
*   **The Baseline Problem:** Standard chunking methods often suffer from an indexing dilemma—small chunks lack context, while massive chunks dilute relevance[cite: 1].
*   **Sentence Window Retrieval:** Decouples embedding search from generator context[cite: 1]. It queries single sentences for ultra-precise matches, then restores a surrounding window of text before passing it to the LLM[cite: 1].
*   **The Automerging Winner:** By dynamically merging granular text leaves into full parent blocks when a threshold of child nodes is met, **Auto-merging Retrieval optimized Context Relevance by ~50%** and notably boosted groundedness, making it the superior architecture for this dataset[cite: 1].

---

##  Repository Structure

```text
├── Advanced_RAG_Pipeline.ipynb   # Main production notebook with complete logic[cite: 1]
├── eval_questions.txt            # Benchmark dataset containing evaluation queries[cite: 1]
├── utils.py                      # Prebuilt indexers and TruLens recorders[cite: 1]
├── eBook-How-to-Build-a-Career-in-AI.pdf  # Target text corpus document[cite: 1]
└── README.md                     # Project documentation
