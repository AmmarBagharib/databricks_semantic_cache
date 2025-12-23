# Gold Layer: Classification and Semantic Caching

This folder contains the core logic of the project: turning chatbot conversations
into continuously analyzable signals using a hybrid semantic cache + LLM approach.

---

## Overview

The Gold classification layer transforms cleaned conversations into:
- Summarized representations
- Structured topic categories
- Semantic embeddings
- A searchable vector index

The goal is to minimize LLM usage while maintaining high-quality classification.

---

## Step 1: Conversation Summarization

Notebook: `3_gold_llm_summarizer.ipynb`

- Long conversations are summarized using an LLM
- Summaries capture user intent more efficiently than raw text
- Reduces embedding cost and noise

Output:
- One summary per conversation

---

## Step 2: Taxonomy Creation

Notebook: `4_gold_llm_taxonomy_creation.ipynb`

- A sample of summaries is sent to an LLM
- The model proposes a compact, non-overlapping set of categories
- Produces a global taxonomy grounded in actual user behavior

Output:
- List of topic categories

---

## Step 3: Vector Index Creation (run only once)

Notebook: `7-3_index_creation.ipynb`

- Conversation summaries are embedded
- A Databricks Vector Search index is created
- The index is configured to sync with Delta tables

This index forms the semantic cache.

---

## Step 4: Semantic Classification (Cache First)

Notebook: `5_gold_semantic_classification.ipynb`

For each new conversation:
1. Embed the summary
2. Query the vector index
3. Retrieve top-k similar conversations
4. Apply a similarity threshold

If similarity ≥ threshold:
- Reuse the existing category
- Avoid LLM call

---

## Step 5: LLM Classification (Fallback)

Notebook: `6_gold_llm_classification.ipynb`

If no semantic match meets the threshold:
- Call an LLM to classify the conversation
- Persist the new label
- Write back to Delta

---

## Step 6: Cache Update
Notebook: `7-3_index_creation.ipynb`
- Newly classified conversations are merged into the Gold table
- Vector index is synchronized
- Cache effectiveness improves over time

---

## Key Insight

Semantic caching exploits the fact that conversation intents repeat.

As the index grows:
- Cache hit rate increases
- LLM calls decrease
- Classification becomes cheaper and faster

This enables continuous analytics rather than one-off studies.
