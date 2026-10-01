# ICSR Case Workbench

A single-file, browser-based workbench that walks through **pharmacovigilance case processing** for one Individual Case Safety Report (ICSR): intake, MedDRA-style coding, Naranjo causality, seriousness/expectedness, reporting clock, narrative, QC and a saved case log.

> **Educational prototype. Not for clinical, regulatory, or patient-care decisions.** Verify all imported and inferred information against source documents.

**This is Project 2 of a 2-project PV portfolio.** It receives supporting cases from [faers-signal-detection](../faers-signal-detection) (Project 1) and sends aggregated feedback back to it.

---

## Live demo

After you enable GitHub Pages (see [Deploy](#deploy-on-github-pages)):
`https://Shashank1gawd.github.io/icsr-case-workbench/`

## Use case

A PV associate, or someone learning PV, needs to process an adverse event case end to end:
- Is the case **valid** (four minimum criteria)?
- What is the **causality** and is the event **serious / expected**?
- What is the **reporting deadline** from Day 0?
- Can the case be **coded**, **narrated**, **quality-checked** and **logged**?

It can also work in a workflow with Project 1: a statistical signal is found there, its supporting cases are processed here one by one, and the results go back as evidence for signal assessment.

## Features

| Tab | What it does |
|---|---|
| **Signal** | Load a case set exported from Project 1 (`PVCASES:` text), see the signal context, and copy feedback back (`PVFEEDBACK:` text). |
| **Intake** | Patient, reporter, suspect product(s), event, dates, outcome, seriousness criteria, expectedness, and other case details. A progress bar checks the **four minimum criteria** (identifiable patient, reporter, suspect drug, adverse event). |
| **Coding** | MedDRA-style coding against a small **fictional demo dictionary** that illustrates the SOC, HLGT, HLT, PT and LLT levels. |
| **Causality** | **Naranjo scale**: ten weighted questions with an automatic score and category (Definite / Probable / Possible / Doubtful). Also copy follow-up questions. |
| **Assessment & Reporting** | Seriousness, expectedness, reporting-clock logic (see below), auto-generated case **narrative** (copy button), follow-up management, and a submission readiness view. |
| **QC & Audit** | Checklist (e.g. duplicate check completed, MedDRA coding verified, causality verified, follow-up items closed, data consistent), consistency warnings, and an audit trail of changes. |
| **Case log** | Save cases, then load, delete or filter them (including by status and signal association). |
| **Learn** | Plain-language explanations of ICSR, minimum criteria, seriousness vs severity, expectedness, Day 0, Naranjo, MedDRA, duplicates, follow-up, QC and audit trail. |

### Reporting-clock logic used

- Serious post-marketing case: expedited report within **15 calendar days** of Day 0.
- Non-serious post-marketing case: no expedited report; goes into periodic reports (PBRER/PSUR).
- Clinical-trial SUSAR (serious, related, unexpected): **7 days** if fatal or life-threatening, otherwise **15 days**.
- Day 0 is when the company first receives valid information.

These are simplified for teaching. Real deadlines depend on the region, regulation and company SOPs.

### Data provenance labels

Each key field shows where its value came from, so nothing inferred is mistaken for fact:

- **Source: FAERS** (reported in the imported record)
- **Inferred: verify**
- **Auto-prefilled: verify** (for example Naranjo Q3 and Q4 prefilled from dechallenge/rechallenge fields; confirm them and write a rationale before the case counts as assessed)
- **Manually entered**

## How to use

1. Open `index.html` in a modern browser, or use the Pages link above. **No internet connection or API is required.**
2. **Standalone:** go to **Intake**, enter the case, then work through Coding → Causality → Assessment & Reporting → QC & Audit, and press **Save case to log**.
3. **With Project 1:** in Project 1's **Investigate** tab press **Copy case set for Project 2**, paste it into the **Signal** tab here, press **Load signal cases**, and process each case. When done, press **Copy feedback for Project 1** and paste it into Project 1's feedback box.
4. Use **Case log** to reopen, filter or delete saved cases.

The two apps are separate sites and do not share browser storage, so copy/paste is the bridge between them.

## Limitations

- **Demo MedDRA only.** The coding dictionary is a small fictional list. Real MedDRA is licensed and far larger.
- **Simplified regulatory logic.** Timelines and criteria are teaching approximations, not a substitute for local regulations or company procedures.
- **Naranjo is an aid, not proof.** It is one structured scale; WHO-UMC is not implemented.
- **Duplicate detection and QC are basic checks**, not a validated system.
- **Local storage only.** The case log and loaded signal are kept in your browser's `localStorage`: private to that browser, lost if you clear site data, not shared across devices. Export or copy anything you need to keep.
- **The audit trail is illustrative.** It is not a tamper-proof, access-controlled audit trail, and there are no electronic signatures or user accounts.
- **No real personal data.** Do **not** enter real patient information. Use fictional or fully anonymised data only.
- No file attachments, no E2B/regulatory-format export (for example no XML submission file), no quizzes.
- Not validated; not suitable for regulatory submissions.

## Deploy on GitHub Pages

See [docs/DEPLOY.md](docs/DEPLOY.md). Short version: push this repo, then **Settings → Pages → Deploy from a branch → `main` / root**.

## Repository layout

```
icsr-case-workbench/
├── index.html        # the whole app (HTML + CSS + JS, no build step)
├── README.md
├── LICENSE
├── .gitignore
└── docs/
    ├── DEPLOY.md     # GitHub upload + Pages steps
    └── PV-CONCEPTS.md# short PV primer for reviewers/recruiters
```

## Tech

Plain HTML, CSS and vanilla JavaScript in one file. No dependencies, no build step, no server.

## Disclaimer

Educational prototype only. Not medical advice, not a validated pharmacovigilance system, and not suitable for regulatory submissions or patient-care decisions. Do not enter real patient data.

## License

MIT, see [LICENSE](LICENSE).

## Author

Shashank Gautam · [LinkedIn](www.linkedin.com/in/shashank-gautam2004) · [GitHub](https://github.com/Shashank1gawd)
