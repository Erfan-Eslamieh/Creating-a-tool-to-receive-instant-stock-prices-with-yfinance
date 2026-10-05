# 📈 Stock Price Tool with LangChain & yfinance

## 📖 Overview
This repository demonstrates how to create a **custom tool for retrieving real-time stock prices** using the LangChain framework integrated with yfinance. The project showcases how to build an **AI agent** that can fetch current stock prices and provide intelligent responses about financial data.

The project highlights:
- Creating custom tools with LangChain
- Integration with yfinance for real-time stock data
- Building AI agents with tool-calling capabilities
- Implementing Zero-Shot ReAct agents for financial queries

---

## 🧠 **Features**
- Real-time stock price retrieval using yfinance
- Custom LangChain tool creation
- AI agent with reasoning capabilities
- Support for any stock ticker symbol
- Verbose logging to understand agent decision-making
- Integration with OpenAI GPT models

---

## 📁 **File Structure**
- `Tools.ipynb` → Main notebook including:
  - Library installation and setup
  - Custom stock price function implementation
  - LangChain tool conversion
  - AI agent creation and configuration
  - Testing with real stock queries (AAPL, GOOGL)

---

## 🚀 **How to Use**

### 1. Clone the repository:
```bash
git clone https://github.com/your-username/stock-price-tool.git
```

### 2. Navigate to the folder:
```bash
cd stock-price-tool
```

### 3. Install required dependencies:
```bash
pip install yfinance langchain langchain-openai
```

### 4. Set up OpenAI API Key:
- Get your API key from OpenAI
- Add it to your Google Colab secrets or environment variables
- The notebook uses `userdata.get('Openai_api_key')` for secure access

### 5. Run the notebook:
```bash
jupyter notebook Tools.ipynb
```

---

## 📚 **Workflow Overview**

### ✅ **Step 1: Library Installation**
- Install yfinance for stock data retrieval
- Install langchain and langchain-openai for AI agent functionality

### ✅ **Step 2: Function Creation**
```python
def get_stock_price(ticker: str) -> str:
    data = yf.Ticker(ticker).history(period="1d")
    price = data["Close"].iloc[-1]
    return f"The current price of {ticker.upper()} is ${price:.2f}"
```

### ✅ **Step 3: Tool Conversion**
- Convert Python function to LangChain Tool
- Define tool name, function, and description
- Create tools list for agent initialization

### ✅ **Step 4: Agent Creation**
- Initialize ChatOpenAI LLM with GPT-4o-mini
- Create Zero-Shot ReAct agent with verbose logging
- Configure agent with custom tools

### ✅ **Step 5: Testing & Usage**
- Test agent with real stock queries
- Observe reasoning process through verbose output
- Get accurate, real-time stock price information

---

## 🔧 **Code Structure**

### **Core Function:**
```python
import yfinance as yf
from langchain.tools import Tool

def get_stock_price(ticker: str) -> str:
    data = yf.Ticker(ticker).history(period="1d")
    price = data["Close"].iloc[-1]
    return f"The current price of {ticker.upper()} is ${price:.2f}"
```

### **Tool Definition:**
```python
get_stock_price_tool = Tool(
    name="get_stock_price",
    func=get_stock_price,
    description="Get the current stock price for a given ticker symbol (e.g., AAPL, GOOGL)."
)
```

### **Agent Setup:**
```python
from langchain.agents import initialize_agent, AgentType
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini", temperature=0)
agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

---

## 📊 **Example Usage**

### Query Example:
```python
response = agent.run("What is the current price of AAPL stock?")
```

### Expected Output:
```
> Entering new AgentExecutor chain...
I need to find the current stock price for AAPL. 
Action: get_stock_price
Action Input: "AAPL"
Observation: The current price of AAPL is $226.01
Thought: I now know the final answer.
Final Answer: The current price of AAPL stock is $226.01.
> Finished chain.
```

---

## ✨ **Key Features & Benefits**

- ✔ **Real-time Data**: Get up-to-date stock prices from Yahoo Finance
- ✔ **AI Integration**: Combine financial data with AI reasoning
- ✔ **Custom Tools**: Learn how to create custom LangChain tools
- ✔ **Agent Reasoning**: Observe AI decision-making process
- ✔ **Scalable Design**: Easily extend with additional financial tools
- ✔ **Production Ready**: Clean, well-structured code for deployment

---

## 🛠 **Prerequisites**

- Python 3.7+
- OpenAI API key
- Internet connection for real-time stock data
- Basic understanding of Python and AI concepts

---

## 📈 **Supported Stock Markets**

The tool supports any ticker symbol available on Yahoo Finance, including:
- **US Markets**: AAPL, GOOGL, MSFT, TSLA, etc.
- **International Markets**: Various global exchanges
- **Indices**: ^GSPC (S&P 500), ^DJI (Dow Jones), etc.
- **Cryptocurrencies**: BTC-USD, ETH-USD, etc.

---

## 🔮 **Future Enhancements**

- [ ] Add historical price analysis
- [ ] Implement price alerts and notifications
- [ ] Add technical indicators (RSI, MACD, etc.)
- [ ] Support for options and derivatives data
- [ ] Integration with additional financial data sources
- [ ] Portfolio tracking and analysis features

---

## ⚠️ **Disclaimer**

This tool is for educational and informational purposes only. Stock prices are retrieved from Yahoo Finance and may have delays. Always verify financial information from official sources before making investment decisions. The authors are not responsible for any financial losses incurred through the use of this tool.

---

## 👨‍💻 **Author**

**Erfan Eslamieh**

M.Sc. in Cognitive Science – Specializing in Generative AI, Machine Learning, and Deep Learning  
📧 [erfan.cognitive.work@gmail.com]   
🔗 [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/erfan-eslamieh) [![Kaggle](https://img.shields.io/badge/Kaggle-20BEFF?style=flat&logo=kaggle&logoColor=white)](https://www.kaggle.com/erfaneslamieh)

