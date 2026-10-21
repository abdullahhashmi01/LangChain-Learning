# LangChain Learning

Hands-on notebooks for learning the modern LangChain API (`langchain` v1 and `langgraph`). Each notebook covers one core concept with small, runnable examples, mostly using Groq's `openai/gpt-oss-120b` model, with OpenAI and Google Gemini examples where relevant.

## Notebooks

All notebooks are in the `updatedlangchain/` folder.

| Notebook                 | What it covers                                                                                                                                                               |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `langchain_intro.ipynb`  | Loading API keys with `python-dotenv`, `init_chat_model`, and direct integrations with OpenAI (`ChatOpenAI`), Google Gemini (`ChatGoogleGenerativeAI`) and Groq (`ChatGroq`) |
| `modelintegration.ipynb` | Streaming responses chunk by chunk with `model.stream()`, and running many prompts in parallel with `model.batch()` (including `max_concurrency`)                            |
| `messages.ipynb`         | Text prompts vs message prompts, `SystemMessage`, `HumanMessage`, `AIMessage`, `ToolMessage`, message metadata (`name`, `id`) and `usage_metadata`                           |
| `structuredoutput.ipynb` | Getting typed output with `with_structured_output()` using Pydantic models, nested schemas, `TypedDict`, `include_raw=True`, and `response_format` in `create_agent`         |
| `tools.ipynb`            | Defining tools with `@tool`, binding them with `bind_tools()`, reading `tool_calls`, building agents with `create_agent`, and a manual tool execution loop                   |
| `middleware.ipynb`       | Agent middleware: `SummarizationMiddleware` (trigger by message count, tokens or fraction) and `HumanInTheLoopMiddleware` (approve, reject and edit tool calls)              |

## Topics in more detail

**Model integration.** Switching between providers (OpenAI, Gemini, Groq) with the same `.invoke()` interface.

**Messages.** How a conversation is represented as a list of typed messages, and how to attach metadata and tool calls to message history.

**Structured output.** Forcing the model to return data that matches a schema, so results can be used directly in code.

**Tools and agents.** Letting a model call Python functions, and wrapping that loop with `create_agent`.

**Middleware.**

- _Summarization_ compresses old conversation history when it grows past a limit, keeping recent messages.
- _Human-in-the-loop_ pauses the agent before sensitive tool calls (for example sending an email) so a person can approve, reject or edit the call. Resuming uses `Command(resume={"decisions": [...]})` with the same `thread_id`.

## Setup

**Requirements:** Python 3.11+ and [uv](https://docs.astral.sh/uv/) (or `pip`).

```bash
# clone the repo
git clone https://github.com/abdullahhashmi01/LangChain-Learning.git
cd LangChain-Learning

# install dependencies with uv
uv sync

# or with pip
pip install -r requirements.txt
```

### API keys

Create a `.env` file in the project root (this file is git-ignored, never commit it):

```env
GROQ_API_KEY=your_groq_key
OPENAI_API_KEY=your_openai_key
GOOGLE_API_KEY=your_google_key
```

You only need the keys for the providers you want to try. Most notebooks only need `GROQ_API_KEY`.

## Running

Open any notebook in VS Code, Jupyter or your IDE, select the project's `.venv` as the kernel, and run the cells from top to bottom.

```bash
jupyter lab
```

## Project structure

```
LangChain-Learning/
├── updatedlangchain/
│   ├── langchain_intro.ipynb
│   ├── modelintegration.ipynb
│   ├── messages.ipynb
│   ├── structuredoutput.ipynb
│   ├── tools.ipynb
│   └── middleware.ipynb
├── src/langchain_updated/
├── pyproject.toml
├── requirements.txt
└── README.md
```

## Tech stack

- [LangChain](https://python.langchain.com/)
- [LangGraph](https://langchain-ai.github.io/langgraph/)
- [Groq](https://groq.com/), [OpenAI](https://openai.com/), [Google Gemini](https://ai.google.dev/)
- [Pydantic](https://docs.pydantic.dev/)
- [python-dotenv](https://pypi.org/project/python-dotenv/)

## Notes

These notebooks are my personal learning notes, so some cells contain experiments and intentional mistakes while debugging. Model names may change over time, so update them if a provider retires a model.
