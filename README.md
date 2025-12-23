# Databricks Semantic Cache for GenAI Chatbot Analytics

https://github.com/user-attachments/assets/9c8d68d5-fe36-4746-b4bd-4652bb652ae8

This repository demonstrates how Databricks can be used as an end-to-end analytics platform
for GenAI chatbot applications, with a focus on reducing LLM classification costs through
a semantic cache layer built using Mosaic AI Vector Search.

Instead of relying on reactive signals such as surveys or bug tickets, this project shows
how continuous conversation analysis can support proactive, data-driven feature development
for chatbot-based products.

---

## Motivation

Most chatbot analytics today are retrospective.

Product teams typically learn about user friction only after:
- Surveys are filled
- Bug tickets are raised
- Feedback is manually reported

While LLMs are effective at classifying user intent, using them to label every conversation
on an ongoing basis does not scale well for frequent analysis (daily or weekly).

This project explores a hybrid approach:
- Use semantic similarity to reuse labels when intents repeat
- Fall back to LLMs only when the semantic cache misses
- Continuously improve cache effectiveness over time

---

## Core Idea: Semantic Cache for Conversation Classification
<img width="1677" height="802" alt="Screenshot 2025-12-24 at 3 50 11 AM" src="https://github.com/user-attachments/assets/3175a9da-7f90-4d43-808e-a20133acdc6b" />

Conversation intents repeat.

If a new conversation is semantically similar to a previously labeled conversation, we can
reuse the existing category instead of calling an LLM again.

The classification flow is:

Vector Search hit → reuse category  
Vector Search miss → call LLM → persist result → sync vector index  

As the vector index grows, the semantic cache becomes more effective, reducing:
- LLM calls
- Cost
- End-to-end classification latency

---

## Dataset

This project uses the **WildChat public dataset** from Hugging Face, which contains real-world
chatbot conversations across a wide range of domains.

The dataset is treated as a stand-in for production chatbot logs.

---

## Repository Structure

```text
.
├── bronze/
│   └── README.md
│
├── silver/
│   ├── 1_silver_etl.ipynb
│   └── README.md
│
├── gold_classification/
│   ├── 2_gold_etl.ipynb
│   ├── 3_gold_llm_summarizer.ipynb
│   ├── 4_gold_llm_taxonomy_creation.ipynb
│   ├── 5_gold_semantic_classification.ipynb
│   ├── 6_gold_llm_classification.ipynb
│   ├── 7-3_index_creation.ipynb
│   └── README.md
│
├── gold_aggregation/
│   ├── 7-1_gold_class_country.ipynb
│   ├── 7-2_gold_class_user.ipynb
│   └── README.md
│
└── README.md
