# Arabic → English Translation

Interactive Jupyter widget for translating Arabic text (MSA and dialects) to English using Meta's NLLB-200 model.

---

## Model

[facebook/nllb-200-distilled-600M](https://huggingface.co/facebook/nllb-200-distilled-600M)

No Language Left Behind — trained on 200 languages, strong on Arabic dialects (Gulf, Levantine, Egyptian, Maghrebi). Downloads ~1.2 GB on first run and caches locally.

---

## Setup

```bash
uv pip install transformers sentencepiece torch ipywidgets
jupyter notebook translation_ar_eng.ipynb
```

Run all cells top to bottom. The widget appears after the last cell.

---

## Usage

Type Arabic text into the input box and press **Translate**.

**Example:**
```
Input:  اتبع قلبك فحسب.
Output: Just follow your heart.
```

---

## Changing the language pair

Edit the **Config cell** (cell 1) only:

```python
SRC_LANG  = "arb_Arab"   # source language code
TGT_LANG  = "eng_Latn"   # target language code
SRC_LABEL = "Arabic"     # display label
TGT_LABEL = "English"    # display label
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

## How it works

1. The tokenizer encodes the source text with no language prefix (NLLB embeds language in the model weights).
2. `forced_bos_token_id` is set to the target language token ID, which forces the decoder to generate in that language.
3. `model.generate()` runs beam search and the tokenizer decodes the output.

```python
inputs  = tokenizer(text, return_tensors="pt")
tgt_id  = tokenizer.convert_tokens_to_ids(TGT_LANG)
outputs = model.generate(**inputs, forced_bos_token_id=tgt_id, max_new_tokens=128)
result  = tokenizer.decode(outputs[0], skip_special_tokens=True)
```
