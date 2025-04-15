# Blog Title Suggestion API

This repository provides a simple Django-based API for suggesting blog post titles using the GPT-2 model from Hugging Face's Transformers library. The service exposes a single endpoint, `/suggest-titles/`, which accepts blog post content via a POST request and returns three AI-generated title suggestions.

> **Note:** All development and testing for this project were performed on a Kaggle notebook environment, as my local machine did not have sufficient resources to run the GPT-2 model.

## Features

- **Django server**: Lightweight setup with minimal dependencies.
- **GPT-2 integration**: Uses the `transformers` library to generate title suggestions.
- **Ngrok tunneling**: Exposes the local Django server via a public URL for easy testing.
- **Single-file implementation**: All code resides in `main.py` for simplicity.

## Prerequisites

- Python 3.7+
- Internet connection (for downloading model weights and using ngrok)
- Kaggle notebook or similar environment with GPU support

## Installation

1. **Clone the repository** (or copy the files into your workspace).

2. **Install dependencies**:
   ```bash
   pip install django transformers torch pyngrok
   ```

3. **Create `main.py`**:
   Ensure that `main.py` contains the full implementation, including:
   - Django settings configuration
   - GPT-2 model loading
   - Ngrok authentication
   - Endpoint definition
   - Server launch logic

4. **Set your Ngrok auth token**:
   In `main.py`, replace the placeholder with your actual ngrok token:
   ```python
   conf.get_default().auth_token = "YOUR_NGROK_AUTH_TOKEN"
   ```

## Usage

1. **Run the server**:
   ```bash
   python3 main.py
   ```

2. **Note the public URL**:
   After launching, you'll see an output like:
   ```
   🔗 Public URL: http://xxxxx.ngrok.io
   📮 POST to /suggest-titles/
   ```

3. **Test the endpoint**:
   ```bash
   curl -X POST http://xxxxx.ngrok.io/suggest-titles/ \
     -H "Content-Type: application/json" \
     -d '{"content": "Your blog post text here"}'
   ```

4. **Response**:
   ```json
   {
     "titles": [
       "Title Suggestion 1",
       "Title Suggestion 2",
       "Title Suggestion 3"
     ]
   }
   ```

## Notes

- The service uses port `8001` by default to avoid conflicts in notebook environments.
- Django's autoreload is disabled (`--noreload`) to prevent issues in async notebook kernels.
- Make sure your Kaggle notebook allows outbound HTTP connections for ngrok.
