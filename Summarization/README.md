# English Text Summarization

Interactive Jupyter widget for summarizing English text using Meta's BART model.

---

## Model

[facebook/bart-large-cnn](https://huggingface.co/facebook/bart-large-cnn)

BART fine-tuned on CNN/DailyMail — strong on news articles, reports, and long-form text. Downloads ~1.6 GB on first run and caches locally.

---

## Setup

```bash
uv pip install transformers torch ipywidgets
jupyter notebook summarization_en.ipynb
```

Run all cells top to bottom. The widget appears after the last cell.

---

## Usage

Paste English text (at least 30 words) into the input box and press **Summarize**. A live word counter updates as you type.

**Example:**

```
Input:  NASA's James Webb Space Telescope has captured the deepest and sharpest
        infrared image of the distant universe to date. The image shows the galaxy
        cluster SMACS 0723 as it appeared 4.6 billion years ago. Thousands of
        galaxies — including the faintest objects ever observed — have appeared
        in Webb's view for the first time...

Output: NASA's James Webb Space Telescope has captured the deepest infrared image
        of the distant universe. The image shows thousands of galaxies, including
        the faintest objects ever observed.
```

---

## Changing the model

Edit the **Config cell** (cell 1) only:

```python
MODEL_NAME = "facebook/bart-large-cnn"
MIN_TOKENS = 30
MAX_TOKENS = 160
```

Available models:

| Model | Best for | Size |
|-------|----------|------|
| `facebook/bart-large-cnn` | News, articles, reports | ~1.6 GB |
| `philschmid/bart-large-cnn-samsum` | Chat, conversations | ~1.6 GB |
| `sshleifer/distilbart-cnn-12-6` | Lightweight, same quality | ~1.2 GB |

---

## How it works

The input is tokenized and truncated to 1024 tokens (BART's context limit). Beam search generates the summary, with `length_penalty` encouraging conciseness.

```python
inputs  = tokenizer(text, return_tensors="pt", max_length=1024, truncation=True)
outputs = model.generate(
    **inputs,
    min_length=MIN_TOKENS,
    max_length=MAX_TOKENS,
    num_beams=4,
    length_penalty=2.0,
    early_stopping=True,
)
result = tokenizer.decode(outputs[0], skip_special_tokens=True)
```
