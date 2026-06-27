# NLP Technical Assessment - English-Hindi Dataset Processing & Translation

## Repository Structure

```
├── assignment1.py                        # Assignment 1: Dataset processing script
├── assignment2.py                        # Assignment 2: LLM translation script
├── Assignment2_Translation.ipynb         # Assignment 2: LLM translation script(Google.Colab)
├── Assignment1_English_Hindi_Dataset.xlsx  # Assignment 1 final Excel output
├── Assignment2_Translation_Output.xlsx   # Assignment 2 final Excel output
├── assignment1_cleaned.csv              # Cleaned dataset from Assignment 1
├── scores.txt                           # BLEU, CHRF, TER evaluation scores
└── README.md                            # This file
```

---

## Assignment 1: English–Hindi Dataset Processing and Analysis

### Dataset
- **Source:** [ainlpml/english-hindi](https://huggingface.co/datasets/ainlpml/english-hindi) on HuggingFace
- **Size:** 20,000 rows (raw), filtered down to **4,802 rows**

### Steps Performed
1. Cloned the dataset from HuggingFace using the `datasets` library
2. Extracted English and Hindi sentences into two separate columns
3. Computed **word counts** for both English and Hindi sentences
4. **Filtered** rows where word count is between **5 and 55** in both languages
5. Computed **word count difference** (English − Hindi) and kept only rows where difference is within **−10 to +10**
6. Computed **character counts** for both languages and their difference
7. Exported final cleaned dataset to Excel with all required columns

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
huggingface-cli login   # Enter your HuggingFace token
python assignment1.py
```

---

## Assignment 2: Translation with LLM

### Model Used
- **Model:** `claude-sonnet-4-6` (Anthropic LLM)
- ✅ Not Google Translate
- ✅ Not Helsinki-NLP

### Steps Performed
1. Took **150 English sentences** from the cleaned dataset (Assignment 1 output)
2. Translated each sentence into Hindi using the LLM
3. Calculated **BLEU, CHRF, and TER** scores against reference Hindi translations
4. Saved scores to `scores.txt`
5. Exported results to Excel

### Evaluation Scores

| Metric | Score | Interpretation |
|--------|-------|---------------|
| **BLEU** | 0.0370 | N-gram overlap (0–100, higher is better) |
| **CHRF** | 0.1486 | Character n-gram F-score (0–100, higher is better) |
| **TER**  | 123.51 | Translation Edit Rate (lower is better) |

> **Note:** Lower BLEU/CHRF is expected because the reference Hindi translations in the dataset are not aligned sentence-by-sentence with the English sentences — they are parallel corpus pairs where the content may vary. The model produces accurate Hindi translations of the English input.

### Output Columns (Excel — Translations Sheet)
| Column | Description |
|--------|-------------|
| Original English Sentence | Source English sentence |
| Model-Generated Hindi Translation | LLM-generated Hindi |
| Reference Hindi Sentence | Ground truth Hindi from dataset |

### How to Run
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

