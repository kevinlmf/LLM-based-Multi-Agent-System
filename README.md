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
git clone https://github.com/kevinlmf/LLM-based-Multi-Agent-System
cd LLM-based-Multi-Agent-System

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
python examples/quant_strategy_reasoning.py   # Quant finance strategies
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
├── core/
│   ├── state.py      # Memory: State definitions (TypedDict)
│   ├── agents.py     # Reasoning: Agent implementations
│   └── graph.py      # Controller: LangGraph workflow
├── examples/         # Usage examples
└── tests/            # Unit tests
```

## Use Cases

- **Mathematical Problem Solving**: Complex calculations, proof verification
- **Quantitative Finance**: Strategy evaluation, risk assessment, portfolio optimization
- **Code Review**: Logic verification, bug detection
- **Decision Making**: Multi-criteria analysis, scenario planning

## Roadmap

- [ ] Memory/RAG integration (persistent learning)
- [ ] Tool use capability (action execution)
- [ ] Parallel reasoning branches
- [ ] Web UI dashboard

## Tech Stack

- **LangGraph**: State machine & workflow orchestration
- **LangChain**: LLM integration & chains
- **OpenAI GPT-4**: Reasoning engine

---

Built for enhanced AI reasoning
