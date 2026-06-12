# LangChain + Gemini + LangSmith Prompt Hub

A simple project demonstrating how to:

* Connect Google Gemini with LangChain
* Enable LangSmith tracing
* Run prompts using Gemini
* Create a LangChain chain
* Push and manage prompts in LangSmith

This project is useful for learning prompt engineering, prompt versioning, and LLM observability.

---

##  Project Overview

This project performs two main tasks:

### 1️⃣ Gemini LLM Invocation

The application connects to Google's Gemini model using LangChain and sends a prompt:

> "Explain how LangSmith tracing works in one sentence."

The model generates a response which is displayed in the notebook.

---

### 2️⃣ Prompt Management with LangSmith

The project creates a reusable prompt template:

```python
Tell me a brief {style} joke about {topic}.
```

It then:

* Combines the prompt with Gemini
* Creates a LangChain chain
* Pushes the chain to LangSmith Prompt Hub
* Generates a shareable URL for future use

---

## Technologies Used

* Python
* Google Gemini 2.5 Flash
* LangChain
* LangSmith
* Google Colab

---

##  Project Structure

```text
project/
│
├── notebook.ipynb
├── README.md
└── requirements.txt
```

---

##  Installation

Install the required libraries:

```bash
pip install langchain_openai
pip install langchain_google_genai
pip install langsmith
```

---

##  Environment Setup

Store your API keys in Google Colab Secrets.

Required secrets:

| Secret Name | Purpose               |
| ----------- | --------------------- |
| geminikey   | Google Gemini API Key |
| task        | LangSmith API Key     |

Set environment variables:

```python
os.environ["GOOGLE_API_KEY"] = userdata.get("geminikey")
os.environ["LANGSMITH_API_KEY"] = userdata.get("task")
```

Enable tracing:

```python
os.environ["LANGSMITH_TRACING"] = "true"
os.environ["LANGSMITH_PROJECT"] = "my-langchain-project"
```

---

##  Running Gemini

Initialize the Gemini model:

```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash"
)
```

Invoke the model:

```python
response = llm.invoke(
    "Explain how LangSmith tracing works in one sentence."
)

print(response.content)
```

---

## What is LangSmith Tracing?

LangSmith tracing helps developers monitor and debug LLM applications by recording:

* Prompts
* Model responses
* Execution steps
* Token usage
* Chain workflows

This makes it easier to understand what happens inside your AI application.

---

##  Creating a Prompt Template

```python
prompt = ChatPromptTemplate.from_template(
    "Tell me a brief {style} joke about {topic}."
)
```

Example:

```python
Tell me a brief funny joke about AI.
```

---

## 🔗 Building a LangChain Chain

```python
chain = prompt | model
```

This pipeline:

```text
User Input
     ↓
Prompt Template
     ↓
Gemini Model
     ↓
Generated Response
```

---

## ☁️ Pushing Prompts to LangSmith

Push the chain to LangSmith Prompt Hub:

```python
url = client.push_prompt(
    "gemini-joke-generator",
    object=chain
)
```

Output:

```python
Successfully pushed prompt!
```

A URL will be generated where the prompt can be viewed and managed.

---

## 📊 Benefits of LangSmith

* Prompt Version Control
* Experiment Tracking
* LLM Debugging
* Tracing & Monitoring
* Team Collaboration
* Prompt Sharing

---

##  Learning Outcomes

After completing this project, you will understand:

* How LangChain integrates with Gemini
* How to create prompt templates
* How LangSmith tracing works
* How to build chains
* How to store and manage prompts in LangSmith

---

## 📸 Workflow

```text
Google Colab
      ↓
Load API Keys
      ↓
Initialize Gemini
      ↓
Send Prompt
      ↓
Receive Response
      ↓
Create Prompt Template
      ↓
Build Chain
      ↓
Push to LangSmith
      ↓
Manage & Trace Prompts
```

---

## Future Improvements

* Add multiple prompt templates
* Create AI chatbots
* Integrate LangGraph agents
* Add memory support
* Build RAG applications
* Deploy as a web application

---

## Author

Built for learning LangChain, Gemini, and LangSmith prompt management.
