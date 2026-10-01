# Travel Reimbursement Approval Agent

A policy-grounded, tool-calling GenAI agent that reviews employee travel reimbursement claims and returns a structured recommendation: `APPROVE`, `PARTIAL_APPROVE`, `REJECT` or `MANUAL_REVIEW`.

**Deliverable:** [`priyanshuverma.ipynb`](priyanshuverma.ipynb). The notebook holds the full README, the code, the tests, the dashboard, the design notes and the final JSON results.

![Results dashboard](UI%20SS_1.png)

## Results

| Claim | Decision | Approved | Deducted | Deciding factor |
|:--|:--|--:|--:|:--|
| CLM-001 | APPROVE | $1,110 | $0 | Fully compliant, manager tier (POL-APR-02) |
| CLM-002 | REJECT | $0 | $380 | Spa + minibar are ineligible (POL-CAT-02) |
| CLM-003 | PARTIAL_APPROVE | $840 | $100 | Hotel $250/night over the $200 cap (POL-PD-02) |
| CLM-004 | MANUAL_REVIEW | – | – | Business class, missing receipt, > $2,000, nights conflict |
| CLM-005 | MANUAL_REVIEW | – | – | Missing receipt, group-meal vs per-diem ambiguity |

## Quick start

```bash
pip install -r requirements.txt
export GROQ_API_KEY="gsk_..."      # free key from console.groq.com (optional)
jupyter notebook priyanshuverma.ipynb   # Kernel → Restart & Run All
```

If no key is set, the notebook still runs. It switches to a deterministic offline planner that calls the same tools. Ollama and OpenAI are also supported through `LLM_PROVIDER`.

## Design in one line

The LLM decides what to check, deterministic tools decide the numbers, and a guardrail decides what ships.

![Architecture](architecture.png)

![Decision cards](UI%20SS_2.png)
