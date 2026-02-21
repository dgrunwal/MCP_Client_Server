Simple MCP Client and Server Tested on Python 3.13

In a virtual environment if possible:
1.	Install the necessary libraries:
pip install mcp openai 
2.	Set your OPENAI key:
set OPENAI_API_KEY=<enter key with no spaces> 
A key with spaces returns the following error:

You can find your API key at <API key URL>.', 'type': 'invalid_request_error', 'code': 'invalid_api_key', 'param': None}, 'status': 401}
Note: Confirm API key has no spaces by running 

echo "%OPENAI_API_KEY%"

3.	Run python mcp_client.py
Note: Both files need to be in the same folder, then just run mcp_client.py — it automatically starts mcp_server.py as a subprocess.

Program performs the following:

1.	The client launches the server as a subprocess over stdio
2.	It calls list_tools() to discover the server's 3 tools and converts them to OpenAI's format
3.	You type a message — it goes to GPT-4o along with the tool definitions
4.	If OpenAI decides a tool is needed (e.g. "what's 42 + 58?"), it returns a tool call request
5.	The client executes that tool on the MCP server and feeds the result back to OpenAI
6.	OpenAI gives a final natural language answer

C:\python3_13>python mcp_client.py
=== Available MCP Tools ===
  • add: Add two numbers together and return the result.
  • greet: Return a friendly greeting for a given name.
  • get_time: Return the current date and time.

Chat with OpenAI + MCP tools. Type 'quit' to exit.

You: What is 2 plus 2?
  [Calling tool: add({'a': 2, 'b': 2})]
  [Tool result: 4]

Assistant: 2 plus 2 equals 4.

Try prompts like:
•	"What is 123 plus 456?" → triggers add
•	"Say hello to Sarah" → triggers greet
•	"What time is it?" → triggers get_time

Now that you have a working MCP client server program, add your own features:

Beginner additions
•	subtract, multiply, divide tools to make a full calculator
•	get_weather tool (using a free API like Open-Meteo, no key needed)
•	reverse_string or word_count tool to show string manipulation
•	Conversation history saving to a .txt or .json file

Intermediate additions
•	read_file / write_file tools so the AI can read and write local files
•	web_search tool using DuckDuckGo's free API
•	run_python tool that executes a snippet of code and returns the output
•	A memory tool that lets the AI store and recall facts across the session
•	Switch between models (GPT-4o vs GPT-4o-mini) based on question complexity

More advanced additions
•	query_database tool backed by a local SQLite database
•	Multi-server support — connect to 2 or more MCP servers at once and combine their tools
•	A simple web UI using Flask or Streamlit instead of the command-line chat loop
•	Streaming responses so the assistant's reply prints word-by-word rather than all at once
•	Tool call logging — write every tool call and result to a structured log file for debugging
Educational/demo focused
•	A --list mode that just prints all available tools and exits, great for teaching tool discovery
•	Verbose mode (--verbose) that pretty-prints the full JSON sent to and from OpenAI, so learners can see exactly what's happening under the hood
•	A mock mode that returns fake tool results without starting a real server, useful for testing the client in isolation


