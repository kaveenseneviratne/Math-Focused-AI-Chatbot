# Math-Focused AI Chatbot (LangChain + LangGraph)

This project is a simple interactive **AI chatbot** built with:

-   **LangChain**
-   **LangGraph**
-   **OpenAI's Chat Models**
-   **Custom Tools** (calculator + greeting tool)

The chatbot runs in your terminal and can: - Perform basic arithmetic -
Greet users - Respond conversationally using an LLM - Stream responses
token-by-token for a smooth chat experience

------------------------------------------------------------------------

## Features

### Custom Tools

This chatbot includes two example tools:

**1. Calculator Tool**\
Performs basic arithmetic and returns results.

**2. Say Hello Tool**\
Greets users with a friendly message.

These tools are integrated into a **ReAct agent** using LangGraph,
letting the model decide when to call them.

------------------------------------------------------------------------

## Project Structure

    project/
    │
    ├── main.py          # Main chatbot logic
    ├── .env             # Stores your OpenAI API key (NOT committed)
    ├── requirements.txt / pyproject.toml
    └── README.md

------------------------------------------------------------------------

## Setup

### Create & activate a virtual environment

``` bash
python3 -m venv venv
source venv/bin/activate
```

### Install dependencies

If using pip:

``` bash
pip install -r requirements.txt
```

If using `uv`:

``` bash
uv sync
```

------------------------------------------------------------------------

## Environment Variables

Create a `.env` file in the project root:

    OPENAI_API_KEY=your_api_key_here

 **Never commit your `.env` file to GitHub.**\
Ensure `.env` is listed in `.gitignore`.

------------------------------------------------------------------------

## Running the Chatbot

Start the chatbot with:

``` bash
python main.py
```

You will see:

    Welcome! I'm your AI assistant. Type 'quit' to exit.
    You can ask me to perform calculations or chat with me.

Now you can type questions like:

-   "Add 12 and 8"
-   "Say hello to John"
-   "What is 5 + 7?"
-   "Tell me something interesting"

Type `quit` to exit.

------------------------------------------------------------------------

## How It Works

### LangGraph + ReAct Agent

The script uses LangGraph's `create_react_agent` to build an agent that
can:

-   Analyze the user's request
-   Call tools when needed
-   Respond conversationally
-   Stream output for real-time responses

### Streaming Responses

Responses are streamed chunk by chunk:

``` python
for chunk in agent_executor.stream(...):
    ...
```

This creates a smooth, dynamic interactive experience.

------------------------------------------------------------------------

## Tools Implemented

### Calculator Tool

``` python
@tool
def calculator(a: float, b: float) -> str:
    return f"The sum of {a} and {b} is {a + b}"
```

### Greeting Tool

``` python
@tool
def say_hello(name: str) -> str:
    return f"Hello {name}, I hope you are well today"
```

These are registered with the agent:

``` python
tools = [calculator, say_hello]
```

------------------------------------------------------------------------

## Requirements

-   Python 3.10+
-   langchain-core
-   langchain-openai
-   langgraph
-   python-dotenv


