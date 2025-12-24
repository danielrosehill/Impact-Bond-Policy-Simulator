# Agent Architecture Variants

This document outlines two design approaches for the multi-agent simulation framework.

## Variant 1: Simple Architecture

A flat structure with unified agents representing each stakeholder category.

### Structure

```
┌─────────────────────────────────────────────┐
│              Deliberation Crew              │
│                                             │
│  ┌──────────────┐    ┌──────────────┐      │
│  │   Impact     │    │  Government  │      │
│  │   Investor   │    │    Agent     │      │
│  │    Agent     │    │              │      │
│  └──────────────┘    └──────────────┘      │
│                                             │
│  ┌──────────────┐    ┌──────────────┐      │
│  │   Outcomes   │    │   Auditor    │      │
│  │    Payer     │    │    Agent     │      │
│  │    Agent     │    │              │      │
│  └──────────────┘    └──────────────┘      │
│                                             │
│  ┌──────────────┐                          │
│  │  Population  │                          │
│  │    Agent     │                          │
│  └──────────────┘                          │
└─────────────────────────────────────────────┘
```

### Characteristics

- **5 agents total** (Investor, Government, Outcomes Payer, Auditor, Population)
- Each agent synthesizes perspectives from their entire stakeholder category
- Agent backstories incorporate multiple viewpoints (e.g., the investor agent considers both philanthropic and commercial perspectives)
- Simpler to implement and debug
- Faster execution (fewer LLM calls)
- May miss nuanced intra-group tensions

### When to Use

- Early prototyping and validation
- Quick feasibility assessments
- Resource-constrained environments
- When stakeholder diversity within categories is less critical

---

## Variant 2: Complex (Hierarchical) Architecture

A two-tier structure where **lead agents** orchestrate **sub-agents** representing variants within their stakeholder category.

### Structure

```
┌──────────────────────────────────────────────────────────────┐
│                     Deliberation Crew                        │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Impact Investor Lead                    │    │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐   │    │
│  │  │Philanthropic│ │ Commercial  │ │   Blended   │   │    │
│  │  │  Investor   │ │  Investor   │ │   Finance   │   │    │
│  │  └─────────────┘ └─────────────┘ └─────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                Government Lead                       │    │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐   │    │
│  │  │   Local     │ │   State     │ │  Federal    │   │    │
│  │  │ Government  │ │ Government  │ │ Government  │   │    │
│  │  └─────────────┘ └─────────────┘ └─────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Outcomes Payer Lead                     │    │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐   │    │
│  │  │  Treasury   │ │  Program    │ │ Budget      │   │    │
│  │  │  Official   │ │  Manager    │ │ Analyst     │   │    │
│  │  └─────────────┘ └─────────────┘ └─────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                 Auditor Lead                         │    │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐   │    │
│  │  │ Financial   │ │  Impact     │ │   Data      │   │    │
│  │  │  Auditor    │ │ Evaluator   │ │ Scientist   │   │    │
│  │  └─────────────┘ └─────────────┘ └─────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │               Population Lead                        │    │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐   │    │
│  │  │  Community  │ │  Advocacy   │ │   General   │   │    │
│  │  │   Leader    │ │   Group     │ │  Taxpayer   │   │    │
│  │  └─────────────┘ └─────────────┘ └─────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────────┘
```

### Characteristics

- **5 lead agents** that orchestrate their respective sub-agents
- **~15 sub-agents** total (3 variants per category, adjustable)
- Lead agents **invoke sub-agents** to gather diverse perspectives within their category
- Lead agents **synthesize and present** a unified position to the main deliberation
- Captures intra-group tensions (e.g., philanthropic vs. commercial investor priorities)
- More realistic modeling of real stakeholder dynamics
- Higher computational cost but richer output

### Lead Agent Responsibilities

1. **Invoke sub-agents** with the proposal context
2. **Collect and reconcile** sub-agent perspectives
3. **Identify consensus and dissent** within the group
4. **Formulate a negotiating position** that acknowledges internal diversity
5. **Represent the group** in cross-stakeholder deliberation

### Implementation Notes

- Sub-agents can be implemented as separate CrewAI agents or as tool calls from the lead agent
- Consider using delegation in CrewAI (`allow_delegation=True`) for lead agents
- Sub-agent invocations can be parallelized for efficiency
- Lead agents maintain memory of sub-agent consultations

### When to Use

- Full-fidelity simulations
- When intra-stakeholder dynamics are important
- Proposals likely to cause internal disagreement within stakeholder groups
- Research and detailed policy analysis

---

## Comparison Matrix

| Aspect | Simple | Complex |
|--------|--------|---------|
| Total agents | 5 | ~20 (5 leads + 15 sub-agents) |
| LLM calls per simulation | Lower | Higher |
| Intra-group dynamics | Synthesized | Explicit |
| Implementation complexity | Low | Medium-High |
| Debugging difficulty | Easy | Moderate |
| Output richness | Good | Excellent |
| Execution time | Fast | Slower |
| Cost per simulation | Lower | Higher |

---

## Recommendation

**Start with Simple, Graduate to Complex**

1. Implement the Simple architecture first for proof-of-concept
2. Validate that agent deliberation produces meaningful insights
3. Add the Complex architecture as an optional "deep dive" mode
4. Allow users to choose architecture based on their needs (quick assessment vs. detailed analysis)

Both architectures should share the same proposal format and output structure, making them interchangeable from the user's perspective.
