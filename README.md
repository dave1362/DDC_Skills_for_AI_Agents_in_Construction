# DDC Skills Collection for Claude Code

**AI Tools for Construction Company Automation**

> *"If data is the new oil, we need to learn to define it, find it, mine it, refine it, to make it valuable."* — Ralph Montague

---

## What is this?

A collection of **167 ready-to-use skills** for automating construction company processes with AI.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│    YOUR COMPANY                     DDC SKILLS                      RESULT  │
│    ────────────                     ──────────                      ──────  │
│                                                                             │
│    ┌──────────┐                   ┌──────────┐                 ┌──────────┐│
│    │  Excel   │ ───────────────>  │   ETL    │ ─────────────>  │  Auto    ││
│    │ Estimates│                   │ Pipeline │                 │ Reports  ││
│    └──────────┘                   └──────────┘                 └──────────┘│
│                                                                             │
│    ┌──────────┐                   ┌──────────┐                 ┌──────────┐│
│    │  Revit   │ ───────────────>  │   IFC    │ ─────────────>  │  Auto    ││
│    │  Models  │                   │ Parsing  │                 │ Estimates││
│    └──────────┘                   └──────────┘                 └──────────┘│
│                                                                             │
│    ┌──────────┐                   ┌──────────┐                 ┌──────────┐│
│    │  Site    │ ───────────────>  │   AI     │ ─────────────>  │  Auto    ││
│    │  Photos  │                   │ Analysis │                 │ Progress ││
│    └──────────┘                   └──────────┘                 └──────────┘│
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Who is this for?

| Role | What you get | Start with |
|------|--------------|------------|
| **Executive** | Understanding how to automate your company | [GETTING_STARTED.md](GETTING_STARTED.md) |
| **Estimator** | Automated estimate creation | `estimate-builder`, `semantic-search-cwicr` |
| **PM / Superintendent** | Automatic reports | `n8n-daily-report`, `n8n-photo-report` |
| **IT / Developer** | Ready Python scripts and APIs | Any skill from `2_DDC_Book/` |

---

## How does it work?

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         PATH TO AUTOMATION                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STEP 1              STEP 2              STEP 3              STEP 4       │
│   Analyze             Connect             Automate            Scale        │
│   ───────             ───────             ────────            ─────        │
│                                                                             │
│   ┌─────────┐        ┌─────────┐        ┌─────────┐        ┌─────────┐    │
│   │  Find   │   →    │ Remove  │   →    │ Create  │   →    │  Add    │    │
│   │  data   │        │  data   │        │  ETL    │        │  more   │    │
│   │  silos  │        │  silos  │        │ pipeline│        │ skills  │    │
│   └─────────┘        └─────────┘        └─────────┘        └─────────┘    │
│                                                                             │
│   data-silo-         etl-pipeline       n8n-daily-          + ML          │
│   detection          data-type-         report              + AI          │
│                      classifier                             + Agents      │
│                                                                             │
│   Time: 1-2 days     Time: 1 week       Time: 2-4 weeks     Ongoing       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Collection Structure

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              4 CATEGORIES                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────┐      ┌─────────────────────────┐              │
│  │     1_DDC_Toolkit       │      │      2_DDC_Book         │              │
│  │     ──────────────      │      │      ──────────         │              │
│  │                         │      │                         │              │
│  │  Production tools:      │      │  50 skills from book:   │              │
│  │                         │      │                         │              │
│  │  • CWICR Database       │      │  • Data types           │              │
│  │    55,719 work items    │      │  • ETL pipelines        │              │
│  │    9 languages          │      │  • ML models            │              │
│  │                         │      │  • Analytics            │              │
│  │  • CAD Converters       │      │                         │              │
│  │    Revit → Excel        │      │  Source:                │              │
│  │    IFC → Excel          │      │  "Data-Driven           │              │
│  │    DWG → Excel          │      │   Construction"         │              │
│  │                         │      │                         │              │
│  └─────────────────────────┘      └─────────────────────────┘              │
│                                                                             │
│  ┌─────────────────────────┐      ┌─────────────────────────┐              │
│  │     3_DDC_Insights      │      │     4_DDC_Curated       │              │
│  │     ─────────────       │      │     ────────────        │              │
│  │                         │      │                         │              │
│  │  Workflows & cases:     │      │  External skills:       │              │
│  │                         │      │                         │              │
│  │  • n8n automation       │      │  • PDF generation       │              │
│  │  • Daily reports        │      │  • Excel reports        │              │
│  │  • Photo reports w/ AI  │      │  • Quality assurance    │              │
│  │  • Integrations         │      │  • Security             │              │
│  │                         │      │                         │              │
│  │  Source:                │      │  Source:                │              │
│  │  Real-world practice    │      │  Anthropic, GitHub      │              │
│  │                         │      │                         │              │
│  └─────────────────────────┘      └─────────────────────────┘              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Top 10 Skills to Start

| # | Skill | What it does | Time savings |
|---|-------|--------------|--------------|
| 1 | `semantic-search-cwicr` | Search 55,719 work items database | 99% (15 min → 10 sec) |
| 2 | `etl-pipeline` | Automated Excel/PDF processing | 80% |
| 3 | `estimate-builder` | Build estimates from data | 87% |
| 4 | `n8n-daily-report` | Automated daily reports | 92% |
| 5 | `data-silo-detection` | Find isolated data sources | - |
| 6 | `ifc-to-excel` | Extract quantities from BIM | 90% |
| 7 | `n8n-photo-report` | AI-powered site photo analysis | 83% |
| 8 | `cost-prediction` | ML cost forecasting | - |
| 9 | `schedule-delay-analyzer` | Schedule variance analysis | 87% |
| 10 | `kpi-dashboard` | Project KPI dashboard | 75% |

---

## Quick Start

### 1. Installation

```bash
pip install pandas openpyxl ifcopenshell pdfplumber qdrant-client
```

### 2. Example: Search Work Items

```python
# Instead of 15 minutes searching manuals → 10 seconds

from qdrant_client import QdrantClient

client = QdrantClient("localhost", port=6333)
results = client.search(
    collection_name="ddc_cwicr_en",
    query_vector=get_embedding("concrete foundation pour"),
    limit=5
)

# Result:
# [{'code': '03.30.00', 'description': 'Concrete works - foundations', 'unit': 'm³'}]
```

### 3. Example: ETL Pipeline

```python
# Automatic processing of all Excel files from folder

import pandas as pd
from pathlib import Path

# Extract
all_data = [pd.read_excel(f) for f in Path("./estimates/").glob("*.xlsx")]
df = pd.concat(all_data)

# Transform
df['Total'] = df['Quantity'] * df['Unit_Price']
summary = df.groupby('Category')['Total'].sum()

# Load
summary.to_excel("summary_report.xlsx")
```

### 4. Example: Automated Report (n8n)

```
Trigger: Every day at 5:00 PM
    ↓
Get data: Excel + Weather API
    ↓
Process: Aggregation + formatting
    ↓
Result: PDF report → Email to management
```

---

## Core Concept

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   BIM, ERP, Excel, PDF, photos — these are all DATABASES in different      │
│   formats. Understanding this is the key to automation.                     │
│                                                                             │
│   ┌────────────────┐   ┌────────────────┐   ┌────────────────┐             │
│   │   STRUCTURED   │   │ SEMI-STRUCTURED│   │  UNSTRUCTURED  │             │
│   │ ────────────── │   │ ────────────── │   │ ────────────── │             │
│   │                │   │                │   │                │             │
│   │ • Excel        │   │ • IFC (BIM)    │   │ • PDF          │             │
│   │ • SQL Database │   │ • JSON         │   │ • Photos       │             │
│   │ • CSV          │   │ • XML          │   │ • Scans        │             │
│   │                │   │                │   │                │             │
│   │ SQL queries ✓  │   │ Parsing ✓      │   │ AI/OCR ✓       │             │
│   └────────────────┘   └────────────────┘   └────────────────┘             │
│                                                                             │
│   DDC Skills help CONNECT this data and AUTOMATE processes                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Documentation

| Document | Description | Audience |
|----------|-------------|----------|
| [**GETTING_STARTED.md**](GETTING_STARTED.md) | Step-by-step automation guide | Executives, beginners |
| [OPTIMIZER_GUIDE.md](OPTIMIZER_GUIDE.md) | How to work effectively with Claude | Developers |
| [IMPROVEMENT_ROADMAP.md](IMPROVEMENT_ROADMAP.md) | Collection development plan | Contributors |

---

## Folder Structure

```
DDC_Skills/
│
├── 1_DDC_Toolkit/              ← Production tools
│   ├── CWICR-Database/         ← 55,719 work items database
│   ├── CAD-Converters/         ← Revit/IFC/DWG → Excel
│   └── ...
│
├── 2_DDC_Book/                 ← 50 skills from the book
│   ├── Chapter-1.1/            ← Data evolution
│   ├── Chapter-1.2/            ← Data silos
│   ├── Chapter-2.1/            ← Data types
│   ├── Chapter-4.2/            ← ETL pipelines
│   └── ...
│
├── 3_DDC_Insights/             ← Practical workflows
│   └── Automation-Workflows/   ← n8n automation
│
├── 4_DDC_Curated/              ← External skills
│   ├── Document-Generation/    ← PDF/Excel generation
│   └── Quality-Assurance/      ← Quality checks
│
├── GETTING_STARTED.md          ← START HERE
└── README.md                   ← You are here
```

---

## ROI of Automation

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           ROI CALCULATION EXAMPLE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Company: 30 employees, 5 active projects                                 │
│                                                                             │
│   TIME SAVINGS:                                                            │
│   ┌─────────────────────────────────────────────────────────┐              │
│   │ Estimates: 5/month × 14 hr savings     =  70 hr/month  │              │
│   │ Reports:   5 projects × 1.8 hr × 22 days = 198 hr/month │              │
│   │ Tracking:  5 projects × 3.5 hr × 4 weeks =  70 hr/month │              │
│   ├─────────────────────────────────────────────────────────┤              │
│   │ TOTAL:                                   338 hr/month   │              │
│   └─────────────────────────────────────────────────────────┘              │
│                                                                             │
│   At $50/hour rate:        $16,900/month                                   │
│   Conservative (50%):       $8,450/month                                   │
│                                                                             │
│   Implementation cost:      $3,000 (one-time)                              │
│   ─────────────────────────────────────────────                            │
│   PAYBACK PERIOD:          < 1 month                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Resources

| Resource | Link |
|----------|------|
| Book | "Data-Driven Construction" by Artem Boiko (ISBN 978-3-9826255-9-1) |
| Website | https://datadrivenconstruction.io |
| CWICR Demo | https://openconstructionestimate.com |
| GitHub | https://github.com/datadrivenconstruction |

---

## License

- **CWICR Database**: CC BY 4.0
- **DDC Tools**: MIT License
- **Skills**: MIT License

---

**Start automation today → [GETTING_STARTED.md](GETTING_STARTED.md)**
