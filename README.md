# ModalQ

ModalQ is an AI-powered educational platform that generates interactive learning materials, including custom flashcards, syllabus extraction, and dynamic quizzes, from a variety of file types. The project features a robust AI backend (`ModalQ-ai`) built with Flask, and a frontend for users to interact with these tools.

## Features

- **AI Flashcard Generation**: Upload various file types (PDF, PPT, Image, Audio, Video, URL, Text) and automatically generate interactive flashcards using context-aware AI.
- **Syllabus Extraction**: Upload a course syllabus PDF and extract a structured plan using the Gemini API.
- **Dynamic Quiz Generation**: Automatically generate multiple-choice questions of varying difficulties (Easy, Medium, Hard) tailored to specific grades, subjects, and topics using Cohere.
- **Explainable AI (XAI) Analysis**: Analyzes and classifies text, providing LIME-based explanations and feature importance plots to make AI predictions transparent.

## Tech Stack & APIs

### Backend (ModalQ-ai)
- **Framework**: Flask (Python)
- **Machine Learning / AI**: TensorFlow, Keras, Transformers (DistilBERT), LIME, SHAP, PyTesseract
- **External API Integrations**: 
  - Cohere API
  - Google Gemini API
  - YouTube API
  - HuggingFace API
  - Pinecone API

### Frontend
- The rest of the repository contains the frontend codebase which communicates with the `ModalQ-ai` backend APIs.

## Setup Instructions

### Prerequisites
- Python 3.8+
- System dependencies for PyTesseract (e.g., `tesseract-ocr`)

### Backend Setup (`ModalQ-ai`)
1. Navigate to the AI directory:
   ```bash
   cd ModalQ-ai
   ```
2. Install the required Python packages:
   ```bash
   pip install flask flask-cors cohere transformers tensorflow pytesseract lime shap pandas matplotlib seaborn python-dotenv
   ```
   *(Ensure any other dependencies required by the specific scripts are also installed.)*

3. Create a `.env` file in the `ModalQ-ai` directory and add your API keys:
   ```env
   YOUTUBE_API_KEY=your_youtube_api_key
   COHERE_API_KEY=your_cohere_api_key
   GEMINI_API_KEY=your_gemini_api_key
   HUGGINGFACE_API_KEY=your_huggingface_api_key
   PINECONE_API_KEY=your_pinecone_api_key
   ```

4. Run the Flask server:
   ```bash
   python app.py
   ```
   The backend will start running on `http://0.0.0.0:5000`.

## API Endpoints Overview

- `POST /generate_flashcard`: Accepts a file and parameters (`filetype`, `grade`) to generate flashcards.
- `POST /generate_syllabus`: Accepts a PDF file to extract and process the syllabus.
- `POST /start_quiz`: Accepts JSON (`{"grade": "...", "subject": "...", "topic": "..."}`) and returns a dictionary of generated quiz questions.
- `POST /ai_flashcard`: Accepts form data (`subject`, `grade`, `topic`, `cohere_api_key`) and generates AI flashcards via RAG.
- `POST /predict`: Accepts JSON (`{"text": "..."}`) and returns an XAI report explaining the model's text classification.

## Project Structure

- `ModalQ-ai/`: Contains the Flask API backend and machine learning scripts.
  - `app.py`: Main application entry point defining the API routes.
  - `rushabh.py`: Additional script handling Cohere-based question generation.
  - `scripts/`: Directory containing specific utility modules for RAG querying, syllabus extraction, media processing (PDF, PPT, Audio, Video, Image), and quiz generation.
- The rest of the repository contains the frontend application and related assets.
