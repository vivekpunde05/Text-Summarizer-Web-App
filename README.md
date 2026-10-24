# 📝 Text Summarizer Web App

[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![HuggingFace](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Transformers-FFD21E?style=for-the-badge)](https://huggingface.co/docs/transformers/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Google T5](https://img.shields.io/badge/Google-T5%20Model-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://huggingface.co/docs/transformers/model_doc/t5)
[![Uvicorn](https://img.shields.io/badge/Uvicorn-499848?style=for-the-badge&logo=uvicorn&logoColor=white)](https://www.uvicorn.org/)
[![Jinja2](https://img.shields.io/badge/Jinja2-B41717?style=for-the-badge&logo=jinja&logoColor=white)](https://jinja.palletsprojects.com/)
[![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=for-the-badge&logo=pydantic&logoColor=white)](https://docs.pydantic.dev/)

An end-to-end Text & Dialogue Summarization web application powered by [**FastAPI**](https://fastapi.tiangolo.com/), [**Hugging Face Transformers (T5)**](https://huggingface.co/docs/transformers/), and [**PyTorch**](https://pytorch.org/). The app provides both a clean, modern user interface for interactive text summarization and a fast RESTful API endpoint for programmatic access.

---

## 🚀 Features

- **T5-Powered Summarization**: Utilizes a fine-tuned Google T5 (Text-to-Text Transfer Transformer) model for generating concise summaries.
- **Hardware Acceleration**: Automatically detects and leverages GPU acceleration via **NVIDIA CUDA** or **Apple Silicon MPS**, falling back gracefully to **CPU**.
- **Interactive Web Interface**: Simple and responsive UI to paste or write text/dialogue and get summaries instantly without page refreshes.
- **RESTful API**: Fast, async API endpoint (`/summarize/`) for seamless integration with other services.
- **Auto-generated API Docs**: Interactive Swagger (`/docs`) and ReDoc (`/redoc`) documentation out of the box with FastAPI.

---

## 🛠️ Tech Stack

- **Backend Framework**: [FastAPI](https://fastapi.tiangolo.com/) & [Uvicorn](https://www.uvicorn.org/)
- **Machine Learning & NLP**: [Hugging Face Transformers](https://huggingface.co/docs/transformers/) & [PyTorch](https://pytorch.org/)
- **Templating**: [Jinja2](https://jinja.palletsprojects.com/)
- **Data Validation**: [Pydantic](https://docs.pydantic.dev/)
- **Frontend**: HTML5, CSS3, Vanilla JavaScript (Fetch API)

---

## 📁 Project Structure

```text
Text Summarizer App/
├── app.py                 # FastAPI application, model loader, and API routes
├── index.html             # Frontend interface template
├── README.md              # Project documentation
└── saved_summary_model/   # Trained/Fine-tuned T5 model and tokenizer artifacts
    ├── config.json
    ├── generation_config.json
    ├── model.safetensors
    ├── tokenizer.json
    └── tokenizer_config.json
```

---

## ⚙️ Installation & Setup

### 1. Prerequisites
- Python 3.9 or higher installed on your system.
- Recommended: A virtual environment (venv or conda).

### 2. Clone / Open Project
Open a terminal in the project root directory:
```bash
cd "Text Summarizer App"
```

### 3. (Optional) Create and Activate a Virtual Environment
- **Windows (PowerShell)**:
  ```powershell
  python -m venv venv
  .\venv\Scripts\Activate.ps1
  ```
- **Linux / macOS**:
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### 4. Install Dependencies
Install the required Python packages:
```bash
pip install fastapi uvicorn transformers torch jinja2 pydantic
```
*(If you have a compatible NVIDIA GPU, install PyTorch with CUDA support from [pytorch.org](https://pytorch.org/get-started/locally/)).*

---

## 🖥️ Running the Application

Start the Uvicorn development server:

```bash
uvicorn app:app --reload
```

- **Web Interface**: Open your browser and navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000)
- **Interactive Swagger Docs**: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **Alternative API Docs**: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 📡 API Reference

### 1. Web Page
- **Method**: `GET`
- **Path**: `/`
- **Description**: Renders and returns the HTML user interface.

---

### 2. Summarize Text
- **Method**: `POST`
- **Path**: `/summarize/`
- **Header**: `Content-Type: application/json`

#### Request Body:
```json
{
  "dialogue": "Alice: Hi Bob, are you coming to the party tonight? Bob: Yes, I will be there around 8 PM."
}
```

#### Response (200 OK):
```json
{
  "summary": "alice is coming to the party tonight around 8 pm."
}
```

#### Example using `curl`:
```bash
curl -X POST "http://127.0.0.1:8000/summarize/" \
     -H "Content-Type: application/json" \
     -d "{\"dialogue\": \"John went to the store to buy apples, bananas, and oranges. He met Sarah there and they decided to grab lunch together.\"}"
```

#### Example using Python (`requests`):
```python
import requests

url = "http://127.0.0.1:8000/summarize/"
payload = {
    "dialogue": "Alice: Did you finish the report? Bob: Almost done, will send it by 4 PM."
}
response = requests.post(url, json=payload)
print(response.json())
```

---

## 🔧 Model Configuration

Generation parameters can be customized in [app.py](file:///d:/Text%20Summarizer%20App/app.py) inside the `summarize_dialogue` function:

```python
targets = model.generate(
    input_ids=inputs["input_ids"],
    attention_mask=inputs["attention_mask"],
    max_length=150,        # Maximum length of the generated summary
    num_beams=4,           # Number of beams for beam search
    early_stopping=True
)
```

---

## 📄 License
This project is open-source and available under the [MIT License](LICENSE).
