# Data Analyst Agent

An autonomous data analysis agent that leverages Google Gemini models to perform scraping, data processing, and visualization. This agent can process both uploaded datasets (CSV, Excel, Parquet, JSON, Images) and live web data.

## Features

- **Robust LLM Fallback**: Implements a custom `LLMWithFallback` class that rotates through up to 10 Gemini API keys and multiple model versions (`gemini-2.5-pro`, `flash`, etc.) to handle rate limits and quotas.
- **Autonomous Agent**: Uses LangChain's tool-calling agent to decide when to scrape data or process existing dataframes.
- **Sandboxed Execution**: Generates Python code dynamically and executes it in a controlled temporary environment to generate answers and visualizations.
- **Multi-Format Scraper**: Automatically detects and parses CSV, Excel, Parquet, JSON, and HTML tables from provided URLs.
- **Image Processing**: Capable of handling image uploads using PIL.
- **System Diagnostics**: Built-in `/summary` endpoint to monitor network health, API key validity, and system resources.
- **Optimized Visualizations**: Includes a `plot_to_base64` helper that ensures generated charts are optimized and compressed (under 100KB) for API responses.

##  Technology Stack

- **Backend**: FastAPI, Uvicorn
- **LLM Framework**: LangChain, Google Generative AI
- **Data Analysis**: Pandas, NumPy, Matplotlib, Seaborn, NetworkX
- **Diagnostics**: Psutil, HTTPX

##  Prerequisites

- Python 3.9+
- Google AI (Gemini) API Keys

## 🔧 Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Shi-pra-19/agent.git
   cd agent
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Environment Variables:**
   Create a `.env` file in the root directory and add your Gemini API keys:
   ```env
   gemini_api_1=your_api_key_1
   gemini_api_2=your_api_key_2
   # Supports up to gemini_api_10
   GOOGLE_MODEL=gemini-2.5-pro
   PORT=8000
   ```

##  Usage

### Starting the Server
```bash
python app.py
```
The server will start at `http://0.0.0.0:8000`.

### API Endpoints

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/` | `GET` | Serves the web frontend (`index.html`). |
| `/api` | `POST` | The primary analysis endpoint. Accepts `questions_file` (.txt) and an optional `data_file`. |
| `/summary` | `GET` | Returns system diagnostics and LLM health checks. |


### Analysis Request Example
To use the API, send a `multipart/form-data` request:
- `questions_file`: A `.txt` file containing natural language questions.
- `data_file`: (Optional) A CSV, XLSX, or image file for analysis.




## 📄 License
[Insert License Type - e.g., MIT]
