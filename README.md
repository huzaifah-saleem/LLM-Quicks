# LLM Quicks

A growing collection of self-contained Jupyter notebooks, each demonstrating one practical LLM task — runnable in minutes, no boilerplate.

---

## Notebooks

| # | Task | Notebook | Model |
|---|------|----------|-------|
| 1 | Arabic → English translation | [translation_ar_eng.ipynb](translation_ar_eng.ipynb) | `facebook/nllb-200-distilled-600M` |

---

## Getting started

**Requirements:** Python 3.10+, [uv](https://github.com/astral-sh/uv)

```bash
git clone https://github.com/<your-username>/LLM-Quicks.git
cd LLM-Quicks
uv pip install transformers sentencepiece torch ipywidgets jupyter
jupyter notebook
```

Then open any notebook and run all cells.

---

## Notebook 1 — Arabic → English Translation

An interactive widget that translates Arabic text (including dialects) to English in real time.

**Model:** [facebook/nllb-200-distilled-600M](https://huggingface.co/facebook/nllb-200-distilled-600M) — Meta's No Language Left Behind model, trained on 200 languages.

**How to change the language pair**

Only the Config cell needs to change:

```python
SRC_LANG  = "arb_Arab"   # Arabic
TGT_LANG  = "eng_Latn"   # English
```

Common NLLB language codes:

| Language | Code |
|----------|------|
| Arabic | `arb_Arab` |
| English | `eng_Latn` |
| French | `fra_Latn` |
| Spanish | `spa_Latn` |
| German | `deu_Latn` |

Full list: [FLORES-200 language codes](https://github.com/facebookresearch/flores/blob/main/flores200/README.md)

---

## Structure

```
LLM-Quicks/
├── translation_ar_eng.ipynb   # Notebook 1 — Arabic → English
└── README.md
```

New notebooks will be added as standalone files — one task per notebook, no shared dependencies.

---

## License

[MIT](LICENSE)
