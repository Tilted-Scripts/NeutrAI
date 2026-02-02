⚖️ AI Legal Mediator CLI (Web-Enabled)A professional, interactive command-line tool that uses xAI's Grok (via the OpenAI-compatible API) to act as an impartial legal mediator.Unlike standard chatbots, this active agent is capable of Real-Time Web Search. When specific statutes, case law, or local jurisdiction rules are mentioned, the bot pauses to verify current information before responding—bridging the gap between general legal principles and specific local reality.✨ Key Features🕵️ Active Research Agent: Equipped with "Tool Use" capabilities. If a user asks about "Florida 2025 Alimony Reform," the bot will search the web via DuckDuckGo to provide up-to-date answers rather than relying on stale training data.💻 Rich Terminal UI: Uses the rich library for beautiful output, including loading spinners during research phases and rendered Markdown for legal text.💾 Robust Session Management: Save your mediation to a JSON file, auto-save progress, and resume later.↩️ In-Chat Commands: Use /undo to revert mistakes (smartly handles complex search-and-response chains) and /save to snapshot the conversation.🛡️ Network Resilience: Built-in retry logic (via tenacity) handles API timeouts or connectivity glitches.🛠️ RequirementsPython 3.8 or higherAn API Key from xAI ConsoleInstall dependencies:Bashpip install openai tenacity rich duckduckgo-search
🚀 Quick StartGet your xAI API key → https://console.x.aiSet the key (recommended)Linux/macOS:Bashexport XAI_API_KEY="sk-..."
Windows (PowerShell):PowerShell$env:XAI_API_KEY="sk-..."
Run the mediatorBashpython mediator_bot.py
You will be prompted for the dispute topic. Try a specific legal question to test the search, e.g., "What is the statute of limitations for debt in Texas?"📖 Usage ExamplesBash# Basic interactive session (Web Search enabled by default)
python mediator_bot.py

# Start with a specific dispute and auto-save when finished
python mediator_bot.py --topic "Contractor abandoned job site" --save-session construction_dispute.json

# Resume a previous session
python mediator_bot.py --load-session construction_dispute.json

# Use a different model or lower temperature for stricter adherence to facts
python mediator_bot.py --model grok-beta --temperature 0.3
🎮 In-Chat CommandsWhile the bot is running, you can type these commands instead of a message:CommandDescription/undoSmart undo. Removes the last user message, the bot's response, and any background search tool calls associated with that turn./saveManually triggers a save to the session file./quitExits the application (saves automatically if --save-session is active).exitSame as /quit.⚙️ All Command-Line OptionsOptionDescriptionDefault--modelModel name (must support Tool Use)grok-beta--base-urlAPI base URLhttps://api.x.ai/v1--api-keyAPI key (not recommended; use env var instead)None--topicDispute topic (skips interactive prompt)None--save-sessionJSON file to save session on exitNone--load-sessionJSON file to load previous conversationNone--max-tokensMaximum tokens per response1000--temperatureSampling temperature (0.0–1.0)0.5💾 Session File Format (JSON)The session file now includes "Tool" messages, preserving the research history so the bot remembers what it searched for when you reload the session.JSON[
  {"role": "user", "content": "What is the small claims limit in CA?"},
  {"role": "assistant", "tool_calls": [...]},
  {"role": "tool", "content": "- California Courts: The limit is $12,500 for individuals..."},
  {"role": "assistant", "content": "Mediator: As of 2024, the limit for an individual is $12,500..."}
]
⚠️ Important DisclaimersNot Legal Advice: This tool is not a licensed attorney or certified mediator.Search Limitations: While the bot uses web search to find current information, it may still encounter outdated sources or misinterpret search results.Consult Professionals: Always recommend parties consult qualified legal professionals for binding advice.📄 LicenseMIT License (Open Source Use Only)Feel free to modify, extend, or integrate into open-source projects.Commercial Restriction:For commercial use, contact the developer at tonyelias2012@gmail.com for further discussions.Note: Failure to receive exclusive permission from the developer for commercial use of this bot will result in legal action being taken.Enjoy mediating!
