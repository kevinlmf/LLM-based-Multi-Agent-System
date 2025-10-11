# Multi-Agent Reasoning System

A production-grade **Cognitive Loop** framework using LangGraph with three specialized agents that iteratively improve reasoning quality across multiple domains.

## System Overview

This is an **extensible multi-agent reasoning framework** designed to be applied to various real-world scenarios. The core engine provides:
- Iterative reasoning refinement
- Confidence-based decision routing
- Multi-perspective analysis
- Pluggable domain adapters

### Current Status
- ✅ **Core Engine**: Fully implemented (Reasoner → Critic → Refiner loop)
- ✅ **Scenario**: Quantitative Trading Strategy Analysis (see `examples/`)
-  **Future Scenarios**: Smart decision analysis, sentiment monitoring, lifestyle assistant (see Roadmap)

## Cognitive Loop Architecture

The core reasoning engine implements a complete cognitive cycle that can be adapted to any domain:

| Phase | Module | Technical Implementation |
|------|---------|---------|
| 1. Receive | Input Adapter | Question Input / State Initialization |
| 2. Record | Memory | LangGraph State / Reasoning History |
| 3. Understand | Reasoning Core | **Reasoner Agent** (LLM-powered) |
| 4. Decide | Controller | **Critic Agent** (Confidence-based routing) |
| 5. Execute | Tool Layer | **Refiner Agent** (Answer synthesis) |
| 6. Reflect | Feedback Module | Multi-iteration loop with critique |

**Core Flow:** Input → Reasoner → Critic → (iterate if needed) → Refiner → Output

## Installation

```bash
git clone https://github.com/kevinlmf/Multi-Agent-LLM-System
cd Multi-Agent-LLM-System
pip install -r requirements.txt
export OPENAI_API_KEY='your-api-key-here'
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

```bash
agent_reasoning_system/
├── core/        # Core reasoning engine
│   ├── state.py     # Manages agent memory and contextual state
│   ├── agents.py    # Defines Reasoner, Critic, and Refiner agents
│   └── graph.py     # LangGraph controller that orchestrates the cognitive loop
│
├── examples/    # Demonstrations and reasoning experiments
│                 # (Includes unified strategy reasoning and strategy comparison demos)
│
└── tests/       # Unit tests for reasoning and workflow integrity
```
##  Applied Scenario

The first real-world application demonstrates the cognitive loop in financial strategy analysis:

### Features

1. **LLM Reasoning Engine**  
   - Iterative strategy evaluation and refinement  
   - Risk analysis and portfolio recommendations  
   - Context-aware market interpretation  

2. **Investment Master Personas**  
   - Simulate legendary investors (Simons, Buffett, Soros, Dalio, Wood)  
   - Multi-perspective reasoning and consensus building  
   - Learn diverse investment philosophies  

3. **Performance Comparison**  
   - Backtest traditional vs LLM-driven strategies  
   - Test robustness across different market regimes  
   - Evaluate Sharpe ratio, drawdown, and efficiency  


### Try It Now
```bash
# Interactive demo with all features
python examples/unified_strategy_demo.py

# Individual components
python examples/quant_strategy_reasoning.py      # LLM reasoning only
python examples/strategy_comparison/quick_start.py  # Traditional vs LLM
```

##  Roadmap

### Phase 1: Core Engine Enhancement (Current)
- [ ] Memory/RAG integration (persistent learning across sessions)
- [ ] Tool use capability (API calls, data retrieval)
- [ ] Parallel reasoning branches (explore multiple solutions)
- [ ] Web UI dashboard (interactive monitoring)
- [x] ✅ Real-time financial data integration (yfinance, market APIs)

### Phase 2: Future Application Scenarios

#### Scenario 2: Intelligent Decision Assistant 
**Status**:  Planned
- **Example Use Cases**:
  - "Should I take the subway or bike to work today considering weather and traffic?"
  - "Recommend the best time to leave for my 3 PM meeting downtown"
  - "Is today a good day for outdoor activities?"

#### Scenario 3: Public Sentiment Monitor 
- **Example Use Cases**:
  - "Analyze how people perceive **Artificial Intelligence (AI)**."
  - "Understand public opinion on the **Federal Reserve’s interest rate cuts**."
  - "Explore how people think about **LeBron James** — especially his decisons."



## Tech Stack

- **LangGraph**: State machine & workflow orchestration
- **LangChain**: LLM integration & chains
- **OpenAI GPT-4**: Reasoning engine

---
Better reasoning, brighter tomorrow✨

