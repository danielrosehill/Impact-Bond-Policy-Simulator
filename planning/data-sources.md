# Data Sources and External Resources

This document outlines available data sources and how they might be used in the simulation.

---

## Source Materials

Reference materials are collected in:

```
planning/design/context/source-materials/
```

These materials can be suggested as **reliable sources for RAG (Retrieval-Augmented Generation)** if the simulation incorporates external data retrieval. They provide authoritative context for agent reasoning.

---

## Available Resources

### Government Outcomes Lab (GO Lab) - Oxford

The primary academic resource for impact bond research.

**Knowledge Base & Data**:
- [INDIGO Knowledge Bank](https://golab.bsg.ox.ac.uk/knowledge-bank/indigo/) - Central repository
- [Impact Bond Dataset v2](https://golab.bsg.ox.ac.uk/knowledge-bank/indigo/impact-bond-dataset-v2/) - Structured data on global impact bonds
- [Fund Directory](https://golab.bsg.ox.ac.uk/knowledge-bank/indigo/fund-directory/) - Outcomes funds listing
- [Pipeline Dataset](https://golab.bsg.ox.ac.uk/knowledge-bank/indigo/pipeline-dataset/) - Projects in development

**Snapshot**: `June-2025-Snapshot.pdf` in source-materials contains a point-in-time export.

### Brookings Institution

- [Impact Bonds Collection](https://www.brookings.edu/collection/impact-bonds/) - Research and analysis

### Education Outcomes Fund (EOF)

- [EOF Work](https://www.educationoutcomesfund.org/work) - Example of an outcomes fund in operation

---

## Priority: Actual Impact Bond Examples

For the simulation to produce realistic outputs, agents need exposure to **what real impact bonds look like**. This includes:

### Deal Documentation (Instructive Material)

- Term sheets
- Outcome metric specifications
- Payment structures
- Stakeholder agreements
- Evaluation frameworks

### Why This Matters

Real examples provide:
1. **Structural templates**: How deals are actually structured
2. **Metric precedents**: What outcome metrics have been used and accepted
3. **Negotiation outcomes**: What terms different stakeholders have agreed to
4. **Failure cases**: What has gone wrong and why

### Potential Sources for Examples

- GO Lab INDIGO dataset (structured data, may need enrichment)
- Published case studies from intermediaries (Social Finance, Third Sector Capital)
- Academic papers with detailed deal descriptions
- Government procurement documents (where public)

---

## RAG Integration Notes

If implementing RAG for agent context:

1. **Source materials folder** contains curated, reliable documents
2. **GO Lab INDIGO** provides structured data suitable for programmatic access
3. **Example deals** would provide the most valuable retrieval targets for agent queries like:
   - "What outcome metrics have been used for recidivism programs?"
   - "What return rates have investors accepted for education interventions?"
   - "How have attribution challenges been handled in employment programs?"

The simulation doesn't require RAG to function, but access to real deal data would significantly improve the realism and specificity of agent deliberations.
