# LLM Quicks

Self-contained Jupyter notebooks, each demonstrating one practical LLM task — runnable in minutes, no shared dependencies between notebooks.

---

## Notebooks

| # | Task | Folder | Model |
|---|------|--------|-------|
| 1 | Arabic → English translation | [Translation/](Translation/) | `facebook/nllb-200-distilled-600M` |

---

## Getting started

**Requirements:** Python 3.10+, [uv](https://github.com/astral-sh/uv)

```bash
git clone https://github.com/<your-username>/LLM-Quicks.git
cd LLM-Quicks
uv pip install transformers sentencepiece torch ipywidgets jupyter
jupyter notebook
```

Open any notebook folder and follow its own README for model-specific setup.

---

## Structure

```
LLM-Quicks/
├── README.md                        # this file — repo index
├── Translation/
│   ├── translation_ar_eng.ipynb
│   └── README.md
└── <future-notebooks>/
    ├── notebook.ipynb
    └── README.md
```

---

## License

[MIT](LICENSE)
