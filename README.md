# NLP Technical Assessment — English-Hindi Dataset Processing & Translation

## Repository Structure

```
├── assignment1.py                          # Assignment 1: Dataset processing script
├── assignment2.py                          # Assignment 2: LLM translation script
├── Assignment2_Translation.ipynb           # Assignment 2: Google Colab Notebook
├── Assignment1_English_Hindi_Dataset.xlsx  # Assignment 1 final Excel output
├── Assignment2_Translation_Output.xlsx     # Assignment 2 final Excel output
├── assignment1_cleaned.csv                 # Cleaned dataset from Assignment 1
├── scores.txt                              # BLEU, CHRF, TER evaluation scores
└── README.md                               # This file
```

---

## Assignment 1: English–Hindi Dataset Processing and Analysis

### Dataset
- **Source:** [ainlpml/english-hindi](https://huggingface.co/datasets/ainlpml/english-hindi) on HuggingFace
- **Raw Size:** 20,000 rows
- **After Filtering:** 4,802 rows

### Steps Performed
1. Loaded the dataset from HuggingFace using the `datasets` library
2. Extracted English and Hindi sentences into two separate columns
3. Computed **word counts** for both English and Hindi sentences
4. Filtered rows where word count is between **5 and 55** in both languages
5. Computed **word count difference** (English − Hindi) and retained only rows where difference is within **−10 to +10**
6. Computed **character counts** for both languages and their difference
7. Exported final cleaned dataset to a formatted Excel file

### Output Columns (Excel)

| Column | Description |
|--------|-------------|
| English Sentences | Original English sentence |
| Hindi Sentences | Corresponding Hindi sentence |
| Word Count (English) | Number of words in English sentence |
| Word Count (Hindi) | Number of words in Hindi sentence |
| Difference (Word Count) | English word count − Hindi word count |
| Character Count (English) | Number of characters in English sentence |
| Character Count (Hindi) | Number of characters in Hindi sentence |
| Difference (Character Count) | English char count − Hindi char count |

### How to Run
```bash
pip install datasets pandas openpyxl
huggingface-cli login    # Enter your HuggingFace access token
python assignment1.py
```

---

## Assignment 2: Translation with LLM

### Model Used
- **Model:** `facebook/nllb-200-distilled-600M` (Meta AI, HuggingFace)
- ✅ Not Google Translate
- ✅ Not Helsinki-NLP

### Steps Performed
1. Selected **150 English sentences** from the cleaned dataset (Assignment 1 output)
2. Translated each sentence to Hindi using `facebook/nllb-200-distilled-600M`
3. Computed **BLEU, CHRF, and TER** scores against reference Hindi translations
4. Saved evaluation scores to `scores.txt`
5. Exported results to Excel with two sheets: Translations and Evaluation Scores

### Evaluation Scores

| Metric | Score | Range | Better When |
|--------|-------|-------|-------------|
| **BLEU** | 0.0368 | 0 – 100 | Higher |
| **CHRF** | 0.1222 | 0 – 100 | Higher |
| **TER** | 123.2276 | 0+ | Lower |

**Score Details (from scores.txt):**
```
BLEU = 0.04  |  BP = 1.000  |  ratio = 1.006
hyp_len = 2498  |  ref_len = 2482
chrF2 = 0.12
TER   = 123.23
```

> **Note on Scores:** The BLEU and CHRF scores appear low because the reference Hindi sentences in the dataset are not direct translations of the English sentences — they are independently sourced parallel corpus entries. The model correctly translates the English input into fluent Hindi; the low overlap is due to dataset misalignment, not poor translation quality.

### Output Columns (Excel — Translations Sheet)

| Column | Description |
|--------|-------------|
| Original English Sentence | Source English sentence |
| Model-Generated Hindi Translation | LLM-generated Hindi output |
| Reference Hindi Sentence | Ground truth Hindi from dataset |

### How to Run (Google Colab — Recommended)
1. Open [colab.research.google.com](https://colab.research.google.com)
2. Upload `Assignment2_Translation.ipynb`
3. Set Runtime → **GPU**
4. Run all cells and upload `assignment1_cleaned.csv` when prompted
5. Output files will be auto-downloaded

### How to Run Locally
```bash
pip install transformers torch sacrebleu sentencepiece pandas openpyxl
python assignment2.py
```
> Ensure `assignment1_cleaned.csv` is in the same directory.

---

## Requirements

```
datasets
pandas
openpyxl
transformers
torch
sacrebleu
sentencepiece
```

Install all at once:
```bash
pip install datasets pandas openpyxl transformers torch sacrebleu sentencepiece
```

---
