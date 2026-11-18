# ragtune

ragtune is a Python and Streamlit app for evaluating Retrieval-Augmented Generation (RAG) pipelines. Compare LLMs, embedding models, query transformations, and rerankers using your documents and reference answers. Automated optimization is planned but not yet available.

## Features

- Evaluate generated answers and retrieved context with Ragas metrics.
- Compare LLMs and embedding models across pipeline configurations.
- Test query transformations and rerankers from the Rerankers library.
- Add model providers and pipeline options by editing the Python configuration.

## Installation

Use Python 3.10 or newer. From the project root, create a virtual environment and install the dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Document loading uses [Unstructured](https://www.unstructured.io/). Install the system dependencies needed for your file types:

- `libmagic-dev` for file type detection.
- `poppler-utils` and `tesseract-ocr` for images and PDFs.
- `libreoffice` for Microsoft Office documents.
- `pandoc` for EPUB, RTF, and OpenOffice documents. RTF support requires Pandoc 2.14.2 or newer.

Create a `.env` file in the project root with the API keys for the providers you intend to use:

```plaintext
OPENAI_API_KEY=sk-xyz
COHERE_API_KEY=cohere-xyz
ANTHROPIC_API_KEY=anthropic-xyz
```

Replace the placeholder values with your keys. Do not commit this file. Some Hugging Face rerankers also require accepting the model's terms of use.

## Usage

Start the app from the project root:

```bash
streamlit run Home.py
```

Open the address printed by Streamlit if your browser does not open automatically.

1. Add your documents, evaluation questions, and corresponding ground-truth answers in the app.
2. Follow each section's steps in order to configure and run the pipeline.
3. Review the evaluation results before changing configurations and running another comparison.

Missing dataset inputs or skipped steps can cause errors, including error boxes on tabs that depend on earlier results. Evaluations can make many API calls and incur provider charges.

The evaluation metrics include answer relevancy, answer similarity, answer correctness, context precision, context recall, and context entity recall. See the [Ragas metric documentation](https://docs.ragas.io/en/stable/concepts/metrics/) for definitions.

To add an LLM provider, update `llm_options`, install its required LangChain integration, and load any necessary API keys in `Home.py`. Embedding models, rerankers, and query transformations can also be extended in the code.

## License

Licensed under the MIT License. This project is based on [misbahsy/RAGTune](https://github.com/misbahsy/RAGTune). See `LICENSE` for the full terms, and retain the original copyright and permission notice when redistributing the code.
