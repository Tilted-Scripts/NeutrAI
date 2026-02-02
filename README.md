# ⚖️ AI Legal Mediator CLI

A professional, interactive command-line tool that uses **xAI's Grok** (via the OpenAI-compatible API) to simulate an impartial legal mediator.

This bot facilitates disputes between two parties ("Party A" and "Party B") by listening to arguments, asking clarifying questions, and suggesting resolutions based on common legal principles—all rendered in a beautiful, readable terminal interface.

## ✨ Features

* **Rich Terminal UI:** Uses the `rich` library for colored output, loading spinners, and properly rendered Markdown (headers, lists, bold text) for AI responses.
* **Session Management:** Save your mediation to a JSON file and resume it later.
* **In-Chat Commands:** Use `/undo` to revert mistakes and `/save` to snapshot the conversation mid-stream.
* **Network Resilience:** Built-in retry logic (via `tenacity`) handles API timeouts or temporary connection glitches gracefully.
* **Flexible Configuration:** Compatible with xAI (Grok), OpenAI, or any other OpenAI-compatible endpoint.

## 🛠️ Requirements

* Python 3.8 or higher
* An API Key from [xAI Console](https://console.x.ai/)

**Install dependencies:**

```bash
pip install openai tenacity rich

```

## 🚀 Quick Start

1. **Get your xAI API key** → [https://console.x.ai](https://console.x.ai)
2. **Set the key (recommended)** *Linux/macOS:*
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


You’ll be prompted for the dispute topic, then alternate between **Party A** and **Party B**.

## 📖 Usage Examples

```bash
# Basic interactive session
python mediator_bot.py

# Start with a specific dispute and auto-save when finished
python mediator_bot.py --topic "Neighbor fence encroachment dispute" --save-session fence_case.json

# Resume a previous session
python mediator_bot.py --load-session fence_case.json

# Use a different model or temperature
python mediator_bot.py --model grok-beta --temperature 0.5 --max-tokens 800

# Override base URL (useful for proxies or future endpoints)
python mediator_bot.py --base-url https://api.x.ai/v1

```

## 🎮 In-Chat Commands

While the bot is running, you can type these commands instead of a message:

| Command | Description |
| --- | --- |
| `/undo` | Removes the last message (and the bot's response) so you can rephrase. |
| `/save` | Manually triggers a save to the session file. |
| `/quit` | Exits the application (saves automatically if `--save-session` is active). |
| `exit` | Same as `/quit`. |

## ⚙️ All Command-Line Options

| Option | Description | Default |
| --- | --- | --- |
| `--model` | Model name | `grok-beta` |
| `--base-url` | API base URL | `https://api.x.ai/v1` |
| `--api-key` | API key (not recommended; use env var instead) | `None` |
| `--topic` | Dispute topic (skips interactive prompt) | `None` |
| `--save-session` | JSON file to save session on exit | `None` |
| `--load-session` | JSON file to load previous conversation | `None` |
| `--max-tokens` | Maximum tokens per response | `1000` |
| `--temperature` | Sampling temperature (0.0–1.0) | `0.7` |

## 💾 Session File Format (JSON)

The saved JSON is a simple list of OpenAI-compatible message objects. You can edit, version-control, or feed these files into other tools.

```json
[
  {"role": "system", "content": "..."},
  {"role": "user", "content": "Dispute topic: Neighbor fence encroachment"},
  {"role": "user", "content": "Party A: He built 3 inches over the line."},
  {"role": "assistant", "content": "Mediator: I understand. Party B, how do you respond?"}
]

```

## ⚠️ Important Disclaimers

* **Not Legal Advice:** This tool is **not** a licensed attorney or certified mediator.
* **Informational Only:** All suggestions are informational only and based on general patterns in data.
* **Consult Professionals:** Always recommend parties consult qualified legal professionals for binding advice.

## 📄 License

**MIT License (Open Source Use Only)** Feel free to modify, extend, or integrate into open-source projects.

**Commercial Restriction:** For commercial use, contact the developer at **tonyelias2012@gmail.com** for further discussions.

> **Note:** Failure to receive exclusive permission from the developer for commercial use of this bot will result in legal action being taken.

Enjoy mediating!
