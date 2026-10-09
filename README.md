# Interview Prep Chatbot

A simple Streamlit app that simulates a job interview. You enter your background and the role you're targeting, an AI "HR executive" interviews you, and at the end you get a score and written feedback.

## How It Works

The app moves through three stages, tracked with Streamlit session state:

1. **Setup** – Enter your name, experience and skills, then choose a level (Junior / Mid-level / Senior), a position (Data Scientist, Data Engineer, ML Engineer, BI Analyst, Financial Analyst) and a company (Amazon, Meta, Udemy, 365 Company, Nestle, LinkedIn, Spotify).
2. **Interview** – The chatbot (OpenAI `gpt-4o`) is given a system prompt built from your details and asks interview questions. Responses are streamed live. You get 5 answers in total; the AI replies to the first 4, and your 5th answer ends the interview.
3. **Feedback** – Click **Get Feedback** and a second `gpt-4o` call reviews the full transcript and returns an overall score (1–10) plus written feedback. **Restart Interview** reloads the page.

## Tech Stack

- [Streamlit](https://streamlit.io/) – UI and session state
- [OpenAI Python SDK](https://github.com/openai/openai-python) – chat completions (`gpt-4o`)
- [streamlit-js-eval](https://github.com/aghasemi/streamlit_js_eval) – used to reload the page on restart

## Getting Started

### 1. Install dependencies

```bash
pip install streamlit openai streamlit-js-eval
```

### 2. Add your OpenAI API key

Create `.streamlit/secrets.toml` in the project folder:

```toml
OPENAI_API_KEY = "your-openai-api-key"
```

### 3. Run the app

```bash
streamlit run app.py
```

(Replace `app.py` with your script's filename.)

## Deploying to Streamlit Community Cloud

Push the code to GitHub, create a new app on Streamlit Community Cloud, and add `OPENAI_API_KEY` under **Settings → Secrets**.

## Possible Improvements

- Use `st.session_state` for the system prompt to include interview-style instructions (e.g. ask one question at a time).
- Add a `requirements.txt` for reproducible installs.
- Make the question limit, model, and company/position lists configurable.
- Add error handling for failed API calls.

## Notes

- Never commit your API key; keep it in Streamlit secrets.
- Each interview and feedback request uses OpenAI API credits.
