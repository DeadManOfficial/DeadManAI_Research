# DeadManAI Research Repository

**NASA-Standard Research Documentation for AI-Augmented Content Production**

---

## Overview

Comprehensive research repository covering LLM agent architecture, networking infrastructure, and content production workflows. All research follows NASA documentation standards (NPR 7120/7123/8735) with full citations, 3-Factor Ruling compliance, and implementation-ready content.

---

## Repository Structure

```
DeadManAI_Research/
├── 00_RESEARCH_INDEX.md        # Master research index
├── R37-R38/                    # Planning with Files (Manus context engineering)
├── R36/                        # WiFi 7 & QoS for streaming
├── R61-R62/                    # Network infrastructure (SDN, remote production)
└── [Additional research documents]
```

---

## Research Categories

| Range | Category | Count |
|-------|----------|-------|
| **R37-R38** | Planning with Files (Manus context engineering, task management) | 2 docs |
| **R36** | WiFi 7 & QoS (802.11be, WMM streaming) | 2 docs |
| **R61-R62** | Network Infrastructure (SDN, remote video production) | 3 docs |

**Total Research Documents:** 9+ (see 00_RESEARCH_INDEX.md)

---

## Research Standards

### Document Structure (11+ Required Sections)

1. **Paper Overview** - Citation, abstract, prior work
2. **Core Problem** - Limitations addressed, tasks affected
3. **Proposed Framework** - Concept, components, process
4. **Experimental Results** - Benchmarks, data, performance
5. **Framework Application** - DeadManAI-specific use cases
6. **Implementation Strategies** - Templates, when to use
7. **Compliance Check** - 3-Factor Ruling assessment
8. **Limitations** - Considerations and mitigations
9. **Source Citations** - Full bibliography
10. **Key Takeaways** - Numbered insights (20+)
11. **Integration Status** - Priorities, next steps

### 3-Factor Ruling

Every source evaluated against:

| Factor | Question | Requirement |
|--------|----------|-------------|
| **Human-in-Loop** | Does human direct, not AI? | MUST PASS |
| **Retention Velocity** | Does it improve content quality/retention? | MUST PASS |
| **Asset Reusability** | Does it create lasting, reusable value? | MUST PASS |

**Scoring:**
- 3/3 = FULL INTEGRATION
- 2/3 = INFORMATIONAL (partial value)
- 1/3 or 0/3 = REJECT

---

## Featured Research

### R37-R38: Planning with Files

**Manus-style context engineering for AI agents**
- File-based planning (task_plan.md, notes.md, deliverable.md)
- Attention manipulation for 50+ tool calls without drift
- Validated by Meta's $2B Manus acquisition
- Production-ready templates included

### R36: WiFi 7 & QoS

**Next-generation wireless for streaming quality**
- 802.11be analysis with Multi-Link Operation
- WMM QoS for reliable streaming
- Latency < 5ms targets for production

### R61-R62: Network Infrastructure

**Professional network design**
- Remote video production networks
- Software-defined networking (SDN) with OpenFlow
- QoS optimization for 4K streaming

---

## Using This Research

### For Developers

```bash
# Clone repository
git clone https://github.com/DeadManOfficial/DeadManAI_Research.git

# Navigate to research
cd DeadManAI_Research

# Read index
cat 00_RESEARCH_INDEX.md
```

### For Integration

1. Review `00_RESEARCH_INDEX.md` for overview
2. Read theory document (R##_Topic.md)
3. Use implementation document (R##_Implementation.md) for production
4. Apply 3-Factor Ruling to validate fit

---

## Research Workflow

All research follows the 9-step process:

```
INTAKE → FETCH → ANALYZE → CONTEXTUALIZE →
  DOCUMENT → INDEX → IMPLEMENT → AUDIT → REPEAT
```

See: [research-integration skill](https://github.com/DeadManOfficial/DeadManAI_Framework_TheUnseen/tree/master/skills/research-integration)

---

## Related Repositories

- **Framework:** [DeadManAI_Framework_TheUnseen](https://github.com/DeadManOfficial/DeadManAI_Framework_TheUnseen)
- **Runtime:** [DeadManAI_Runtime](https://github.com/DeadManOfficial/DeadManAI_Runtime)

---

## Contributing

Research submissions must:
- Pass 3-Factor Ruling (3/3)
- Follow NASA documentation template
- Include full citations
- Provide implementation guidance

---

**Version:** 1.0.0
**Last Updated:** 2026-01-03
**License:** Proprietary
**Maintained By:** DeadManAI Research Team
