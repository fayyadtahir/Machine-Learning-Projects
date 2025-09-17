# Vision RAG with Cohere Embed-4 

A powerful visual Retrieval-Augmented Generation (RAG) system that utilizes Cohere's state-of-the-art Embed-4 model for multimodal embedding and Google's efficient Gemini 2.5 Flash model for answering questions about images and PDF pages.

## Features

- **Multimodal Search**: Leverages Cohere Embed-4 to find the most semantically relevant image (or PDF page image) for a given text question.
- **Visual Question Answering**: Employs Google Gemini 2.5 Flash to analyze the content of the retrieved image/page and generate accurate, context-aware answers.
- **Flexible Content Sources**: 
    - Use pre-loaded sample financial charts and infographics.
    - Upload your own custom images (PNG, JPG, JPEG).
    - **Upload PDF documents**: Automatically extracts pages as images for analysis.
- **No OCR Required**: Directly processes complex images and visual elements within PDF pages without needing separate text extraction steps.
- **Interactive UI**: Built with Streamlit for easy interaction, including content loading, question input, and result display.
- **Session Management**: Remembers loaded/uploaded content (images and processed PDF pages) within a session.


## How It Works

The application follows a two-stage RAG process:

1.  **Retrieval**: 
    - When you load sample images or upload your own images/PDFs:
        - Regular images are converted to base64 strings.
        - **PDFs are processed page by page**: Each page is rendered as an image, saved temporarily, and converted to a base64 string.
    - Cohere's `embed-v4.0` model (with `input_type="search_document"`) is used to generate a dense vector embedding for each image or PDF page image.
    - When you ask a question, the text query is embedded using the same `embed-v4.0` model (with `input_type="search_query"`).
    - Cosine similarity is calculated between the question embedding and all image embeddings.
    - The image with the highest similarity score (which could be a regular image or a specific PDF page image) is retrieved as the most relevant context.

2.  **Generation**:
    - The original text question and the retrieved image/page image are passed as input to the Google `gemini-2.5-flash-preview-04-17` model.
    - Gemini analyzes the image content in the context of the question and generates a textual answer.

## Use Cases

- Analyze financial charts and extract key figures or trends.
- Answer specific questions about diagrams, flowcharts, or infographics within images or PDFs.
- Extract information from tables or text within screenshots or PDF pages without explicit OCR.
- Build and query visual knowledge bases (from images and PDFs) using natural language.
- Understand the content of various complex visual documents, including multi-page reports.