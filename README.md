# LangGraph RAG Agent with Web Search

A powerful Retrieval-Augmented Generation (RAG) application built with LangGraph, Streamlit, and advanced AI technologies. This application can answer questions about malaria and health-related topics using both local PDF knowledge base and real-time web search capabilities.

## 🚀 Features

- **Intelligent Routing**: Automatically decides whether to use local knowledge base or web search
- **PDF Knowledge Base**: Processes and searches through local PDF documents
- **Real-time Web Search**: Searches WHO and other health websites for latest information
- **Interactive Chat Interface**: User-friendly Streamlit web interface
- **Vector Database**: Efficient semantic search using Chroma DB
- **Advanced AI Models**: Powered by Groq's fast language models

## 📋 Prerequisites

- Python 3.11 or higher
- Windows 10/11 (PowerShell)
- Internet connection for API access
- Free API keys from Groq and Tavily

## 🛠️ Installation

### 1. Clone Repository
```powershell
git clone https://github.com/vinothezhumalai1987-ind/langgraph.git
cd langgraph
```

### 2. Virtual Environment Setup
```powershell
# Navigate to src directory
cd src

# Activate virtual environment (Windows)
.\.venv\Scripts\Activate.ps1

# If you get execution policy errors, run:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 3. Install Dependencies
```powershell
# From the project root directory
uv sync --directory "src"
```

### 4. Get API Keys
1. **Groq API Key** (Free): 
   - Visit: https://console.groq.com/keys
   - Sign up and get your API key starting with `gsk_`

2. **Tavily API Key** (Free):
   - Visit: https://app.tavily.com/sign-up
   - Sign up and get your API key starting with `tvly-`

### 5. Configure Environment
Edit `src/.env` file:
```env
GROQ_API_KEY=gsk_your_actual_groq_api_key_here
TAVILY_API_KEY=tvly-your_actual_tavily_api_key_here
USER_AGENT=LangGraph-RAG-Application/1.0
```

## 🏃‍♂️ Quick Start

### Running the Application
```powershell
# From project root directory
uv run --directory "src" streamlit run main.py
```

The application will be available at: http://localhost:8501

### Initial Setup
1. **Access the web interface** at http://localhost:8501
2. **Check sidebar** - you should see "Found 1 PDF(s) in knowledge base"
3. **Click "🔄 Ingest/Re-ingest PDFs"** to create the vector database
4. **Start asking questions** about malaria or health topics!

## 📚 Usage

### Example Questions
- "What are the symptoms of malaria?"
- "How is malaria transmitted?"
- "What are the latest WHO guidelines for malaria prevention?"
- "Tell me about malaria treatment options"

### How It Works
1. **Question Analysis**: The router analyzes your question
2. **Source Selection**: Automatically chooses between local PDFs or web search
3. **Information Retrieval**: Fetches relevant information from selected source
4. **Response Generation**: Uses AI to provide comprehensive answers

## 🗂️ Project Structure

```
langgraph/
├── src/
│   ├── main.py              # Main Streamlit application
│   ├── .env                 # Environment variables (create this)
│   ├── knowledge-base/      # PDF documents directory
│   │   └── malaria_report.pdf
│   ├── chroma_db/          # Vector database (auto-created)
│   ├── .venv/              # Virtual environment
│   └── pyproject.toml      # Project dependencies
├── README.md               # This file
├── TROUBLESHOOTING.md      # Troubleshooting guide
└── SETUP_GUIDE.md         # Detailed setup instructions
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙋‍♂️ Support

For issues and questions:
1. Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. Review [SETUP_GUIDE.md](SETUP_GUIDE.md)
3. Create an issue on GitHub

## 🔗 Links

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [Groq API](https://console.groq.com/)
- [Tavily Search API](https://app.tavily.com/)