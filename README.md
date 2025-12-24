# Impact Bond Policy Simulator

A multi-agent simulation framework for exploring stakeholder reactions to Pay-for-Success (PFS) impact bond proposals before real-world deployment.

## Overview

Pay-for-Success impact bonds are innovative financing mechanisms that bring together public and private money, attracting for-profit investors to address specific social challenges. The core difficulty isn't designing the intervention—it's getting diverse stakeholders to agree on implementation.

This simulator uses AI agents to model stakeholder perspectives and run deliberation simulations, helping identify:
- Where proposals would enjoy support
- Where they would face opposition
- Specific concerns and objections from each stakeholder group
- Potential negotiation leverage points and compromises

## How It Works

### Phase 1: Proposal Generation
An AI agent designs impact bond proposals based on:
- Target population and social challenge
- Proposed intervention mechanism
- Success metrics and measurement approach
- Financial structure (investment amount, return rates, outcomes payments)

### Phase 2: Stakeholder Deliberation
Five stakeholder agents evaluate and debate the proposal:

| Stakeholder | Primary Concerns |
|-------------|------------------|
| **Impact Investors** | ROI potential, risk assessment, exit timeline, portfolio fit |
| **Government** | Policy alignment, budget constraints, political viability, precedent |
| **Outcomes Payers** | Cost-effectiveness, verification burden, long-term obligations |
| **Auditors** | Measurability, data quality, attribution challenges, accountability |
| **General Population** | Equity concerns, public acceptance, unintended consequences |

### Phase 3: Simulation Output
The system produces:
- Support/opposition mapping per stakeholder
- Specific objections with reasoning
- Suggested modifications to increase consensus
- Risk assessment for implementation

## Tech Stack

- **Python 3.11+**
- **CrewAI** - Multi-agent orchestration framework
- **LangChain** - LLM integration layer
- **OpenRouter** - LLM API access (Claude, GPT-4, etc.)

## Project Structure

```
├── planning/            # Design and ideation
│   └── agents/          # Agent persona definitions (markdown specs)
│
└── app/                 # CrewAI simulation application
    ├── agents/          # Python agent implementations
    ├── src/             # Core simulation engine
    ├── config/          # Configuration files
    ├── proposals/       # Proposal YAML files
    └── outputs/         # Simulation results
```

## Getting Started

```bash
cd app

# Create virtual environment
uv venv
source .venv/bin/activate

# Install dependencies
uv pip install -r requirements.txt

# Configure API keys
cp .env.example .env
# Edit .env with your OpenRouter API key

# Run a simulation
python -m src.simulate --proposal proposals/examples/education.yaml
```

## Example Use Cases

1. **Education intervention** - Early childhood literacy program with outcomes tied to 3rd-grade reading scores
2. **Recidivism reduction** - Job training for formerly incarcerated individuals
3. **Homelessness prevention** - Rapid rehousing with wraparound services
4. **Healthcare** - Diabetes prevention program for at-risk populations

## Status

🚧 **In Development** - Framework scaffolding in place, agents and simulation engine under construction.

## License

MIT

## Author

Daniel Rosehill (public@danielrosehill.com)
