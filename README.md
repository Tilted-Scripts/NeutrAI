# Legal Mediator Bot – README  
`mediator_bot.py`

A robust, plug-and-play AI-powered legal mediator that uses **xAI’s Grok models** via the OpenAI-compatible API.

Perfect for quick testing, demos, dispute-resolution prototypes, or integration into larger ADR platforms.

### Features
- One-file, zero-config start (just set your API key)
- CLI arguments for model, topic, temperature, session save/load
- Automatic retry with exponential backoff (`tenacity`)
- Session persistence to JSON (continue conversations later)
- Proper logging and graceful error handling
- Works with `grok-4`, `grok-3` or any future xAI model

### Requirements
```bash
pip install openai tenacity
```

### Quick Start

1. **Get your xAI API key**  
   → https://console.x.ai

2. **Set the key (recommended)**
   ```bash
   export XAI_API_KEY="sk-..."
   ```

3. **Run the mediator**
   ```bash
   python mediator_bot.py
   ```

   You’ll be prompted for the dispute topic, then alternate between **Party A** and **Party B**.

### Common Usage Examples

```bash
# Basic interactive session
python mediator_bot.py

# Start with a specific dispute and auto-save when finished
python mediator_bot.py --topic "Neighbor fence encroachment dispute" --save-session fence_case.json

# Resume a previous session
python mediator_bot.py --load-session fence_case.json

# Use a different model or temperature
python mediator_bot.py --model grok-4 --temperature 0.5 --max-tokens 800

# Override base URL (useful for proxies or future endpoints)
python mediator_bot.py --base-url https://api.x.ai/v1
```

### All Command-Line Options

| Option              | Description                                      | Default          |
|---------------------|--------------------------------------------------|------------------|
| `--model`           | Model name                                       | `grok-4`         |
| `--base-url`        | API base URL                                     | `https://api.x.ai/v1` |
| `--api-key`         | API key (not recommended; use env var instead)   | `None`           |
| `--topic`           | Dispute topic (skips interactive prompt)         | `None`           |
| `--save-session`    | JSON file to save session on exit                | `None`           |
| `--load-session`    | JSON file to load previous conversation          | `None`           |
| `--max-tokens`      | Maximum tokens per response                      | `500`            |
| `--temperature`     | Sampling temperature (0.0–1.0)                    | `0.7`            |

### Session File Format (JSON)
The saved JSON is a simple list of OpenAI-compatible message objects, e.g.:

```json
[
  {"role": "system", "content": "..."},
  {"role": "user", "content": "Dispute topic: ..."},
  {"role": "user", "content": "Party A: ..."},
  {"role": "assistant", "content": "Mediator: ..."}
]
```

You can edit, version-control, or feed these files into other tools.

### Important Disclaimers
- This tool is **not** a licensed attorney or certified mediator.
- All suggestions are informational only.
- Always recommend parties consult qualified legal professionals for binding advice.

### License
MIT – feel free to modify, extend, or integrate into commercial or open-source projects.

Enjoy mediating!
