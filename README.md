# Multi-Agent Reasoning System

A production-grade multi-agent reasoning system using **LangGraph** for enhanced cognitive loops. The system employs three specialized agents (Reasoner, Critic, Refiner) to iteratively improve reasoning quality through structured feedback loops.

## Key Features

- **Multi-Round Reasoning**: Iterative refinement through agent collaboration
- **State Management**: Comprehensive reasoning history tracking with LangGraph
- **Quality Control**: Confidence-based iteration decisions
- **Visualization**: Graph structure visualization
- **Production Ready**: Clean architecture, type hints, error handling
- **Domain Agnostic**: Works for math, logic, strategy evaluation, etc.

## Architecture

```
┌─────────────────────────────────────────────────┐
│                  START                          │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
         ┌─────────────────┐
         │   REASONER      │ ← Generates/refines reasoning
         │   Agent         │
         └────────┬────────┘
                  │
                  ▼
         ┌─────────────────┐
         │   CRITIC        │ ← Evaluates quality
         │   Agent         │   & assigns confidence
         └────────┬────────┘
                  │
         ┌────────▼─────────┐
         │  Confidence OK?  │
         └────────┬─────────┘
                  │
        ┌─────────┴─────────┐
        │                   │
    YES │                   │ NO (iterate)
        │                   │
        ▼                   ▼
  ┌──────────┐      ┌──────────────┐
  │ REFINER  │      │  Back to     │
  │ Agent    │      │  REASONER    │
  └────┬─────┘      └──────────────┘
       │
       ▼
  ┌─────────┐
  │   END   │
  └─────────┘
```

### Agent Roles

1. **Reasoner Agent**
   - Generates step-by-step reasoning
   - Incorporates critique from previous iterations
   - Temperature: 0.7 (creative but structured)

2. **Critic Agent**
   - Evaluates reasoning quality
   - Identifies logical flaws and gaps
   - Assigns confidence score (0.0-1.0)
   - Temperature: 0.3 (precise evaluation)

3. **Refiner Agent**
   - Synthesizes final answer
   - Ensures clarity and completeness
   - Temperature: 0.5 (balanced)

## Installation

### Prerequisites

- Python 3.9+
- OpenAI API key

### Setup

```bash
# 1. Clone or create the project
cd agent_reasoning_system

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set OpenAI API key
export OPENAI_API_KEY='your-api-key-here'

# Or create .env file:
echo "OPENAI_API_KEY=your-api-key-here" > .env
```

### Optional: Install pygraphviz for visualization

**macOS:**
```bash
brew install graphviz
pip install pygraphviz
```

**Linux:**
```bash
sudo apt-get install graphviz graphviz-dev
pip install pygraphviz
```

## Quick Start

### Basic Usage

```python
from core import ReasoningGraph

# Initialize the reasoning system
graph = ReasoningGraph(max_iterations=3)

# Ask a question
question = "What is the best approach to diversify a $100k portfolio?"

# Get reasoned answer
result = graph.reason(question)

print(result["final_answer"])
print(f"Confidence: {result['confidence_score']}")
print(f"Iterations: {result['iterations']}")
```

### Run Examples

```bash
# Math reasoning examples
python examples/math_reasoning.py

# Quantitative strategy reasoning examples
python examples/quant_strategy_reasoning.py
```

## Examples

The project includes comprehensive quantitative finance examples. See `examples/quant_strategy_reasoning.py` for full implementations.

### Example 1: Mean Reversion Strategy

```python
from core import ReasoningGraph

graph = ReasoningGraph(max_iterations=3)

question = """
Evaluate the following mean reversion trading strategy:

Strategy Details:
- Asset: SPY (S&P 500 ETF)
- Signal: Z-score of 20-day moving average
- Entry: When Z-score < -2 (oversold), go LONG
- Exit: When Z-score > 0 (back to mean), close position
- Stop-loss: -3% from entry
- Position sizing: Kelly criterion with 0.5 factor

Market Context:
- Current volatility (VIX): 18
- Recent trend: Sideways with occasional spikes
- Correlation with bonds: -0.3

Questions to address:
1. Is this strategy suitable for current market conditions?
2. What are the key risks?
3. What improvements would you suggest?
4. What should be the expected Sharpe ratio range?
"""

result = graph.reason(question)
print(result["final_answer"])
```

**Output Flow:**
```
🚀 Starting Multi-Agent Reasoning
📝 Question: Evaluate the following mean reversion...
🔄 Max iterations: 3

🧠 [Iteration 1] Reasoner thinking...
🔍 [Iteration 1] Critic evaluating...
   Confidence: 0.75
   → Continuing to next iteration

🧠 [Iteration 2] Reasoner thinking...
🔍 [Iteration 2] Critic evaluating...
   Confidence: 0.92
   → Finalizing (High confidence)

✨ Refiner synthesizing final answer...
✅ Reasoning Complete!
📊 Total iterations: 2
🎯 Final confidence: 0.92
```

The system will iteratively:
1. **Reasoner**: Analyze strategy components
2. **Critic**: Check for missing risk factors (e.g., drawdown analysis)
3. **Reasoner**: Add risk analysis and regime considerations
4. **Critic**: Verify completeness
5. **Refiner**: Synthesize actionable recommendations

### Example 2: Pairs Trading Strategy

```python
question = """
Analyze this pairs trading opportunity:

Pair:
- Stock A: JPM (JP Morgan)
- Stock B: BAC (Bank of America)

Statistical Analysis:
- Cointegration test p-value: 0.03
- Half-life of mean reversion: 5 days
- Historical correlation: 0.85
- Current spread Z-score: 2.3 (2 std dev above mean)

Proposed Trade:
- Short JPM: $100,000
- Long BAC: $100,000
- Hold period: 10 days or until Z-score < 0.5
- Stop-loss: If spread widens to Z-score > 3.0

Context:
- Both stocks report earnings in 2 weeks
- Recent regulatory news affecting financial sector
- Interest rate environment: Fed on hold

Evaluate:
1. Is the cointegration relationship still valid?
2. What is the risk/reward profile?
3. Should we enter this trade given the earnings risk?
4. What position sizing adjustments would you recommend?
"""

result = graph.reason(question)
```

### Example 3: ML-Enhanced Momentum Strategy

```python
question = """
Evaluate this ML-enhanced momentum strategy:

Strategy Framework:
- Universe: Russell 2000 constituents
- Lookback: 60 days momentum
- ML Model: LSTM predicting next 5-day returns
- Position: Long top 20 stocks (highest combined momentum + ML score)
- Rebalancing: Weekly

Backtesting Results (2020-2023):
- Annual Return: 18.5%
- Sharpe Ratio: 1.35
- Max Drawdown: -22%
- Win Rate: 58%
- Avg Holding Period: 12 days

Concerns:
1. Model was trained on 2015-2019 data (pre-COVID)
2. Recent 3-month performance: -5% (market +2%)
3. Model accuracy dropped from 62% to 54%
4. Higher turnover than expected (3.2x per month)

Questions:
1. Is the model degrading? How to diagnose?
2. Should we retrain, adjust, or pause the strategy?
3. How to incorporate regime detection?
4. What risk management improvements would you add?
"""

result = graph.reason(question)
```

### Example 4: Portfolio Optimization

```python
question = """
Design an optimal portfolio allocation strategy:

Investor Profile:
- Risk tolerance: Moderate
- Investment horizon: 5 years
- Current portfolio: 60% stocks, 40% bonds
- AUM: $1M

Available Assets:
1. US Large Cap (SPY): Expected return 8%, Vol 15%
2. US Small Cap (IWM): Expected return 10%, Vol 22%
3. International (EFA): Expected return 7%, Vol 18%
4. Emerging Markets (EEM): Expected return 12%, Vol 28%
5. Corporate Bonds (LQD): Expected return 4%, Vol 8%
6. Treasury Bonds (TLT): Expected return 3%, Vol 12%
7. Real Estate (VNQ): Expected return 9%, Vol 20%
8. Gold (GLD): Expected return 5%, Vol 16%

Constraints:
- Max allocation per asset: 30%
- Min allocation per asset: 5%
- Total equity (stocks): 50-70%
- Total fixed income: 20-40%

Tasks:
1. Propose optimal allocation using modern portfolio theory
2. Calculate expected portfolio Sharpe ratio
3. Identify key risk factors
4. Suggest rebalancing frequency
5. How would you adjust for a recession scenario?
"""

result = graph.reason(question)
```

### Running the Examples

```bash
# Run all quantitative strategy examples
python examples/quant_strategy_reasoning.py

# Results will be saved as JSON files:
# - results_mean_reversion.json
# - results_pairs_trading.json
# - results_ml_momentum.json
# - results_portfolio_optimization.json
```

## Configuration

### Custom Models

```python
graph = ReasoningGraph(
    reasoner_model="gpt-4",
    critic_model="gpt-4",
    refiner_model="gpt-3.5-turbo",  # Can mix models
    max_iterations=5
)
```

### Adjust Temperature

Modify in `core/agents.py`:

```python
class ReasonerAgent(BaseAgent):
    def __init__(self, temperature=0.7):  # Increase for creativity
        ...
```

### Use Anthropic Claude

```python
from langchain_anthropic import ChatAnthropic

# In agents.py, replace:
self.llm = ChatAnthropic(
    model="claude-3-opus-20240229",
    temperature=temperature
)
```

## Understanding Results

### Result Structure

```python
{
    "final_answer": "The synthesized answer",
    "reasoning_history": [
        {
            "role": "reasoner",
            "content": "Step-by-step reasoning...",
            "timestamp": "2024-01-15T10:30:00",
            "metadata": {"iteration": 1}
        },
        {
            "role": "critic",
            "content": "CONFIDENCE: 0.85\nCRITIQUE: ...",
            "timestamp": "2024-01-15T10:30:15",
            "metadata": {"confidence_score": 0.85}
        },
        ...
    ],
    "confidence_score": 0.92,
    "iterations": 2,
    "question": "Original question"
}
```

### Confidence Interpretation

- **0.9-1.0**: Excellent, high certainty
- **0.7-0.89**: Good, minor refinements made
- **< 0.7**: Needed significant iteration

## Visualization

```python
# Generate graph visualization
graph.visualize("reasoning_graph.png")
```

This creates a visual representation of the workflow graph.

## Testing

### Run Tests

```bash
pytest tests/
```

### Create Custom Tests

```python
# tests/test_reasoning.py
from core import ReasoningGraph

def test_basic_reasoning():
    graph = ReasoningGraph()
    result = graph.reason("What is 2+2?")

    assert result["final_answer"] is not None
    assert result["confidence_score"] > 0.5
    assert result["iterations"] >= 1
```

## Project Structure

```
agent_reasoning_system/
├── core/
│   ├── __init__.py          # Package exports
│   ├── state.py             # State definitions (TypedDict)
│   ├── agents.py            # Agent implementations
│   └── graph.py             # LangGraph workflow
├── examples/
│   ├── math_reasoning.py    # Math examples
│   └── quant_strategy_reasoning.py  # Quant finance examples
├── utils/                   # Helper utilities
├── tests/                   # Unit tests
├── requirements.txt         # Dependencies
└── README.md               # This file
```

## Advanced Usage

### Custom Agent Types

```python
class DomainExpertAgent(BaseAgent):
    """Specialized agent for specific domain."""

    def __init__(self):
        super().__init__(temperature=0.5)
        self.role = "domain_expert"

    def analyze(self, state):
        # Custom analysis logic
        pass
```

### Add to Graph

```python
workflow.add_node("expert", self._expert_node)
workflow.add_edge("critic", "expert")
workflow.add_edge("expert", "refiner")
```

### Parallel Reasoning

```python
# In graph.py, add parallel branches
workflow.add_conditional_edges(
    "reasoner",
    lambda s: "branch_a" if condition else "branch_b",
    {"branch_a": "critic_a", "branch_b": "critic_b"}
)
```

## Use Cases

### 1. Mathematical Problem Solving
- Complex calculations
- Proof verification
- Optimization problems

### 2. Quantitative Finance
- Strategy evaluation
- Risk assessment
- Portfolio optimization

### 3. Code Review
- Logic verification
- Bug detection
- Optimization suggestions

### 4. Decision Making
- Multi-criteria analysis
- Risk-benefit evaluation
- Scenario planning

### 5. Research Analysis
- Literature review
- Hypothesis evaluation
- Experimental design

## Roadmap

- [ ] Add more agent types (Planner, Executor)
- [ ] Implement parallel reasoning branches
- [ ] Add memory/RAG integration
- [ ] Support for tool use
- [ ] Web UI dashboard
- [ ] Batch processing mode
- [ ] A/B testing framework

## Contributing

Contributions welcome! Areas of interest:
- New example domains
- Performance optimizations
- Additional agent types
- Testing improvements

## License

MIT License - feel free to use in your projects!

## Acknowledgments

Built with:
- [LangGraph](https://github.com/langchain-ai/langgraph) - State machine framework
- [LangChain](https://github.com/langchain-ai/langchain) - LLM orchestration
- [OpenAI GPT-4](https://openai.com) - Language model

## Contact

Questions? Open an issue or reach out!

---

**Happy Reasoning!**
