# Document Summarization

Reads a PDF from the notebook folder, chunks the text, and produces a concise summary using BART. Designed as a straightforward tutorial — no UI, no file upload, just code.

---

## Model

[facebook/bart-large-cnn](https://huggingface.co/facebook/bart-large-cnn)

BART fine-tuned on CNN/DailyMail — strong on reports, articles, and technical documents. Downloads ~1.6 GB on first run and caches locally.

---

## Setup

```bash
uv pip install transformers torch pypdf
jupyter notebook summarization_en.ipynb
```

Place your PDF in the same folder as the notebook, update `PDF_FILE` in the Config cell, and run all cells top to bottom.

---

## Notebook structure

| Cell | What it does |
|------|-------------|
| 1 — Config | Set the PDF filename, model name, and chunk sizes |
| 2 — Install | `uv pip install` command (uncomment and run once) |
| 3 — Load model | Downloads and loads BART |
| 4 — Extract text | Reads the PDF, prints page count + word count + preview |
| 5 — Chunk | Splits text into chunks that fit BART's 1024-token limit |
| 6 — Summarize chunks | Summarizes each chunk with a progress counter |
| 7 — Final summary | Merges chunk summaries into one final output |

---

## How chunking works

BART has a hard 1024-token input limit. Long documents are handled in three steps:

```
Document
    │
    ├── Chunk 1 ──► Summary 1 ──┐
    ├── Chunk 2 ──► Summary 2 ──┼──► Final Summary
    └── Chunk n ──► Summary n ──┘
```

---

## Changing the model

Edit the **Config cell** only:

```python
PDF_FILE     = "iso27001.pdf"
MODEL_NAME   = "facebook/bart-large-cnn"
CHUNK_TOKENS = 900
MIN_TOKENS   = 30
MAX_TOKENS   = 160
FINAL_MAX    = 300
```

| Model | Best for | Size |
|-------|----------|------|
| `facebook/bart-large-cnn` | News, articles, reports | ~1.6 GB |
| `philschmid/bart-large-cnn-samsum` | Chat, conversations | ~1.6 GB |
| `sshleifer/distilbart-cnn-12-6` | Lightweight, same quality | ~1.2 GB |
