# ⚖️ AI Legal Mediator CLI (Web-Enabled)

A professional, interactive command-line tool that uses **xAI's Grok** (via the OpenAI-compatible API) to act as an impartial legal mediator.

Unlike standard chatbots, this **active agent** is capable of **Real-Time Web Search**. When specific statutes, case law, or local jurisdiction rules are mentioned, the bot pauses to verify current information before responding—bridging the gap between general legal principles and specific local reality.

## ✨ Key Features

* **🕵️ Active Research Agent:** Equipped with "Tool Use" capabilities. If a user asks about "Florida 2025 Alimony Reform," the bot will search the web via DuckDuckGo to provide up-to-date answers rather than relying on stale training data.
* **💻 Rich Terminal UI:** Uses the `rich` library for beautiful output, including loading spinners during research phases and rendered Markdown for legal text.
* **💾 Robust Session Management:** Save your mediation to a JSON file, auto-save progress, and resume later.
* **↩️ In-Chat Commands:** Use `/undo` to revert mistakes (smartly handles complex search-and-response chains) and `/save` to snapshot the conversation.
* **🛡️ Network Resilience:** Built-in retry logic (via `tenacity`) handles API timeouts or connectivity glitches.

## 🛠️ Requirements

* Python 3.8 or higher
* An API Key from [xAI Console](https://console.x.ai/)

**Install dependencies:**

```bash
pip install openai tenacity rich duckduckgo-search

```

## 🚀 Quick Start

1. **Get your xAI API key** → [https://console.x.ai](https://console.x.ai)
2. **Set the key (recommended)**
*Linux/macOS:*
```bash
export XAI_API_KEY="sk-..."

```


*Windows (PowerShell):*
```powershell
$env:XAI_API_KEY="sk-..."

```


3. **Run the mediator**
```bash
python mediator_bot.py

```


You will be prompted for the dispute topic. Try a specific legal question to test the search, e.g., *"What is the statute of limitations for debt in Texas?"*

## 📖 Usage Examples

```bash
# Basic interactive session (Web Search enabled by default)
python mediator_bot.py

# Start with a specific dispute and auto-save when finished
python mediator_bot.py --topic "Contractor abandoned job site" --save-session construction_dispute.json

# Resume a previous session
python mediator_bot.py --load-session construction_dispute.json

# Use a different model or lower temperature for stricter adherence to facts
python mediator_bot.py --model grok-beta --temperature 0.3

```

## 🎮 In-Chat Commands

While the bot is running, you can type these commands instead of a message:

| Command | Description |
| --- | --- |
| `/undo` | Smart undo. Removes the last user message, the bot's response, and any background search tool calls associated with that turn. |
| `/save` | Manually triggers a save to the session file. |
| `/quit` | Exits the application (saves automatically if `--save-session` is active). |
| `exit` | Same as `/quit`. |

## ⚙️ All Command-Line Options

| Option | Description | Default |
| --- | --- | --- |
| `--model` | Model name (must support Tool Use) | `grok-beta` |
| `--base-url` | API base URL | `https://api.x.ai/v1` |
| `--api-key` | API key (not recommended; use env var instead) | `None` |
| `--topic` | Dispute topic (skips interactive prompt) | `None` |
| `--save-session` | JSON file to save session on exit | `None` |
| `--load-session` | JSON file to load previous conversation | `None` |
| `--max-tokens` | Maximum tokens per response | `1000` |
| `--temperature` | Sampling temperature (0.0–1.0) | `0.5` |

## 💾 Session File Format (JSON)

The session file now includes "Tool" messages, preserving the research history so the bot remembers what it searched for when you reload the session.

```json
[
  {"role": "user", "content": "What is the small claims limit in CA?"},
  {"role": "assistant", "tool_calls": [...]},
  {"role": "tool", "content": "- California Courts: The limit is $12,500 for individuals..."},
  {"role": "assistant", "content": "Mediator: As of 2024, the limit for an individual is $12,500..."}
]

```

## ⚠️ Important Disclaimers

* **Not Legal Advice:** This tool is **not** a licensed attorney or certified mediator.
* **Search Limitations:** While the bot uses web search to find current information, it may still encounter outdated sources or misinterpret search results.
* **Consult Professionals:** Always recommend parties consult qualified legal professionals for binding advice.

## 📄 License

**MIT License (Open Source Use Only)**
Feel free to modify, extend, or integrate into open-source projects.

**Commercial Restriction:**
For commercial use, contact the developer at **tonyelias2012@gmail.com** for further discussions.

> **Note:** Failure to receive exclusive permission from the developer for commercial use of this bot will result in legal action being taken.

Enjoy mediating!
