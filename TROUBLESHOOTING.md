# 🔧 Troubleshooting Guide

Common issues and solutions for the LangGraph RAG Application.

## 🚨 Common Issues

### 1. Virtual Environment Issues

#### Problem: `source` command not recognized
```
source : The term 'source' is not recognized...
```
**Solution:**
```powershell
# Windows uses different activation command
.\.venv\Scripts\Activate.ps1

# If execution policy error:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### Problem: Virtual environment not found
**Solution:**
```powershell
# Make sure you're in the src directory
cd src
ls .venv  # Should show Scripts/ and Lib/ directories
```

### 2. Dependency Installation Issues

#### Problem: Network timeout with `safetensors`
```
Failed to download `safetensors==0.6.2`
```
**Solutions:**
```powershell
# Option 1: Increase timeout
$env:UV_HTTP_TIMEOUT="120"; uv sync

# Option 2: Use directory flag
uv sync --directory "C:\path\to\your\project\src"

# Option 3: Retry installation
uv sync --refresh
```

#### Problem: UV command not found
**Solution:**
```powershell
# Install UV package manager
pip install uv

# Or use pip directly
pip install -r requirements.txt
```

### 3. Streamlit Application Issues

#### Problem: File does not exist: main.py
```
Error: Invalid value: File does not exist: main.py
```
**Solutions:**
```powershell
# Option 1: Run from correct directory
cd src
uv run streamlit run main.py

# Option 2: Use full path (recommended)
uv run --directory "src" streamlit run main.py

# Option 3: Check file exists
ls src/main.py  # Should show the file
```

#### Problem: Knowledge base directory not found
**Solution:**
```powershell
# Check directory structure
ls src/knowledge-base/  # Should show PDF files

# Run from correct directory
cd src
uv run streamlit run main.py
```

### 4. API Key Issues

#### Problem: Invalid API Key error (401)
```
Error code: 401 - {'error': {'message': 'Invalid API Key'...}}
```
**Solutions:**
1. **Check .env file format:**
   ```env
   GROQ_API_KEY=gsk_your_key_here
   TAVILY_API_KEY=tvly-your_key_here
   ```

2. **Verify API keys are valid:**
   - Groq: https://console.groq.com/keys
   - Tavily: https://app.tavily.com/dashboard

3. **Restart application after updating keys**

#### Problem: API key not loaded
**Solutions:**
```powershell
# Check if .env file exists
ls src/.env

# Restart Streamlit
taskkill /f /im streamlit.exe
uv run --directory "src" streamlit run main.py
```

### 5. Database Issues

#### Problem: Vector database not found
**Solutions:**
1. **Run PDF ingestion:**
   - Click "🔄 Ingest/Re-ingest PDFs" in sidebar
   - Wait for completion message

2. **Check PDF files:**
   ```powershell
   ls src/knowledge-base/*.pdf
   ```

3. **Clear and recreate database:**
   ```powershell
   rm -rf src/chroma_db
   # Then run ingestion again
   ```

### 6. PowerShell Command Issues

#### Problem: `&&` not recognized
```
The token '&&' is not a valid statement separator
```
**Solution:**
```powershell
# Use separate commands or semicolon
cd src; uv run streamlit run main.py

# Or use full paths
uv run --directory "src" streamlit run main.py
```

#### Problem: Path with spaces
**Solution:**
```powershell
# Use quotes for paths with spaces
cd "C:\Users\Your Name\Desktop\langgraph\langgraph\src"
```

## 🔍 Diagnostic Commands

### Check Environment
```powershell
# Check Python version
python --version

# Check UV installation
uv --version

# Check current directory
pwd

# List files
ls
```

### Check Application Status
```powershell
# Check if Streamlit is running
netstat -an | findstr :8501

# Check running processes
tasklist | findstr streamlit

# Kill Streamlit if needed
taskkill /f /im streamlit.exe
```

### Verify Dependencies
```powershell
# Check installed packages
uv pip list | findstr langgraph

# Verify imports work
python -c "import langgraph; print('LangGraph OK')"
python -c "import streamlit; print('Streamlit OK')"
```

## 📞 Getting Help

### Before Reporting Issues
1. **Check this troubleshooting guide**
2. **Verify all prerequisites are met**
3. **Try running diagnostic commands**
4. **Check the application logs**

### Log Locations
- **Streamlit logs**: Check terminal output
- **Python errors**: Displayed in terminal
- **Browser console**: F12 → Console tab

### Reporting Issues
Include the following information:
- **Operating System**: Windows version
- **Python Version**: `python --version`
- **Error Message**: Complete error text
- **Steps to Reproduce**: What you were doing
- **Screenshots**: If helpful

## 🔄 Reset Instructions

### Complete Reset
```powershell
# 1. Stop application
taskkill /f /im streamlit.exe

# 2. Remove database
rm -rf src/chroma_db

# 3. Clear cache
rm -rf src/__pycache__

# 4. Reinstall dependencies
uv sync --refresh

# 5. Restart application
uv run --directory "src" streamlit run main.py
```

### Partial Reset
```powershell
# Just clear vector database
rm -rf src/chroma_db

# Restart and re-ingest PDFs
```

## ✅ Success Indicators

Your application is working correctly when:
- ✅ Terminal shows: `You can now view your Streamlit app in your browser`
- ✅ Browser loads at http://localhost:8501
- ✅ Sidebar shows: "Found X PDF(s) in knowledge base"
- ✅ No error messages in terminal
- ✅ Can ask questions and get responses

## 🚀 Performance Tips

1. **Keep PDFs small** (< 50MB total)
2. **Use SSD storage** for faster database access
3. **Close other applications** to free memory
4. **Use latest Python version** (3.11+)
5. **Restart application** if it becomes slow