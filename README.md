# Text Summarizer API

A simple FastAPI backend that summarizes text using Groq's Llama 3.3 70B model, returning structured output (summary + key points) via tool calling.

## Features

- Summarizes any input text into a concise summary
- Extracts 3 to 5 key points separately
- Structured output enforced through Pydantic schemas and Groq tool calling (no unstructured text parsing)

## Tech Stack

- FastAPI
- Pydantic
- Groq API (Llama 3.3 70B)
- python-dotenv

## Project Structure

```
text-summarizer/
├── main.py            # FastAPI app and /summarize endpoint
├── llm_client.py       # Groq client, tool definition, and summarization logic
├── schemas.py          # Pydantic models (SummaryResponse)
├── System_Prompt.py    # System prompt for the summarizer
├── requirements.txt
├── .gitignore
└── README.md
```

## Setup

1. Clone the repo and install dependencies:
   ```
   pip install -r requirements.txt
   ```

2. Create a `.env` file in the root directory:
   ```
   groq_api_key=your_groq_api_key_here
   ```

3. Run the server:
   ```
   uvicorn main:app --reload
   ```

## API Usage

**POST** `/summarize`

Request body:
```json
{
  "message": "Your long text goes here."
}
```

Response:
```json
{
  "summary": "A short summary of the given text.",
  "key_points": [
    "Key point 1",
    "Key point 2",
    "Key point 3"
  ]
}
```

## How It Works

1. The user's text is sent to the Groq API along with a defined tool schema (`SummaryResponse`).
2. Tool calling forces the model to return data matching the exact schema — no manual JSON parsing of free-form text.
3. The returned arguments are validated through Pydantic before being sent back as the API response.

## Notes

This project was built as a structured-output practice exercise, focusing on tool calling with Groq and Pydantic schema validation.
