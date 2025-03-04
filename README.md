# Fine-Tuning a Hugging Face LLM for Archaeology Summarization

## Overview
This project focuses on fine-tuning a Hugging Face LLM (such as T5) to summarize academic papers in archaeology and prehistory. Due to the lack of domain-specific summarization datasets, the **Semantic Scholar Network (SSN) dataset** was selected as a workaround. This repository contains the preprocessing scripts, dataset adaptation process, and fine-tuning workflow.

## Challenges & Solutions

### 1. Data Acquisition & Suitability
**Challenge:** Finding an appropriate dataset for fine-tuning a summarization model specialized in archaeology and prehistory.

**Solution:**
- The **SSN dataset (Semantic Scholar Network)** https://drive.google.com/file/d/1P5viA8hMm19n-Ia3k9wZyQTEloCk2gMJ/view was selected because it includes research papers across multiple disciplines.
- While SSN is not explicitly an archaeology dataset, several of its domains align closely with archaeology:
  - **Sociology** – Examines past and present societies.
  - **Geology** – Provides insights into stone, ore types, and stratigraphy.
  - **Biology** – Includes genetics, crucial for studying ancient DNA.
  - **History** – Relates to chronology and historical context.
- By leveraging these sub-fields, SSN serves as a viable source for training a summarization model tailored to archaeology-related disciplines.

### 2. Dataset Structuring & Processing
**Challenge:** Preparing the SSN dataset for Hugging Face’s `Dataset.from_dict()`.

**Issues encountered:**
- **Aspect and text nodes contained nested lists**, requiring flattening.
- **Column length mismatch (`ArrowInvalid` error)** – lists had inconsistent lengths, preventing direct dataset conversion.

**Solutions applied:**
- Standardized list structures to ensure uniformity across all dataset columns.
- Implemented preprocessing scripts to align column lengths before conversion.
- **Preprocessing and training are handled in the same script** to streamline the workflow and avoid redundancy.

### 3. Compute Resource Limitations
**Challenge:** Finding free GPU resources for fine-tuning the model.

**Current Approach:**
- Exploring **Colab Pro, Kaggle, Hugging Face Spaces, and academic cloud resources** as potential solutions.
- Evaluating runtime and VRAM limitations of free-tier GPU options.

### 4. Evaluation with ROUGE Score
**Challenge:** Measuring the performance of the summarization model effectively.

**Solution:**
- Implemented **ROUGE** as part of the `compute_metrics` function.
- Used `rouge.compute(predictions=decoded_preds, references=decoded_labels, use_stemmer=True)` to calculate ROUGE scores.
- This ensures that model performance is evaluated based on content overlap with reference summaries.

## Repository Contents
- **`training_script.py`** – A unified script that includes both preprocessing and training.
- **`notebooks/`** – Jupyter notebooks for data exploration and preprocessing.
- **`README.md`** – Project documentation (this file).

## Future Work
- Experiment with different Hugging Face models for optimal summarization performance.
- Investigate additional data sources to supplement SSN.
- Optimize GPU usage for more efficient fine-tuning.

## Contact
If you have questions or suggestions, feel free to open an issue or reach out!

---
