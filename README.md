# Text Summarizer

A web-based text summarization application built with **FastAPI** and a fine-tuned **T5 Transformer** model. The application provides a simple browser interface where users can enter text and receive an automatically generated summary.

## ✨ Features

- 📝 Simple web interface for entering text
- 🤖 T5-based text summarization
- ⚡ FastAPI backend for inference
- 🌐 Browser-based frontend using HTML, CSS, and JavaScript
- 🧹 Input text preprocessing and cleaning
- 🔌 REST API endpoint for programmatic summarization
- 💻 Automatic device selection: Apple MPS, NVIDIA CUDA, or CPU
- 📓 Training and experimentation notebook included
- 📊 SAMSum dataset files supported for training and validation

## 🛠️ Tech Stack

- **Python**
- **FastAPI**
- **Hugging Face Transformers**
- **PyTorch**
- **T5**
- **HTML / CSS / JavaScript**
- **Jupyter Notebook**

## 📁 Project Structure

```text
Text_Summarizer/
│
├── app.py
├── index.html
├── text_summarizer.ipynb
├── requirements.txt
├── README.md
│
├── samsum-train.csv
├── samsum-validation.csv
├── samsum-test.csv
│
├── saved_summary_model/
│   ├── config.json
│   ├── generation_config.json
│   ├── model.safetensors
│   ├── tokenizer.json
│   └── tokenizer_config.json
│
└── .gitignore
```

> **Note:** The trained model files are intentionally excluded from the GitHub repository because the model is large. The application expects the trained model to be available locally in `saved_summary_model/`.

## ⚙️ Requirements

- Python 3.10 or newer
- A trained T5 model stored in `saved_summary_model/`
- Dependencies listed in `requirements.txt`

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/raushanr64/text-summarizer.git
cd text-summarizer
```

### 2. Create a virtual environment

Windows:

```powershell
py -m venv .venv
```

### 3. Activate the environment

```powershell
.\.venv\Scripts\Activate.ps1
```

### 4. Install dependencies

```bash
python -m pip install -r requirements.txt
```

## 📦 Model Setup

The application loads the trained model from:

```text
./saved_summary_model
```

The backend uses the local model and tokenizer:

```python
model = T5ForConditionalGeneration.from_pretrained("./saved_summary_model")
tokenizer = T5Tokenizer.from_pretrained("./saved_summary_model")
```

Therefore, before running the application, make sure the trained model files are present in the `saved_summary_model/` directory.

> The model is not committed to GitHub because of its large file size.

## ▶️ Run the Application

Start the FastAPI server with:

```bash
uvicorn app:app --reload
```

The application will be available at:

```text
http://127.0.0.1:8000
```

Open that address in your browser.

## 🔄 How It Works

```text
User Input
    ↓
Web Interface
    ↓
FastAPI API
    ↓
Text Cleaning & Preprocessing
    ↓
T5 Tokenizer
    ↓
Fine-tuned T5 Model
    ↓
Generated Summary
    ↓
Browser
```

The input text is cleaned before tokenization. The model accepts up to 512 input tokens and generates a summary using beam search.

## 🔌 API

The application exposes a POST endpoint:

```text
POST /summarize/
```

### Request

```json
{
  "dialogue": "Enter the text you want to summarize."
}
```

### Response

```json
{
  "Summary": "Generated summary."
}
```

The root endpoint:

```text
GET /
```

serves the web interface.

## 🧠 Model Configuration

The summarization generation currently uses:

- Maximum input length: **512 tokens**
- Maximum generated length: **150 tokens**
- Beam search: **4 beams**
- Early stopping: **Enabled**

The application automatically selects the available device in this order:

1. Apple MPS
2. NVIDIA CUDA
3. CPU

## 📓 Training Notebook

The repository includes:

```text
text_summarizer.ipynb
```

The notebook contains the training/testing workflow for the summarization model.

The project uses the **SAMSum** dataset for dialogue summarization. The training and validation CSV files are used by the notebook for model development and evaluation.

## 🎯 Example

### Input

```text
John: Are you coming to the meeting today?
Sarah: Yes, I will join at 3 PM.
John: Great. We need to discuss the new project timeline.
Sarah: Sure, I will prepare the progress report.
```

### Output

```text
John and Sarah will meet at 3 PM to discuss the new project timeline and progress report.
```

## 📌 Current Limitations

- The trained model is not stored directly in the GitHub repository.
- Long input text is truncated to the configured maximum token length.
- Summary quality depends on the fine-tuned model and training data.
- The application currently provides a single summarization endpoint.

## 🔮 Future Improvements

- Add model hosting through Hugging Face Hub
- Add summary length controls
- Add support for uploading text files
- Add PDF/DOCX summarization
- Add multilingual summarization
- Add summary history
- Deploy the application as a public web service
- Add automated evaluation metrics such as ROUGE

## 👨‍💻 Author

**Raushan Kumar Raj**

Diploma in Computer Science & Engineering

## 📄 License

This project is intended for educational and project-development purposes.
