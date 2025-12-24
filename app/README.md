# App

The CrewAI multi-agent simulation application.

## Structure

```
app/
├── agents/          # Python agent implementations
├── src/             # Core simulation engine
├── config/          # Configuration files
├── proposals/       # Proposal YAML files for simulation
├── simulations/     # Simulation run configs
└── outputs/         # Results (gitignored)
```

## Running

```bash
cd app
uv venv && source .venv/bin/activate
uv pip install -r requirements.txt
python -m src.simulate --proposal proposals/examples/education.yaml
```
