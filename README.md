# PythonAIAgentFromScratch


# 🧠 Building an AI Agent in Python

This project demonstrates how to build a beginner-friendly **AI Research Assistant Agent** in Python using the **LangChain** framework and **large language models (LLMs)** such as OpenAI’s GPT or Anthropic’s Claude.

The agent can query multiple tools (Wikipedia, DuckDuckGo search, and custom Python functions), structure responses with typed models, and provide clean, programmatically accessible outputs.

---

## 🚀 Features

* 🔹 **AI Research Assistant** powered by GPT/Claude
* 🔹 **Tool integration** with Wikipedia, DuckDuckGo, and custom Python functions
* 🔹 **Structured outputs** using Pydantic for easy integration into code
* 🔹 **Extensible design** – add tools, refine prompts, or customize schemas
* 🔹 **Environment setup** with secure API key management

---

## ⚙️ Setup & Environment

### Requirements

* **Python 3.10+**
* **Virtual environment** (recommended)
* **Code editor** (e.g., VS Code)

### Virtual Environment Setup

```bash
# Create environment
python -m venv venv  

# Activate environment
# Mac/Linux
source venv/bin/activate  
# Windows
.\venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

Example `requirements.txt` should include:

```
langchain
pydantic
duckduckgo-search
wikipedia
python-dotenv
openai
anthropic
```

---

## 🔑 API Keys

Store your API keys securely in a `.env` file:

```bash
OPENAI_API_KEY="your_openai_api_key_here"
ANTHROPIC_API_KEY="your_anthropic_api_key_here"
```

The project loads keys using:

```python
from dotenv import load_dotenv
load_dotenv()
```

---

## 🏗️ Agent Architecture

1. **LLM Configuration**

   * Choose OpenAI (GPT) or Anthropic (Claude).
   * Provide API key and model version.

2. **Structured Output (Pydantic Models)**

   ```python
   from pydantic import BaseModel
   from typing import List

   class ResearchResponse(BaseModel):
       topic: str
       summary: str
       sources: List[str]
       tools_used: List[str]
   ```

3. **Prompt Templates**

   * Define system role and output schema.
   * Placeholder for user queries.
   * Formatting rules enforce compliance with `ResearchResponse`.

4. **Agent & Executor Setup**

   ```python
   from langchain.agents import create_tool_calling_agent, AgentExecutor

   agent = create_tool_calling_agent(llm=llm, prompt=prompt, tools=tools)
   agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
   ```

---

## 🔧 Tool Integration

* **Wikipedia API Wrapper** – fetch encyclopedia knowledge.
* **DuckDuckGo Search** – alternative to Google search.
* **Custom Python Tools** – e.g., save output to file.

Each tool requires:

* **Name** (no spaces)
* **Description** (when and how to use it)

Tools are passed as a list to the agent:

```python
tools = [wikipedia_tool, duckduckgo_tool, custom_tool]
```

---

## ▶️ Running the Agent

Run the Python script after activating your virtual environment:

```bash
python main.py
```

* Input a research query.
* Agent selects tools, processes responses, and returns structured output.
* Example structured response:

```json
{
  "topic": "Quantum Computing",
  "summary": "Quantum computing uses qubits...",
  "sources": ["Wikipedia", "DuckDuckGo"],
  "tools_used": ["wikipedia", "duckduckgo_search"]
}
```

---

## ⚡ Key Takeaways

* **LangChain + LLMs = Powerful AI agents** that can research, analyze, and structure responses.
* **Structured output models** (via Pydantic) make integration with applications seamless.
* **Tool access** extends agent capability beyond text generation to real-world actions.
* **Virtual environments & secure key management** ensure reproducibility and safety.
* **Highly customizable** – add more tools, refine prompts, and extend agent scope.

---

## 📌 Example Use Cases

* Automated **research assistant**
* **Knowledge extraction** from multiple sources
* AI-powered **summarization & synthesis**
* **Pluggable architecture** for custom workflows

---

## 📝 License

This project is licensed under the MIT License – feel free to use and modify for your own projects.
