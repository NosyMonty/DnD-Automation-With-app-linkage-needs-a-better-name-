  vvd.world AI Agent — README
  Built by NosyMonty
================================================================

WHAT IS THIS?
-------------
This is a locally running AI agent that controls your vvd.world
account automatically. You type what you want in plain English
and it opens a browser, logs in, and does it for you.

It can create cards, build maps, manage your wiki, answer D&D
questions, and generate new lore inspired by your campaign files.
Everything runs on your own computer — no cloud, no subscription.


WHAT YOU NEED
-------------
  - Windows 11
  - Python 3.11 or higher
  - Ollama (IPEX-LLM build for Intel GPU acceleration)
  - Intel Core Ultra processor (tested on Ultra 7 165H)
  - vvd.world account

HOW TO INSTALL
--------------
1. Download and install Ollama
2. Go to https://github.com/ipex-llm/ipex-llm/releases/tag/v2.2.0 and install the llama-cpp-ipex-llm-2.2.0-win.zip github file
3. Download all files
    -unzip if zipped
4. Open PowerShell and type cd "your file location here"
5. Activate a virtual environment
    - .venv/scripts/activate
  6. type pip install requirements.txt
  7. Wait for it to finish installing
  8. Update the .env.exaple file with your Ollama model and login credentials for vvw.worlds
  9. build ai agnet by typing the following in the same PowerShell tab as before
        - ollama.exe create vvd-agent -f "file location"

HOW TO START
------------
1. Double-click start_agent.bat

   This will automatically:
   - Kill any existing Ollama processes
   - Start Ollama with Intel Arc GPU acceleration
   - Activate the Python environment
   - Launch the agent and open a browser

2. The agent will log into vvd.world and ask which world
   You want to work in.

3. Type what you want, and the agent will do it!


WHAT YOU CAN SAY
----------------
CARDS
  "Create a character card for [name]"
  "Make a location called [name]"
  "Add a faction card for [name]"
  "edit [card name] description to [new description]"
  "Delete the card for [name]"
  "link [card a] and [card b] as [relationship]"

MAPS
  "Create a map called [name]"
  "add a pin for [place] on the [map] map"

WORLDS
  "Create a new world called [name]"
  "switch to world [name]"
  "Show me the relationship graph"

WIKI & NOTES
  "set the wiki title to [title]"
  "Create a session note called [title]"

KNOWLEDGE
  "Remember that [lore fact]"
  "What do you know about my campaign?"
  "Suggest what I should create next"

D&D QUESTIONS (searches the web)
  "How does the silence spell work?"
  "What monsters live in the Underdark?"
  "What are the rules for grappling?"

SPECIAL COMMANDS
  "help"        — show this list
  "card debug"  — test card creation without AI
  "wipe memory" — clear all stored memory
  "quit"        — exit the agent


FILES IN THIS FOLDER
--------------------
  agent.py          Main agent script
  start_agent.bat   One-click launcher (use this to start)
  Modelfile         Instructions for building the AI model
  .env              Your login credentials (keep this private!)
  memory.json       Auto-created — stores action history and knowledge
  knowledge/        Folder for your campaign notes
    lore.MD         Your campaign lore or the premade campaign lore included on the download


KNOWLEDGE FOLDER
----------------
Drop any .txt or .md files into the knowledge/ folder and the
The agent will automatically read them and use them when creating
cards and answering questions.

For example, paste your campaign notes into:
  knowledge/lore.md 
or use the pre-made one in the included 
    knowledge/lore.md

The agent uses this to write rich, lore-accurate descriptions
when creating new cards.


AI MODELS USED
--------------
  vvd-agent   Main model (llama3.1:8b with vvd knowledge baked in)
  llava        Vision model — used as a fallback to see the screen


HARDWARE
--------
  CPU:  Intel Core Ultra 7 165H
  GPU:  Intel Arc iGPU (128 EU)
  RAM:  16GB
  OS:   Windows 11

  Ollama runs via the IPEX-LLM build, which uses the Intel Arc
  GPU for acceleration (~139 tokens/second vs ~13 on CPU).


TROUBLESHOOTING
---------------
The agent won't start?
  - Make sure Ollama is not already running in the system tray
  - Run start_agent.bat as Administrator
  - Check your .env file has the correct email and password

The browser opens, but nothing happens.
  - Try typing "card debug" to test browser automation
  - Check the terminal for error messages

Model not found error?
  - Run: cd C:\ipex-ollama
  - Run: ollama.exe create vvd-agent -f "File Location"

Slow responses?
  - Make sure start_agent.bat was used (not python agent.py directly)
  - Check Task Manager GPU tab — should show activity when thinking

Web search not working?
  - Check TAVILY_API_KEY is set in your .env file
  - Sign up for free at https://app.tavily.com


UPDATING THE MODEL
------------------
If vvd.world releases new features, update the Modelfile then:

  cd C:\ipex-ollama
  ollama.exe rm vvd-agent
  ollama.exe create vvd-agent -f "File Location"


PRIVACY
-------
  - Everything runs locally on your machine
  - Your credentials are stored only in .env on your computer
  - Campaign data never leaves your machine
  - vvd.world itself has a zero AI training policy


  Questions or issues? Check the terminal output for clues, or make an issue request
=====================================================================================
