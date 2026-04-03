# 📖 Complete Setup Guide

Step-by-step instructions for setting up the LangGraph RAG Application from scratch.

## 📋 Table of Contents
1. [Prerequisites](#prerequisites)
2. [System Requirements](#system-requirements)
3. [Installation Steps](#installation-steps)
4. [Configuration](#configuration)
5. [First Run](#first-run)
6. [Verification](#verification)
7. [Next Steps](#next-steps)

## 🔧 Prerequisites

### Software Requirements
- **Windows 10/11** with PowerShell
- **Python 3.11 or higher**
- **Git** (for cloning repository)
- **Internet connection** (for downloading dependencies and API access)

### Account Requirements
- **Groq Account** (free) - for AI language model
- **Tavily Account** (free) - for web search functionality

## 💻 System Requirements

### Minimum Requirements
- **RAM**: 4GB (8GB recommended)
- **Storage**: 2GB free space
- **CPU**: Any modern processor
- **Network**: Broadband internet connection

### Recommended Specifications
- **RAM**: 8GB or more
- **Storage**: SSD with 5GB+ free space
- **CPU**: Multi-core processor
- **Network**: Stable internet connection

## 🚀 Installation Steps

### Step 1: Clone Repository
```powershell
# Open PowerShell and navigate to desired location
cd Desktop

# Clone the repository
git clone https://github.com/vinothezhumalai1987-ind/langgraph.git

# Navigate to project directory
cd langgraph
```

### Step 2: Check Project Structure
```powershell
# Verify project structure
ls

# You should see:
# - src/          (main application code)
# - colab-notebooks/
# - studio/
# - .gitignore
```

### Step 3: Virtual Environment Setup

#### Option A: Using Existing Virtual Environment
```powershell
# Navigate to src directory
cd src

# Check if virtual environment exists
ls .venv

# Activate virtual environment
.\.venv\Scripts\Activate.ps1
```

#### Option B: Create New Virtual Environment
```powershell
# Navigate to src directory
cd src

# Create virtual environment
python -m venv .venv

# Activate virtual environment
.\.venv\Scripts\Activate.ps1
```

#### Handling Execution Policy Errors
```powershell
# If you get execution policy error, run:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Then try activation again
.\.venv\Scripts\Activate.ps1
```

### Step 4: Install Dependencies

#### Method 1: Using UV (Recommended)
```powershell
# From project root directory (not src)
cd .. # Go back to project root if in src

# Install dependencies
uv sync --directory "src"

# If timeout issues occur:
$env:UV_HTTP_TIMEOUT="120"; uv sync --directory "src"
```

#### Method 2: Using Pip (Alternative)
```powershell
# Navigate to src directory
cd src

# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt
```

### Step 5: Verify Installation
```powershell
# Check Python version
python --version
# Should show Python 3.11.x

# Check LangGraph installation
python -c "import langgraph; print('LangGraph installed successfully')"

# Check Streamlit installation
python -c "import streamlit; print('Streamlit installed successfully')"

# List key packages
uv pip list | findstr -i "langgraph streamlit groq tavily"
```

## ⚙️ Configuration

### Step 1: Get API Keys

#### Groq API Key
1. **Visit**: https://console.groq.com/keys
2. **Sign up** for a free account
3. **Create API key** (starts with `gsk_`)
4. **Copy the key** (save it somewhere safe)

#### Tavily API Key
1. **Visit**: https://app.tavily.com/sign-up
2. **Sign up** for a free account
3. **Get API key** from dashboard (starts with `tvly-`)
4. **Copy the key** (save it somewhere safe)

### Step 2: Configure Environment Variables
```powershell
# Navigate to src directory
cd src

# Check if .env file exists
ls .env
```

#### Create/Edit .env File
Create or edit `src/.env` with the following content:
```env
# LangGraph RAG Application Environment Variables

# API Keys for LLM and Web Search functionality
GROQ_API_KEY=gsk_your_actual_groq_api_key_here
TAVILY_API_KEY=tvly-your_actual_tavily_api_key_here

# Optional: Set other environment variables
USER_AGENT=LangGraph-RAG-Application/1.0
```

**Important**: Replace the placeholder values with your actual API keys!

### Step 3: Verify Knowledge Base
```powershell
# Check knowledge base directory
ls knowledge-base/

# Should contain:
# - malaria_report.pdf (or other PDF files)
```

## 🏃‍♂️ First Run

### Step 1: Start Application
```powershell
# From project root directory
uv run --directory "src" streamlit run main.py

# Alternative if in src directory:
cd src
uv run streamlit run main.py
```

### Step 2: Access Web Interface
1. **Open browser** and go to: http://localhost:8501
2. **Wait for page to load** (may take 30-60 seconds first time)
3. **Check sidebar** for application status

### Step 3: Initialize Database
1. **Check Knowledge Base section** in sidebar
2. **Should show**: "Found X PDF(s) in knowledge base"
3. **Click**: "🔄 Ingest/Re-ingest PDFs" button
4. **Wait for completion** (may take 2-3 minutes)
5. **Success message**: "✅ Ingested X documents!"

## ✅ Verification

### Application Health Check
- ✅ **Terminal shows**: "You can now view your Streamlit app..."
- ✅ **Browser loads**: http://localhost:8501 successfully
- ✅ **Sidebar displays**: "Found X PDF(s) in knowledge base"
- ✅ **Database status**: "Vector database exists"
- ✅ **No error messages** in terminal or browser

### Test Functionality
1. **Ask a test question**: "What are the symptoms of malaria?"
2. **Check response time**: Should respond within 10-30 seconds
3. **Verify sources**: Should show source information
4. **Test web search**: Ask about "latest WHO malaria guidelines"

### Common Success Indicators
```
✅ Virtual environment activated (prefix in terminal)
✅ All dependencies installed (190+ packages)
✅ Streamlit running on port 8501
✅ Knowledge base PDFs detected
✅ Vector database created successfully
✅ API keys configured and working
✅ Chat interface responding to questions
```

## 🎯 Next Steps

### Customize Your Application
1. **Add more PDFs** to `src/knowledge-base/` directory
2. **Re-ingest PDFs** after adding new documents
3. **Test different types** of health-related questions
4. **Explore web search** functionality

### Advanced Configuration
1. **Modify AI model**: Edit `LLM_MODEL_ID` in `main.py`
2. **Adjust chunk size**: Modify `CHUNK_SIZE` and `CHUNK_OVERLAP`
3. **Customize prompts**: Edit routing and generation prompts
4. **Add new domains**: Update Tavily search domains

### Maintenance
1. **Regular updates**: Run `uv sync` to update dependencies
2. **Monitor usage**: Check API key usage limits
3. **Backup database**: Save `chroma_db/` directory
4. **Update documentation**: Keep README current

## 🆘 If Something Goes Wrong

1. **Check**: [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. **Verify**: All steps in this guide completed
3. **Reset**: Follow complete reset instructions
4. **Ask**: Create issue on GitHub with details

## 🎉 Congratulations!

You have successfully set up the LangGraph RAG Application! You can now:
- Ask questions about malaria and health topics
- Get answers from both local PDFs and web search
- Experience intelligent routing between information sources
- Use a modern AI-powered knowledge assistant

**Happy exploring! 🚀**

---

## 📞 Support

- **Documentation**: [README.md](README.md)
- **Troubleshooting**: [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- **Issues**: GitHub Issues
- **Updates**: Check repository for latest changes