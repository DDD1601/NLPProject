# Text Summarization Project

## Overview

This project is a **Text Summarization Web Application** that utilizes a fine-tuned **PEGASUS** model for text summarization. It consists of a **Flask-based backend** for handling summarization requests and a **React-based frontend** for user interaction.

## Features

- Summarizes input text using a fine-tuned PEGASUS model.
- Simple and intuitive UI for text input and summarization.
- Flask API backend for model inference.
- Supports GPU acceleration if available.

## Project Structure

```
Text Summarization Project
│── backend
│   │── app.py                 # Flask backend
│   │── requirements.txt       # Dependencies for backend
│── frontend
│   │── public
│   │   └── index.html         # Basic HTML template
│   │── src
│   │   ├── App.js             # Main React Component
│   │   ├── index.js           # React Entry Point
│   │   ├── package.json       # Frontend Dependencies
│   │   ├── package-lock.json  # Package Lock File
│── Text-Summarization-Fine-tuning-Transformers-model.ipynb # Model Fine-Tuning Notebook
```

## Setup and Installation

### Backend Setup

#### Prerequisites:

- Python 3.8+
- CUDA (Optional for GPU acceleration)
- Virtual environment (recommended)

#### Steps:

1. Navigate to the backend folder:
   ```sh
   cd backend
   ```
2. Create a virtual environment (optional but recommended):
   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```
3. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```

### Option 1: Retrain the Model

If you want to fine-tune the PEGASUS model yourself, you can either run the training commands directly in your terminal or execute the provided Jupyter Notebook (`Text-Summarization-Fine-tuning-Transformers-model.ipynb`). The notebook contains step-by-step training instructions, ensuring that you generate a new model and checkpoints for inference.

#### Training Commands:

```sh
pip install transformers[sentencepiece] datasets sacrebleu rouge_score py7zr
python Text-Summarization-Fine-tuning-Transformers-model.ipynb  # Run Jupyter Notebook
```

Alternatively, open the Jupyter Notebook and follow the fine-tuning steps to train the model using the **SAMSum dataset**.

### Option 2: Use a Pretrained Model

If you don’t want to retrain the model, you can download a pretrained PEGASUS model along with the tokenizer from our Google Drive link and use it directly for inference.

#### Steps:

1. Download the pretrained model and tokenizer from [Google Drive](https://drive.google.com/drive/folders/17arjGx9-NPU-AdxjuZGrGkwvYNlzjZcn).
2. Extract the files into a `models` directory inside the `backend` folder.
3. Alternatively, you can download the model manually using the following terminal commands:
   ```sh
   mkdir backend/models && cd backend/models
   wget https://huggingface.co/google/pegasus-cnn_dailymail/resolve/main/pytorch_model.bin
   wget https://huggingface.co/google/pegasus-cnn_dailymail/resolve/main/config.json
   wget https://huggingface.co/google/pegasus-cnn_dailymail/resolve/main/spiece.model
   cd ../..
   ```
4. Ensure the following files exist in `backend/models/`:
   - `pytorch_model.bin`
   - `config.json`
   - `spiece.model`
   - `tokenizer_config.json` 
5. **Check **``** to ensure it correctly loads the model from **``**. If needed, update the model path accordingly.**
6. Run the backend server:
   ```sh
   python app.py
   ```
   The backend will start at `http://localhost:5000/`

### Frontend Setup

#### Prerequisites:

- Node.js and npm

#### Steps:

1. Navigate to the frontend folder:
   ```sh
   cd frontend
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the React frontend:
   ```sh
   npm start
   ```
   The frontend will be available at `http://localhost:3000/`

## API Endpoint

- **Endpoint:** `POST /summarize`
- **Request Body:**
  ```json
  {
    "text": "Your text to summarize here"
  }
  ```
- **Response:**
  ```json
  {
    "summary": "Generated summary here"
  }
  ```

## Model Training & Fine-Tuning

The **fine-tuning process** is documented in `Text-Summarization-Fine-tuning-Transformers-model.ipynb` using **Hugging Face Transformers** and the **SAMSum dataset**.

#### Key Libraries Used:

```sh
pip install transformers[sentencepiece] datasets sacrebleu rouge_score py7zr
```

#### Training Steps:

- Load **SAMSum dataset** (`datasets.load_dataset("samsum")`)
- Tokenize input text and summaries.
- Fine-tune `google/pegasus-cnn_dailymail` using **Hugging Face Trainer**.
- Evaluate using **ROUGE metrics**.
- Save the model and tokenizer for deployment.

## References

- [Hugging Face Transformers](https://huggingface.co/transformers/)
- [SAMSum Dataset](https://huggingface.co/datasets/samsum)
- [PEGASUS Paper](https://arxiv.org/abs/1912.08777)

## Future Improvements

- Deploy on a cloud platform (AWS/GCP/Heroku).
- Add user authentication.
- Support multilingual summarization.
- Optimize model for faster inference.

---

**Author:** Group 21\
**Date:** February 2025

