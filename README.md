# 🧠 Cognitive Parliament: A Multi-Persona Deliberative Agent System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)
![Groq](https://img.shields.io/badge/Groq-LLM-orange?style=for-the-badge)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Colab](https://img.shields.io/badge/Google_Colab-Ready-yellow?style=for-the-badge&logo=googlecolab)

**A novel Agentic AI system where 5 cognitive personas debate, rebut, and vote to reach consensus — instead of a single LLM reasoning alone.**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Amdu-B/Cognitive-Parliament-A-Multi-Persona-Deliberative-Agent-System/blob/main/cognitive_parliament_agent.ipynb)

</div>

---

## 🎯 What Is This?

Most LLM agent projects use a **single reasoning chain** — one model thinks, produces an answer, done. This suffers from:

- 🔴 **Sycophancy** — the model agrees with whatever sounds right
- 🔴 **Hallucination** — no internal cross-checking mechanism
- 🔴 **Single perspective** — blind spots baked in by training
- 🔴 **No adversarial pressure** — conclusions are never stress-tested

**Cognitive Parliament** solves this by instantiating **5 orthogonal cognitive personas** that formally debate in multiple rounds, rebut each other's arguments, and produce a weighted consensus — with a minority report capturing dissent.

> The core insight: *heterogeneous groups make better decisions than homogeneous ones, even when the individuals are smart.* — borrowed from social epistemology.

---

## 🏛️ The 5 Personas

| Persona | Cognitive Role | Deliberate Bias |
|---|---|---|
| 🔍 **The Skeptic** | Epistemic guardian | Challenges assumptions, demands evidence, flags logical gaps |
| 🚀 **The Visionary** | Possibility expander | First-principles thinking, bold long-term implications |
| 😈 **The Devil's Advocate** | Consensus stress-tester | Always argues the strongest opposing case |
| 🔧 **The Pragmatist** | Reality anchor | Feasibility, costs, implementation, real-world constraints |
| ⚖️ **The Ethicist** | Moral compass | Fairness, societal impact, multi-framework ethical analysis |

---

## 🏗️ Architecture

```
  User Query
      │
      ▼
┌─────────────────────────────────────────────┐
│           PARLIAMENT ORCHESTRATOR            │
│                                             │
│  Round 0 — Opening Statements               │
│  ┌─────────┐ ┌──────────┐ ┌─────────────┐  │
│  │ Skeptic │ │Visionary │ │Devil's Adv. │  │
│  └─────────┘ └──────────┘ └─────────────┘  │
│  ┌─────────┐ ┌──────────┐                  │
│  │Pragmtst │ │ Ethicist │                  │
│  └─────────┘ └──────────┘                  │
│                                             │
│  Round 1..N — Debate & Rebuttals            │
│  (Each persona reads all others, rebuts,    │
│   may change mind → weight updated)         │
│                                             │
│  ┌──────────────────────────────────────┐   │
│  │      WEIGHTED CONSENSUS ENGINE       │   │
│  │  Vote + Confidence → Final Answer    │   │
│  │  + Minority Report (if dissent)      │   │
│  └──────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
      │
      ▼
  Final Answer + Full Deliberation Transcript
  + Confidence Evolution Chart
  + Persona Influence Graph
```

---

## ✨ Key Features

- **Multi-round deliberation** — personas rebut each other across N rounds, not just once
- **Dynamic weight system** — epistemic humility is rewarded; personas that update their views gain more influence in the final vote
- **Structured outputs** — every persona response is a Pydantic model with `stance`, `confidence`, `rebuttals`, `changed_mind` fields
- **Minority report** — dissenting views are captured even after consensus
- **Full analytics** — confidence evolution chart + directed influence graph (who rebutted whom)
- **Model-agnostic** — works with Groq (free), Anthropic, or any OpenAI-compatible API

---

## 📦 Tech Stack

| Library | Purpose |
|---|---|
| `groq` | LLM API (free tier — Llama 3.3 70B) |
| `pydantic` | Structured persona output validation |
| `rich` | Beautiful debate transcript rendering |
| `networkx` | Directed persona influence graph |
| `matplotlib` | Confidence evolution & weight charts |
| `pandas` | Session summary DataFrame |

---

## 🚀 Quick Start

### Option 1 — Google Colab (Recommended)

1. Click the **Open in Colab** badge above
2. Go to **🔑 Secrets** (left sidebar) → Add `GROQ_API_KEY`
3. Get your free key at [console.groq.com](https://console.groq.com)
4. **Runtime → Run All**

### Option 2 — Local

```bash
git clone https://github.com/Amdu-B/Cognitive-Parliament-A-Multi-Persona-Deliberative-Agent-System.git
cd Cognitive-Parliament-A-Multi-Persona-Deliberative-Agent-System
pip install groq pydantic rich networkx matplotlib pandas
export GROQ_API_KEY="your-key-here"
jupyter notebook cognitive_parliament_agent.ipynb
```

---

## 💡 Example Queries

The parliament works best on **genuinely hard, multi-dimensional questions**:

```python
# Try any of these:
"Should autonomous AI agents be allowed to take irreversible real-world actions without human approval?"
"Should AI companies be required by law to publish full model weights for frontier models?"
"Should universal basic income be implemented as AI automates more jobs?"
"Is scientific consensus on nutrition science trustworthy enough for public health policy?"
```

---

## 📊 Sample Output

```
╭──────────────────────────────────────────────────────╮
│ 🏛️ PARLIAMENT SESSION BEGINS                         │
│ Should autonomous AI agents take irreversible actions? │
╰──────────────────────────────────────────────────────╯

════════════════════════════════════════
📣 OPENING STATEMENTS
════════════════════════════════════════

╭─ 🔍 The Skeptic ───────────────────────────────────────╮
│ Stance: Strongly oppose — insufficient safeguards      │
│ Confidence: 85%                                        │
│ The evidence for reliable AI judgment in irreversible  │
│ contexts is thin. We have no robust failure-mode       │
│ taxonomy for autonomous action yet...                  │
╰────────────────────────────────────────────────────────╯

... [full debate transcript] ...

╭─ 🏆 PARLIAMENTARY CONSENSUS ───────────────────────────╮
│ Autonomous AI agents should not be permitted to take   │
│ irreversible real-world actions without human approval │
│ under current capability levels...                     │
│                                                        │
│ Parliament Confidence: 78%                             │
│ ⚠️ Minority Report: The Visionary notes this blanket   │
│ restriction may itself cause harm in time-critical...  │
╰────────────────────────────────────────────────────────╯
```

---

## 🔬 Research Foundations

This project sits at the intersection of three real research threads:

| Paper | Connection |
|---|---|
| [Society of Mind — Minsky (1986)](https://en.wikipedia.org/wiki/Society_of_Mind) | Intelligence as emergent property of competing sub-agents |
| [LLM Debate — Du et al. (2023)](https://arxiv.org/abs/2305.14325) | Multi-agent debate measurably improves factual accuracy |
| [Constitutional AI — Anthropic (2022)](https://arxiv.org/abs/2212.08073) | Critique-based self-improvement via structured feedback |

---

## 🛠️ Roadmap / Extensions

- [ ] Tool-augmented personas (Skeptic can web-search to verify claims)
- [ ] Persistent memory across sessions (ChromaDB)
- [ ] Gradio / Streamlit interactive UI
- [ ] Multi-model parliament (each persona runs on a different LLM)
- [ ] Dynamic persona selection based on query domain
- [ ] LLM-as-judge scoring vs human baseline

---

## 📁 Project Structure

```
├── cognitive_parliament_agent.ipynb   # Main notebook (run this)
├── README.md                          # This file
└── parliament_analytics.png           # Generated after first run
```

---

## 🤝 Contributing

Pull requests are welcome. For major changes, open an issue first.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ❤️ by <a href="https://github.com/Amdu-B">Amdu-B</a>

⭐ Star this repo if you find it useful!

</div>
