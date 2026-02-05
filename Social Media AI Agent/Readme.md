# 🤖 AI Social Architect: Multi-Agent Workflow

[![n8n](https://img.shields.io/badge/Orchestration-n8n-FF6C37?logo=n8n)](https://n8n.io/)
[![LLM](https://img.shields.io/badge/LLM-OpenAI%20/%20Anthropic-412991?logo=openai)](https://openai.com/)
[![Interface](https://img.shields.io/badge/Interface-Telegram-26A5E4?logo=telegram)](https://telegram.org/)

An advanced **Multi-Agent Orchestration** system built in n8n that transforms visual assets into brand-aligned social media content. This project demonstrates a production-grade AI pipeline featuring **LLM-as-a-Judge** scoring and a stateful **Human-in-the-Loop** feedback loop.

---

## 🏗️ Architecture & Multi-Agent Roles

Instead of a single prompt, this workflow distributes intelligence across specialized agents to ensure professional-grade output:

1.  **The Visionary Agent (Perception)**: Analyzes the uploaded image to extract technical metadata (lighting, composition, mood) and aesthetic context.
2.  **The Creative Voice (Generation)**: Processes the vision data to draft minimalist captions. It is connected to **Session Memory** to allow for iterative edits.
3.  **The Critic Agent (LLM-as-a-Judge)**: Acts as an automated quality gate. It evaluates the caption against a strict **Brand Rubric** and assigns a score.



---

## 🧠 Key Technical Features

### 1. LLM-as-a-Judge (Rubric Scoring)
The workflow implements an automated evaluation step. The **Critic Agent** uses a set of rubrics to grade the content:
* **Minimalism**: Is the text concise? (0-10)
* **Aesthetic**: Does it follow the "lowercase-only" brand rule? (0-10)
* **Quality Gate**: An `If Node` acts as a filter; only posts scoring **7/10 or higher** are forwarded for approval.

### 2. Human-in-the-Loop (HITL) & Stateful Memory
Unlike linear automations, this workflow supports a **Feedback Loop**:
* **Session ID Tracking**: Uses `{{ $json.message.chat.id }}` to maintain conversation history.
* **Edit Requests**: Users can reply to the bot (e.g., *"Add 4 hashtags"* or *"Make it punchier"*).
* **Smart Routing**: A `Switch Node` detects if the input is a **New Photo** (starts a new process) or **Text Feedback** (updates the current draft via memory).

---

## 🚦 Workflow Logic

1.  **Ingress**: Telegram Trigger receives photo/text.
2.  **Logic Branch**: 
    * **Photo?** → Visionary → Creative → Critic → User.
    * **Text?** → Creative (w/ Memory) → User.
3.  **Memory Port**: `Window Buffer Memory` stores the last 5-10 interactions to maintain context for edits.

---

## 🛠️ Setup Instructions

1.  **Import**: Import the provided `n8n_multi_agent_social_bot.json` into n8n.
2.  **Credentials**: 
    * Set up a **Telegram Bot** via `@BotFather`.
    * Connect your **LLM Provider** (OpenAI, Anthropic, etc.).
3.  **Session Key**: Verify the Memory node is using the dynamic expression:
    ```javascript
    {{ $node["Telegram Trigger"].json.message.chat.id }}
    ```
4.  **Activate**: Turn the workflow on and send a photo to your bot to begin.

---

## 🛠️ Infrastructure Options: Cloud vs. Local

This workflow is designed with a **Hybrid-Ready** architecture. While the default path uses high-reasoning Cloud LLMs, an **unconnected Ollama node** is included to allow for immediate local transition.

### ⚖️ Strategy Comparison

| Feature | Cloud (OpenAI/Anthropic) | Local (Ollama - Optional) |
| :--- | :--- | :--- |
| **Reasoning Power** | High (Best for "Critic" role) | Medium (Best for "Visionary" role) |
| **Privacy** | Standard API Privacy | **100% Private** (Data stays on-device) |
| **Cost** | Pay-per-token | **Free** (Unlimited usage) |
| **Infrastructure** | No setup required | Requires Local GPU + Ngrok Tunnel |

---

## 🏠 Optional: Activating Local Inference (Ollama)

For users prioritizing privacy or zero-cost image processing, the workflow includes a pre-configured (but unconnected) **Ollama node**:

1.  **Install Ollama**: Run `ollama serve` on your local hardware.
2.  **Model**: Pull a vision-capable model: `ollama pull llama3.2-vision`.
3.  **Local-to-Cloud Tunnel**: Since Telegram requires a public endpoint, use **Ngrok** to expose your local n8n instance:
    ```bash
    ngrok http 5678
    ```
4.  **Activation**: Simply connect the Ollama node to the **Switch** output to swap cloud processing for local inference.

## 📸 Preview

![Workflow Screenshot](./Social_AI_Agent.png)
