# Text Summarizer

A small FastAPI web app that summarizes text with a locally stored, fine-tuned T5 model.

## Features

- Paste text into a simple browser interface and request a summary.
- Runs inference with the model stored in `saved_summary_model/`.
- Includes a notebook for training and testing the model.

## Requirements

- Python 3.10 or newer
- Git LFS to download the model weights

## Setup

From the project directory, create and activate a virtual environment, then install dependencies:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

When cloning this repository, install Git LFS before cloning so the model weights are downloaded. If the weights are missing after cloning, run:

```powershell
git lfs install
git lfs pull
```

## Run the app

```powershell
uvicorn app:app --reload
```

Open http://127.0.0.1:8000 in a browser.

The API accepts `POST /summarize/` with JSON such as `{"dialogue": "Text to summarize"}` and returns a `Summary` field.

## Training notebook

`text_summarizer.ipynb` expects the SAMSum CSV files `samsum-train.csv` and `samsum-validation.csv` in the project directory. These data files are not included in this repository; obtain them from the SAMSum dataset source before running the training cells. The notebook samples a subset of the training and validation data.

## Model storage

`saved_summary_model/model.safetensors` is tracked with Git LFS because it exceeds GitHub's regular per-file upload limit. Git LFS must be enabled to retrieve the model weights.
