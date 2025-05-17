
# NLP-Powered Bug Ticket Summarization

**Disclaimer**  
This project was originally implemented in 2021 as part of a research thesis.  
It has since been cleaned, commented, and restructured for clarity and publication.  
While the core logic remains intact to preserve its academic context,  
I would take a different architectural and engineering approach if starting today.

---

## Project Overview

Modern software teams often rely on verbose bug reports. This project uses NLP to compress long tickets and commit logs into concise summaries using transformer models (BERT, BART, T5).

### Key features:
- Clean & tokenize noisy ticket data
- Summarize descriptions and commits (extractive & abstractive)
- Export results to structured JSON

---

## Project Pipeline

This summarization module fits into a larger bug ticket analysis workflow.  
The diagram below shows how raw data flows from cloud storage through selection, pre-processing, fine-tuning, and summarization — producing structured output suitable for indexing or further use.

![Summarization Pipeline](/images/pipeline.png)

---

## Models Supported

| Model           | Type        | Description                                          |
|------------------|-------------|------------------------------------------------------|
| `bert-ext`       | Extractive  | Based on `bert-base-uncased`                        |
| `bert-ext-sci`   | Extractive  | SciBERT fine-tuned for scientific domain            |
| `bert-ext-bug`   | Extractive  | Custom fine-tuned on ticket/commit text             |
| `BART`, `T5`     | Abstractive | Transformer encoder-decoder via Hugging Face        |

---

## Fine-Tuning

You can fine-tune your own BERT-based model using this notebook:

```python
# Run cell-by-cell in:
finetune_bert.ipynb
```

> ⚠️ Model weights (`bert-ext-bug`) are not included to respect data privacy.  
> All training code is available so you can retrain on your own dataset.

---

## Example Input/Output

**Input JSON:**
```json
{
  "id": "BUG-2031",
  "summary": "Crash on launch",
  "comments": [{ "raw_text": "App crashes with null pointer..." }]
}
```

**Output JSON:**
```json
{
  "id": "BUG-2031",
  "header": "Crash on launch",
  "summary": "Fix addresses null pointer crash in startup config handling."
}
```

---

## Folder Structure

```
project/
├── finetune_bert.ipynb         # Notebook for fine-tuning of extractive model
├── summarize_ticket.ipynb      # Notebook for transformer-based summarization 
├── README.md
└── images/
    └── pipeline.png            # Visual workflow diagram
```

---

## 🔬 Research Background

This repository contains the official implementation of the experiments and pipeline described in the bachelor thesis:

**“NLP-Assisted Workflow Improving Bug Ticket Handling”**  
by Caroline Eriksson & Emilia Kallis  
KTH Royal Institute of Technology, 2021  
[Read the full thesis on KTH DiVA](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-301248)

> The code was originally written in 2021, and has since been revisited, commented, and republished for transparency and educational use.

---

## Technologies Used

- Python, Transformers, Summarizer
- BERT, T5, BART models
- Regex, SentencePiece, PyTorch
- Google Colab for prototyping

---

## Skills Demonstrated

- NLP pipeline design & data cleaning
- Custom BERT fine-tuning
- Model selection & evaluation
- JSON I/O automation
- Real-world research application

---

## License

Open for academic and educational use.
