# Multi-Modal RAG

A simple multimodal Retrieval-Augmented Generation pipeline that:
- Extracts text and images from a PDF using PyMuPDF
- Embeds text and images via Hugging Face CLIP
- Stores embeddings in a FAISS vector store
- Retrieves relevant chunks for a query
- Calls Google Gemini via LangChain to answer using text and referenced images

## Project Structure

- `multi.ipynb` — main notebook with the full pipeline
- `multimodal_sample.pdf` — sample PDF used by the notebook

## Requirements

- Python 3.9+
- Packages:
  - pymupdf
  - pillow
  - numpy
  - torch
  - torchvision
  - transformers
  - langchain
  - langchain-community
  - langchain-google-genai
  - scikit-learn
  - python-dotenv
  - faiss-cpu

Install:

```bash
python3 -m pip install pymupdf pillow numpy torch torchvision transformers \
  langchain langchain-community langchain-google-genai scikit-learn python-dotenv faiss-cpu
```

## Environment

Create a `.env` file with your Gemini key:

```
GEMINI_API_KEY=your_key_here
```

The notebook maps this to the variable expected by LangChain’s Google client:

```python
os.environ["GOOGLE_API_KEY"] = os.getenv("GEMINI_API_KEY")
```

## Usage (Notebook)

1. Open `multi.ipynb` in VS Code
2. Select a Python interpreter
3. Run cells to install/import dependencies (restart kernel if needed)
4. Run the pipeline cells and try example queries in the last cell

## Notes

- CLIP model (`openai/clip-vit-base-patch32`) is downloaded from Hugging Face; no OpenAI API key is required
- `ChatGoogleGenerativeAI` uses your Google Gemini API key mapped to `GOOGLE_API_KEY`
- Images are passed to the LLM as base64 strings in the constructed message

## Git

This repo follows a simple notebook-first workflow. Use standard Git commands to commit and push updates:

```bash
git add .
git commit -m "Update notebook and docs"
git push
```
