<h1 align="center">🤖 LangGraph Research Assistant</h1>

<p align="center">
An AI-powered research assistant using <b>LangGraph</b>, <b>LangChain</b>, and <b>Ollama embeddings</b> to read PDFs, answer queries, and store long-term insights.
</p>

<hr>

<h2>⚙️ Features</h2>
<ul>
  <li>📄 PDF Loader: Upload and chunk multiple PDFs for session-based processing</li>
  <li>🧠 Query Analyzer: Extracts keywords and intent from user queries</li>
  <li>🔍 Information Retriever: Retrieves relevant chunks from session PDFs and long-term memory</li>
  <li>💬 Response Generator: Fuses conversation history + context to generate answers</li>
  <li>📚 Long-term Memory: Stores concise insights for future sessions using Chroma embeddings</li>
  <li>⏱️ Short-term Memory: Maintains session-based context for follow-up queries</li>
  <li>🛠️ Debug & Cleanup: Inspect state and safely remove session caches</li>
</ul>

<hr>

<h2>📂 File Structure</h2>
<pre>
langgraph-research-assistant/
├── langgraph_research_assistant.ipynb             (Install dependencies & configure Ollama)
├── requirements.txt        (Python dependencies)
└── README.md               
</pre>

<hr>

<h2>🚀 Setup Instructions</h2>

<ol>
  <li>Clone the repository</li>
  <pre><code>git clone https://github.com/your-username/langgraph-research-assistant.git
cd langgraph-research-assistant</code></pre>

  <li>Create a Python virtual environment & install dependencies</li>
  <pre><code>python -m venv venv
source venv/bin/activate   # Linux/Mac
venv\Scripts\activate      # Windows
pip install -r requirements.txt</code></pre>

  <li>Install system dependencies & Ollama</li>
  <pre><code>sudo apt-get install -y pciutils
curl -fsSL https://ollama.com/install.sh | sh
ollama pull all-minilm</code></pre>

  <li>Run the Ollama server</li>
  <pre><code>import subprocess, os
os.environ['OLLAMA_HOST'] = '0.0.0.0:11434'
os.environ['OLLAMA_ORIGINS'] = '*'
subprocess.Popen(["ollama", "serve"])</code></pre>

  <li>Set up OpenAI or custom LLM API</li>
  <pre><code>export GITHUB_TOKEN="your_github_token"
# or update directly inside 02_config.py</code></pre>

  <li>Run the agent with a session</li>
  <pre><code>python 07_run_example.py</code></pre>
</ol>

<hr>

<h2>💡 Example Usage</h2>

<p><b>Example 1: Initial PDF Query</b></p>
<pre><code>
from 07_run_example import research_app, initial_state

result = research_app.invoke(initial_state)
print(result["messages"][-1].content)
</code></pre>

<p>✅ Output:</p>
<ul>
  <li>Summarized insights from uploaded PDFs</li>
  <li>Relevant chunks retrieved from session and long-term memory</li>
</ul>

<p><b>Example 2: Follow-up Query</b></p>
<pre><code>
follow_up_state = {
    **result,
    "messages": result["messages"] + [HumanMessage(content="Explain the key findings in a short paragraph.")],
    "session_id": result["session_id"]
}
follow_up_result = research_app.invoke(follow_up_state)
print(follow_up_result["messages"][-1].content)
</code></pre>

<p>✅ Output:</p>
<ul>
  <li>Short-term memory ensures follow-up context is preserved</li>
  <li>New insights may also be stored in long-term memory</li>
</ul>

<hr>

<h2>🙌 Credits</h2>
<p>
Built with <b>LangGraph</b>, <b>LangChain</b>, <b>Ollama embeddings</b>, <b>ChromaDB</b>, and <b>Python</b>.
</p>

<p align="center">⭐ Star this repo if you find it useful!</p>
