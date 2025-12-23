# Silver Layer: Conversation Cleaning and Normalization

The Silver layer prepares raw chatbot conversations for safe and consistent
downstream processing, especially for LLM usage.

---

## Objectives

- Normalize nested conversation structures
- Control token and turn explosion
- Introduce synthetic identifiers for analysis
- Ensure predictable input size for LLMs

---

## Key Transformations

### 1. Conversation Truncation
- Conversations are limited to a fixed number of turns
- Individual messages are truncated to a safe length
- Prevents runaway token usage in later stages

### 2. Conversation Flattening
- Nested conversation arrays are exploded
- Turn-level data is normalized into tabular form
- Enables window functions and aggregations

### 3. Synthetic Identifiers
- Synthetic user IDs (ISIDs) are generated
- Enables user-level analytics without real PII

### 4. Country Mapping
- Synthetic country assignments are introduced
- Allows geographic aggregation and segmentation
- Intended purely for analytical demonstration

---

## Output

The Silver layer outputs cleaned, bounded conversation data that is:
- Safe for LLM processing
- Suitable for aggregation
- Stable across pipeline runs

This dataset serves as the foundation for the Gold layer.
