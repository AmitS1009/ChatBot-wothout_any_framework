
# Conversation Management & Summarization using Groq API

This project demonstrates managing a running chat history with an AI assistant while **truncating old messages** and **periodically summarizing conversation history** using the Groq API.

---

## 📌 Objective

- Maintain a running **conversation history** between a user and an AI assistant.
- Limit memory by keeping only the **last N turns** (`MAX_TURNS`).
- Periodically **summarize older parts of the conversation** to preserve context efficiently.
- Designed for **interactive command-line chats**.

---

## 🛠️ Dependencies

- Python 3.x  
- Groq SDK (`pip install groq`)  
- Optional: `requests` (used for potential API calls outside Groq)  

---

## ⚡ Setup

1. Set your **Groq API Key**:

```python
import os
os.environ["GROQ_API_KEY"] = "<YOUR_API_KEY>"
````

2. Initialize the Groq client:

```python
from groq import Groq
client = Groq(api_key=os.environ["GROQ_API_KEY"])
```

3. Configure conversation settings:

```python
MAX_TURNS = 3                    # Maximum user-assistant turns to keep
SUMMARIZE_AFTER_N_TURNS = 3      # Summarize every 3 turns
MODEL_NAME = "llama-3.1-8b-instant"
```

---

## 🔧 How It Works

1. **Conversation Loop**

   * User types input.
   * AI responds using Groq's `chat.completions.create`.
   * Messages appended to `convo_history`.

2. **Truncation**

   * Keeps only the last `MAX_TURNS` user-assistant pairs (to avoid memory bloat).

3. **Periodic Summarization**

   * After every `SUMMARIZE_AFTER_N_TURNS`:

     * All prior messages (except the latest assistant reply) are summarized.
     * The summary replaces the old messages in the history.
     * Latest assistant reply is retained for continuity.

4. **Output**

   * Prints the AI’s reply to the user.
   * Prints a short summary snippet when summarization occurs.

---

## 🚀 Example

```text
User: Hello
Assistant: Hi! How can I help you?
User: I need help with my project
Assistant: Sure! What’s the project about?
...
🔄 Summarizing conversation history...
📌 Summary stored: Project discussion includes AI-based data extraction, Python implementation...
```

**Behavior:**

* Only last 3 turns are kept in memory.
* Older context is summarized and stored as a system message.

---

## 📝 Features

* Limits memory usage via truncation.
* Maintains **context-aware chat** using periodic summaries.
* Can be integrated with chatbots or assistants for efficient long conversations.
* Supports any Groq-compatible chat model.

---

## ⚠️ Notes

* Summarization may fail if API call errors occur; fallback is retaining truncated history.
* Ensure the Groq API key is valid and the model is active.
* Designed for terminal/CLI-based interaction; can be extended for web or GUI interfaces.

---

## 🔗 References

* [Groq Python SDK Documentation](https://www.groq.ai/docs)
* [JSON Schema](https://json-schema.org/) (for structured data extraction if combined with Task 2)

---

**Author:** Amit Kushwaha

