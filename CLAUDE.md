# CLAUDE.md - Project Context for AI Assistants

## What This Project Is

This is a **multi-agent simulation framework** for testing Pay-for-Success (PFS) impact bond proposals. The goal is to use AI agents representing different stakeholders to predict how a proposed impact bond would be received—identifying support, opposition, and specific concerns before real-world deployment.

## Domain Background

### What Are Pay-for-Success Impact Bonds?

Pay-for-Success (PFS) contracts, also called Social Impact Bonds (SIBs), are outcomes-based financing mechanisms where:

1. **Private investors** provide upfront capital for a social intervention
2. **Service providers** deliver the intervention to a target population
3. **Independent evaluators** measure outcomes against predefined metrics
4. **Outcomes payers** (usually government) repay investors only if outcomes are achieved
5. Investors receive their principal plus a return if successful; they lose capital if unsuccessful

### The Core Challenge

The technical design of impact bonds is well-understood. The real challenge is **stakeholder alignment**—getting investors, government, service providers, auditors, and the public to agree on:
- Target metrics (what counts as "success"?)
- Attribution methodology (how do we know the intervention caused the outcome?)
- Risk allocation (who bears what risks?)
- Return rates (what's fair compensation for investor risk?)
- Population targeting (who benefits, and is that equitable?)

This simulator models these negotiations before they happen in reality.

## Architecture

### Multi-Agent Framework: CrewAI

We use [CrewAI](https://github.com/joaomdmoura/crewai) for agent orchestration because:
- Clean agent/task/crew abstractions
- Built-in support for agent collaboration and delegation
- Memory and context management
- Easy integration with various LLM backends

### Agent Definitions

Each stakeholder is modeled as a CrewAI Agent with:
- **Role**: Their position in the impact bond ecosystem
- **Goal**: What they're trying to achieve/protect
- **Backstory**: Context that shapes their perspective
- **Tools**: Any specific analysis capabilities they have

#### The Five Stakeholder Agents

1. **Impact Investor Agent** (`app/agents/investor.py`)
   - Evaluates ROI potential and risk
   - Considers portfolio fit and exit timeline
   - May represent different investor archetypes (philanthropic vs. commercial)

2. **Government Agent** (`app/agents/government.py`)
   - Assesses policy alignment and political viability
   - Weighs budget constraints and precedent concerns
   - May represent different levels (local, state, federal)

3. **Outcomes Payer Agent** (`app/agents/outcomes_payer.py`)
   - Focuses on cost-effectiveness vs. traditional spending
   - Evaluates verification burden and long-term obligations
   - Often overlaps with government but has distinct fiscal concerns

4. **Auditor Agent** (`app/agents/auditor.py`)
   - Scrutinizes measurability and data quality
   - Identifies attribution challenges
   - Ensures accountability mechanisms are robust

5. **General Population Agent** (`app/agents/population.py`)
   - Represents public interest and equity concerns
   - Identifies potential unintended consequences
   - Evaluates whether the proposal serves community needs

### Simulation Flow

```
┌─────────────────┐
│ Proposal Input  │  (YAML/JSON defining the impact bond)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Proposal Agent  │  (Optional: generates/refines proposals)
└────────┬────────┘
         │
         ▼
┌─────────────────────────────────────────┐
│         Deliberation Crew               │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐   │
│  │Investor │ │Government│ │ Auditor │   │
│  └────┬────┘ └────┬────┘ └────┬────┘   │
│       │           │           │         │
│  ┌────┴────┐ ┌────┴────┐              │
│  │Outcomes │ │Population│              │
│  │ Payer   │ │         │              │
│  └─────────┘ └─────────┘              │
└────────────────────┬────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────┐
│            Simulation Output            │
│  - Support/opposition by stakeholder    │
│  - Specific objections with reasoning   │
│  - Suggested modifications              │
│  - Consensus probability score          │
└─────────────────────────────────────────┘
```

## Directory Structure

```
planning/                # Design and ideation phase
  └── agents/            # Agent persona specs (markdown)
      └── project-ideator.md

app/                     # CrewAI simulation application
  ├── agents/            # Python agent implementations
  │   ├── investor.py
  │   ├── government.py
  │   ├── outcomes_payer.py
  │   ├── auditor.py
  │   └── population.py
  ├── proposals/         # Impact bond proposal definitions
  │   └── examples/      # Sample proposals for testing
  ├── simulations/       # Simulation configurations
  │   └── configs/       # YAML configs for different scenarios
  ├── outputs/           # Simulation results (gitignored)
  ├── config/            # Application configuration
  └── src/               # Core simulation engine
      ├── crew.py        # CrewAI crew definitions
      ├── tasks.py       # Task definitions for deliberation
      ├── simulate.py    # Main entry point
      └── utils/         # Helper utilities
```

## Development Guidelines

### Python Environment

Use `uv` to create a virtual environment:
```bash
cd app
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

### LLM Configuration

This project uses OpenRouter for LLM access. Set `OPENROUTER_API_KEY` in `app/.env`.

Default model preferences:
- Agent reasoning: Claude Sonnet 4 or GPT-4o
- Quick evaluations: Claude Haiku or GPT-4o-mini

### Running Simulations

```bash
cd app

# Run with a specific proposal
python -m src.simulate --proposal proposals/examples/education.yaml

# Run with verbose agent output
python -m src.simulate --proposal proposals/examples/education.yaml --verbose

# Run multiple rounds of deliberation
python -m src.simulate --proposal proposals/examples/education.yaml --rounds 3
```

## Key Design Decisions

1. **YAML for proposals**: Human-readable, easy to version control, supports comments
2. **Separate agent definitions**: Each stakeholder in its own file for clarity
3. **OpenRouter over direct APIs**: Flexibility to switch models, unified billing
4. **CrewAI over alternatives**: Better agent collaboration model than AutoGen for this use case

## Future Enhancements

- [ ] Web UI for proposal input and visualization
- [ ] Historical impact bond database for training/context
- [ ] Agent memory across simulation runs
- [ ] Quantitative outcome predictions (not just qualitative deliberation)
- [ ] Integration with real policy databases

## Useful Resources

- [Government Outcomes Lab (Oxford)](https://golab.bsg.ox.ac.uk/) - Impact bond research
- [Brookings Impact Bonds Database](https://www.brookings.edu/articles/impact-bonds-database/) - Real-world examples
- [CrewAI Documentation](https://docs.crewai.com/)
- [LangChain Documentation](https://python.langchain.com/)
