# Multi-Agent Reasoning System

A production-grade **Cognitive Loop** system using LangGraph with three specialized agents that iteratively improve reasoning quality.

## Cognitive Loop Architecture

The system implements a complete cognitive cycle:

| 阶段 | 对应模块 | 技术实现 |
|------|---------|---------|
| 1. 接收信息 | Input Adapter | Question Input / State Initialization |
| 2. 记录信息 | Memory | LangGraph State / Reasoning History |
| 3. 理解推理 | Reasoning Core | **Reasoner Agent** (LLM-powered) |
| 4. 决策规划 | Controller | **Critic Agent** (Confidence-based routing) |
| 5. 执行动作 | Tool Layer | **Refiner Agent** (Answer synthesis) |
| 6. 反思学习 | Feedback Module | Multi-iteration loop with critique |

**Flow:** Input → Reasoner → Critic → (iterate if needed) → Refiner → Output

## Installation

```bash
git clone <repository-url>
cd agent_reasoning_system
pip install -r requirements.txt
export OPENAI_API_KEY='your-api-key-here'
```

## Usage

```python
from core import ReasoningGraph

graph = ReasoningGraph(max_iterations=3)
result = graph.reason("Your question here")

print(result["final_answer"])
print(f"Confidence: {result['confidence_score']}")
```

**Run Examples:**
```bash
# Interactive unified demo (recommended!)
python examples/unified_strategy_demo.py

# Individual examples
python examples/quant_strategy_reasoning.py      # LLM strategy reasoning
python examples/strategy_comparison/quick_start.py  # Traditional vs LLM comparison
```

## Result Structure

```python
{
    "final_answer": str,           # Synthesized answer
    "reasoning_history": list,     # Full conversation trace
    "confidence_score": float,     # 0.0-1.0 (0.9+ = high quality)
    "iterations": int              # Number of refinement loops
}
```

## Project Structure

```
agent_reasoning_system/
├── core/                          # Core reasoning engine
│   ├── state.py                  # Memory: State definitions
│   ├── agents.py                 # Reasoning: Agent implementations
│   └── graph.py                  # Controller: LangGraph workflow
├── examples/
│   ├── unified_strategy_demo.py  # 🌟 Interactive demo (reasoning + comparison)
│   ├── quant_strategy_reasoning.py  # LLM reasoning examples
│   └── strategy_comparison/      # Traditional vs LLM comparison
│       ├── traditional_finance/  # Technical indicators strategy
│       ├── llm_crypto/           # LLM-based crypto strategy
│       ├── compare_strategies.py # Comparison framework
│       ├── visualize_results.py  # Visualization tools
│       └── quick_start.py        # Quick comparison demo
└── tests/                        # Unit tests
```

## Use Cases

### 1. LLM Reasoning (Qualitative Analysis)
- **Strategy Evaluation**: Analyze trading strategies with deep reasoning
- **Risk Assessment**: Identify risks and suggest improvements
- **Portfolio Optimization**: Design allocation strategies
- **Market Analysis**: Interpret complex market conditions

### 2. Performance Comparison (Quantitative Testing)
- **Traditional vs LLM**: Head-to-head backtesting
- **Multi-Regime Testing**: Test across different market conditions
- **Risk-Adjusted Performance**: Sharpe ratio, drawdown analysis
- **Cost-Benefit Analysis**: Compare API costs vs performance gains

### 3. Investment Master Personas 🎩 (NEW!)
- **Simulate Legendary Investors**: Analyze opportunities as Simons, Buffett, Soros, Dalio, or Wood
- **Multi-Perspective Analysis**: See how different investment philosophies view the same trade
- **Master Debates**: Compare all 5 masters' opinions and find consensus
- **Educational**: Learn different investment frameworks and decision-making styles

### 4. Combined Approach (Recommended)
Use unified_strategy_demo.py to:
- Understand HOW LLM thinks about strategies (reasoning)
- Analyze FROM different master investors' perspectives (personas)
- Measure WHETHER it performs better in practice (comparison)
- Make informed decisions about when to use each approach

## Roadmap

### Core Features
- [ ] Memory/RAG integration (persistent learning)
- [ ] Tool use capability (action execution)
- [ ] Parallel reasoning branches
- [ ] Web UI dashboard

### Real-time Data Integration

#### Financial Market Data
- [ ] **Stock Markets**: NASDAQ, SSE (Shanghai Stock Exchange), SZSE (Shenzhen Stock Exchange)
- [ ] **Futures & Commodities**: CME (Chicago Mercantile Exchange), CBOT (Chicago Board of Trade)
- [ ] **Cryptocurrency**: Real-time prices via Binance API, Coinbase
- [ ] **Foreign Exchange**: Live forex rates (USD/CNY, EUR/USD, etc.)
- [ ] **APIs**: Alpha Vantage, Yahoo Finance, yfinance, AKShare, Tushare

#### Scenario 1: Intelligent Decision Analysis
- [ ] **Weather Data**: Real-time weather, temperature, precipitation
- [ ] **Traffic Data**: Live traffic conditions, congestion index, public transit status
- [ ] **News Feeds**: Breaking news aggregation
- [ ] **APIs**: OpenWeatherMap, QWeather, Amap API, Baidu Maps, NewsAPI, Google News RSS
- **Use Case**: Smart commute recommendations based on weather, traffic, and current events

#### Scenario 2: Public Sentiment Monitoring
- [ ] **Social Media**: Twitter/Weibo trending topics, Reddit discussions, Instagram insights
  - Twitter API v2, Tweepy
  - Reddit API (PRAW - Python Reddit API Wrapper)
  - Instagram Graph API, Apify Instagram Scraper
  - Weibo Open Platform
  - TikTok/Douyin API
- [ ] **News Sources**: Multi-source news aggregation and sentiment analysis
  - NewsAPI, Google News RSS
  - Financial Times API, Reuters API
  - Aggregators: Feedly API, Inoreader
- [ ] **Search Trends**: Google Trends, Baidu Index for emerging topics
  - Google Trends API (pytrends)
  - Baidu Index
  - YouTube Trending API
- **Use Case**: Real-time hotspot detection and sentiment analysis

#### Scenario 3: Lifestyle Assistant
- [ ] **Weather & Air Quality**: AQI, PM2.5, UV index
- [ ] **Transportation**: Multi-modal transit optimization
- [ ] **E-commerce**: Price tracking and comparison
- [ ] **APIs**: AirVisual, OpenWeatherMap, Amap API, Taobao Open Platform, JD Union API
- **Use Case**: Daily decision support with personalized recommendations

## Tech Stack

- **LangGraph**: State machine & workflow orchestration
- **LangChain**: LLM integration & chains
- **OpenAI GPT-4**: Reasoning engine

---

Built for enhanced AI reasoning
