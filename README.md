# DDC Skills Collection for Claude Code

A comprehensive collection of AI skills for construction industry automation, organized into 4 super-categories.

## Strategic Documents

| Document | Purpose |
|----------|---------|
| [OPTIMIZER_GUIDE.md](OPTIMIZER_GUIDE.md) | How to communicate with Claude for maximum quality |
| [IMPROVEMENT_ROADMAP.md](IMPROVEMENT_ROADMAP.md) | Strategic plan for skills collection development |
| [ADDITIONAL_SKILLS_PROPOSAL.md](ADDITIONAL_SKILLS_PROPOSAL.md) | Proposed new skills for construction automation |

## Super-Categories Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         DDC SKILLS COLLECTION                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  ┌──────────┐│
│  │  DDC_Toolkit    │  │ DDC_Methodology │  │  DDC_Insights   │  │DDC_Curated│
│  │                 │  │                 │  │                 │  │          ││
│  │ Production-ready│  │ Book-based      │  │ Community       │  │ External ││
│  │ tools & DBs     │  │ methodology     │  │ insights        │  │ curated  ││
│  │                 │  │                 │  │                 │  │          ││
│  │ • Converters    │  │ • 41 skills     │  │ • Workflows     │  │ • PDF    ││
│  │ • CWICR DB      │  │ • 5 parts       │  │ • Best practices│  │ • Excel  ││
│  │ • Kaggle        │  │ • 17 chapters   │  │ • Case studies  │  │ • QA     ││
│  │ • noBIM tool    │  │                 │  │                 │  │ • Security│
│  └─────────────────┘  └─────────────────┘  └─────────────────┘  └──────────┘│
│                                                                              │
│  Source: DDC Tools    Source: DDC Book    Source: Social Media  Source:     │
│  & Repositories                           & Telegram Groups     Community   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

## 1. DDC_Toolkit

**Production-ready tools and databases from DataDrivenConstruction.io**

| Category | Skills | Description |
|----------|--------|-------------|
| CWICR-Database | semantic-search-cwicr | 55,719 work items, 9 languages |
| CAD-Converters | revit-to-excel, ifc-to-excel, dwg-to-excel, dgn-to-excel | No-license CAD conversion |
| Kaggle-Notebooks | 5000-projects-analysis | Large-scale BIM analytics |
| BIM-Visualization | nobim-image-generator | Python-based visualization |

**Sources:**
- [OpenConstructionEstimate-DDC-CWICR](https://github.com/datadrivenconstruction/OpenConstructionEstimate-DDC-CWICR)
- [cad2data Pipeline](https://github.com/datadrivenconstruction/cad2data-Revit-IFC-DWG-DGN-pipeline)
- [Revit-IFC-Creating-images](https://github.com/datadrivenconstruction/Revit-IFC-Creating-images)
- [Kaggle Notebooks](https://www.kaggle.com/artemboiko)

## 2. DDC_Methodology

**Skills based on "Data-Driven Construction" book by Artem Boiko**

| Part | Chapters | Skills | Topics |
|------|----------|--------|--------|
| I | 1.1-1.2 | 3 | Data evolution, ERP systems |
| II | 2.1-2.6 | 14 | Data types, Pandas, LLM, quality |
| III | 3.1-3.5 | 9 | Cost estimation, QTO, scheduling |
| IV | 4.1-4.5 | 14 | Analytics, ETL, ML predictions |
| V | 5.1 | 1 | Digital transformation |

**Total: 41 skills** generated from book chapters

**Source:**
- Book: "Data-Driven Construction" (ISBN 978-3-9826255-9-1)
- Website: https://datadrivenconstruction.io

## 3. DDC_Insights

**Skills derived from community discussions and social media content**

| Category | Focus |
|----------|-------|
| Automation-Workflows | n8n pipelines for construction |
| Industry-Analysis | Digital transformation insights |
| Integration-Patterns | System integration patterns |

**Key Skills:**
- n8n-pto-pipeline (task distribution)
- n8n-cost-estimation (automated estimates)

**Sources:**
- LinkedIn posts and articles
- Telegram groups (n8n Workflows, BIM Open Source)
- Facebook and social media content

## 4. DDC_Curated

**External skills curated for construction industry**

| Category | Skills | Original Source |
|----------|--------|--------------------|
| Document-Generation | pdf-construction, xlsx-construction | Anthropic Skills |
| Data-Processing | web-artifacts, data-analysis | Community |
| Quality-Assurance | security-review-construction, verification-loop-construction, continuous-learning | everything-claude-code |

**New Skills (January 2026):**
- **security-review-construction** - Data security for construction systems
- **verification-loop-construction** - QA for estimates, schedules, reports
- **continuous-learning** - Pattern extraction from sessions

**Sources:**
- Anthropic Official Skills
- [everything-claude-code](https://github.com/affaan-m/everything-claude-code)
- [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
- [obra/superpowers](https://github.com/obra/superpowers)

## Quick Start

### Optimizer Communication

Read [OPTIMIZER_GUIDE.md](OPTIMIZER_GUIDE.md) for best practices on:
- Structuring requests for maximum quality
- Context optimization techniques
- Skill invocation patterns
- Error recovery strategies

### Install Dependencies
```bash
pip install pandas openpyxl qdrant-client openai matplotlib seaborn scikit-learn pdfplumber
```

### Use DDC_Toolkit
```python
# Semantic search for cost estimation
from qdrant_client import QdrantClient
client = QdrantClient("localhost", port=6333)
results = client.search(collection_name="ddc_cwicr_en", query_vector=embedding, limit=10)
```

### Use DDC_Methodology
```python
# Run book analysis script
python analyze_book_skills.py
```

### Use DDC_Insights
Import n8n workflows from JSON files and customize for your needs.

### Use DDC_Curated
Combine with DDC tools for complete construction automation.

## Folder Structure

```
DDC_Skills/
├── DDC_Toolkit/                  # Production tools
│   ├── CWICR-Database/
│   ├── CAD-Converters/
│   ├── Kaggle-Notebooks/
│   └── BIM-Visualization/
│
├── DDC_Methodology/              # Book-based skills
│   ├── Chapter-1.1/
│   ├── Chapter-1.2/
│   │   ... (17 chapters)
│   └── Chapter-5.1/
│
├── DDC_Insights/                 # Community insights
│   ├── Automation-Workflows/
│   ├── Industry-Analysis/
│   └── Integration-Patterns/
│
├── DDC_Curated/                  # External curated
│   ├── Document-Generation/
│   ├── Data-Processing/
│   └── Quality-Assurance/
│
├── OPTIMIZER_GUIDE.md            # Communication best practices
├── IMPROVEMENT_ROADMAP.md        # Strategic development plan
├── ADDITIONAL_SKILLS_PROPOSAL.md # Proposed new skills
└── README.md                     # This file
```

## Roadmap

See [IMPROVEMENT_ROADMAP.md](IMPROVEMENT_ROADMAP.md) for the complete development roadmap:

### Phase 1: Foundation (Current)
- Core DDC tools and database skills
- Book-based methodology skills
- Essential curated skills

### Phase 2: Automation
- n8n workflow expansion
- MCP integrations for construction platforms
- Document processing automation

### Phase 3: Quality Assurance
- Verification skills
- Security review skills
- Continuous learning

### Phase 4: AI/ML
- Cost prediction models
- Schedule optimization
- Computer vision for site photos

### Phase 5: Multi-Agent
- Specialized construction agents
- Agent orchestration framework
- Swarm capabilities

## Resources

- **Book**: "Data-Driven Construction" by Artem Boiko
- **Website**: https://datadrivenconstruction.io
- **GitHub**: https://github.com/datadrivenconstruction
- **Demo**: https://openconstructionestimate.com

## License

- **DDC CWICR Database**: CC BY 4.0
- **DDC Tools**: MIT License
- **Skills**: MIT License
- **Curated Skills**: Varies by source

---

*"If data is the new oil, we need to learn to define it, find it, mine it, refine it, to make it valuable."* — Ralph Montague
