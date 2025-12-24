# Planning

This folder contains design documents, agent definitions, and ideation work for the Impact Bond Policy Simulator.

## Contents

- **agents/** - Agent persona definitions and behavioral specifications
  - **ideation/** - Agents that generate and refine impact bond proposals
  - **roleplay/** - Stakeholder agents that evaluate proposals in simulations
- **proposals/** - Impact bond proposal ideas and templates (to be created)

## Agent Structure

### Ideation Agents (`agents/ideation/`)

Agents that help generate, refine, and structure impact bond proposals:

| Agent | Purpose |
|-------|---------|
| `project-ideator.md` | Generates novel impact bond ideas |
| `proposal-drafter.md` | Structures ideas into formal proposals |
| `terms-drafter.md` | Drafts contract terms and conditions |
| `proposals/project-shortlister.md` | Evaluates and prioritizes proposals |

### Roleplay Agents (`agents/roleplay/`)

Stakeholder agents that evaluate proposals during simulations:

#### Investors (`roleplay/investors/`)
| Agent | Perspective |
|-------|-------------|
| `impact-investor.md` | Balanced impact/return investor |
| `catalytic-capital.md` | Patient capital, accepts below-market returns |
| `return-focused-investor.md` | Commercially-oriented, market-rate returns |
| `meta-investor.md` | Intermediary structuring deals |

#### Government (`roleplay/gov/`)
| Agent | Perspective |
|-------|-------------|
| `gov-representative.md` | General government official |
| `gov-evaluator.md` | Analyst comparing intervention to existing methods |
| `gov-fiscal.md` | Budget/finance officer focused on fiscal implications |

#### Delivery Organizations (`roleplay/delivery-org/`)
| Agent | Perspective |
|-------|-------------|
| `service-provider.md` | Balanced organizational perspective |
| `service-provider-advocate.md` | Internal champion for PFS participation |
| `service-provider-skeptic.md` | Internal voice cautioning against participation |

#### Beneficiaries (`roleplay/beneficiaries/`)
| Agent | Perspective |
|-------|-------------|
| `service-user.md` | Individual receiving services |
| `community-advocate.md` | Community-level representative |

#### Media (`roleplay/media/`)
| Agent | Perspective |
|-------|-------------|
| `mainstream-media.md` | General news reporter |
| `trade-media.md` | Sector/impact investing trade press |

#### Academia (`roleplay/academia/`)
| Agent | Perspective |
|-------|-------------|
| `academic-researcher.md` | Impartial scholar studying PFS |
| `policy-economist.md` | Economist focused on incentives and efficiency |

#### Audit (`roleplay/audit/`)
| Agent | Perspective |
|-------|-------------|
| `auditor.md` | Independent evaluator assessing measurability |

## Agent Definition Format

All roleplay agents follow a standardized format:

```markdown
# Agent Name

> Brief one-line description

## Role
Who this agent represents in the impact bond ecosystem.

## Goal
What this agent is trying to achieve or protect in the deliberation.

## Backstory
Context and experience that shapes this agent's perspective.

## Key Concerns
- Specific issues this stakeholder focuses on
- Factors that drive their evaluation

## Evaluation Criteria
**Would Support If:**
- Conditions that would lead to support

**Red Flags:**
- Issues that would trigger opposition

## Typical Questions
Questions this stakeholder would ask about a proposal.
```

This format maps directly to CrewAI agent configuration:
- **Role** → `role` parameter
- **Goal** → `goal` parameter
- **Backstory** → `backstory` parameter
- **Key Concerns** and **Evaluation Criteria** → inform agent reasoning
- **Typical Questions** → inform task definitions

## Workflow

1. Define agent personas in `agents/` as markdown specs
2. Draft proposal ideas for simulation testing
3. Select which agents to include in each simulation
4. Translate finalized designs into code in `../app/`

## Simulation Configuration

When running simulations, select agents based on the proposal context:

**Minimal simulation** (5 agents):
- 1 investor, 1 government, 1 service provider, 1 beneficiary, 1 auditor

**Standard simulation** (8-10 agents):
- 2-3 investors, 2 government, 2 service providers, 1-2 beneficiaries, 1 auditor

**Comprehensive simulation** (all agents):
- All investor variants, all government variants, all stakeholder types, media, academia
