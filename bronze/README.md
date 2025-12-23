# Bronze Layer: Raw Data Ingestion

This folder documents how the raw WildChat dataset is sourced and prepared
for downstream processing.

---

## Dataset Source

The project uses the **WildChat public dataset**, available on Hugging Face:

https://huggingface.co/datasets/allenai/WildChat

WildChat contains real-world chatbot conversations spanning multiple domains
and use cases, making it a good proxy for production chatbot logs.

For this project, `train-00000-of-00006.parquet` has been utilized as the main conversations table.
