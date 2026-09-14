# kane-cli Assurance — Vehicle Insurance Quote App

Requirements-linked, evidence-sealed test suite for the **Vehicle Insurance Quote App** (`sampleapp.tricentis.com/101/index.php`), authored via the [kane-cli assurance lifecycle](https://www.testmuai.com/docs/kane-cli-assurance).

---

## What this is

This project demonstrates the full kane-cli assurance loop — from a Product Requirements Document to designed, executed, and coverage-measured browser tests — with every test permanently linked to the acceptance criterion it verifies.

---

## The loop at a glance

```
PRD  →  Ingest  →  Extract  →  Review  →  Design  →  Author  →  Cover
```

| Stage | Command | What happens |
|---|---|---|
| **Capture** | `kane-cli context ingest docs/PRD-vehicle-insurance-quote-app.md --mode agent` | Snapshot the PRD into `.context/` |
| **Extract** | _(runs automatically on 0.7.1+)_ | AI proposes use-cases with cited evidence |
| **Review** | `kane-cli context review --approve <ids>` | Promote use-cases to trusted |
| **Design** | `kane-cli design tests --use-case <id> --mode agent --max 8` | Generate ACs, scenarios, and runnable tests |
| **Author** | `kane-cli testrun run --from-context <ids> --parallel 3 --headless` | Run tests in a real browser, seal evidence |
| **Measure** | `kane-cli cover gaps` | Coverage ribbon: designed % x proven % |
| **Maintain** | `kane-cli maintain reconcile --from docs/PRD-vehicle-insurance-quote-app.md --source-id vehicle_insurance_prd --mode agent` | Reconcile when the PRD changes |

---

## Project structure

```
.
├── docs/
│   └── PRD-vehicle-insurance-quote-app.md   # Source PRD (ingest this)
├── .context/                                 # Assurance store — gitignored, do not edit
├── .testmuai/
│   └── tests/                               # Generated *_test.md files (one per scenario)
├── .gitignore
└── README.md
```

> **Important:** `.context/` is gitignored. It is append-only and not git-mergeable. Collaborators re-run `context ingest` to build their local store from the shared PRD.

---

## Requirements

- kane-cli **0.8.1 or later**

```bash
kane-cli --version
```

- Authenticated LambdaTest account

```bash
kane-cli whoami
```

Install / update:

```bash
npm install -g @testmuai/kane-cli
# or
brew upgrade kane-cli
```

---

## Step-by-step

### 1. Ingest the PRD

```bash
kane-cli context ingest docs/PRD-vehicle-insurance-quote-app.md --mode agent
```

On kane-cli 0.7.1+ this lands the document and runs extraction in one flow. The agent proposes use-cases with exact citations back to the PRD.

### 2. Review use-cases

List what was proposed:

```bash
kane-cli context list --json --inferred
```

Approve the ones you want to design tests for:

```bash
kane-cli context review --approve <uc-id1> <uc-id2> ...
```

### 3. Design tests

For each approved use-case:

```bash
kane-cli design tests --use-case <uc-id> --mode agent --max 8
```

This produces acceptance criteria, scenarios, and runnable `*_test.md` files under `.testmuai/tests/`. Review the design output before authoring.

### 4. Review the design

```bash
kane-cli context list --json --inferred
kane-cli context review --approve <design-ids>
```

### 5. Author and run tests

Run all designed tests in parallel (authorizes in a real browser on first run, replays from cache on subsequent runs):

```bash
kane-cli testrun run --from-context <t-id1>,<t-id2>,... --parallel 3 --headless
```

Or author a single test interactively:

```bash
kane-cli testmd run .testmuai/tests/<name>_test.md --agent
```

### 6. Check coverage

```bash
kane-cli cover gaps                   # full coverage ribbon
kane-cli cover gaps <uc-id>           # dossier for one use-case
kane-cli cover gaps --json            # machine-readable output
```

### 7. View evidence

```bash
kane-cli evidence serve .testmuai/evidence/<pack-id>.evidence
```

---

## When the PRD changes

Do **not** re-ingest the updated file directly. Use reconcile:

```bash
kane-cli maintain reconcile \
  --from docs/PRD-vehicle-insurance-quote-app.md \
  --source-id vehicle_insurance_prd \
  --mode agent
```

This versions the source, marks stale tests, and proposes ADD / MODIFY / ARCHIVE actions for your review.

---

## Application under test

| | |
|---|---|
| **URL** | https://sampleapp.tricentis.com/101/index.php |
| **Journey** | Select vehicle category → Vehicle Data → Insurant Data → Product Data → Price Option → Send Quote → Confirmation |
| **Vehicle categories** | Automobile, Truck, Motorcycle, Camper |
| **P0 scenarios** | 19 (smoke + E2E + navigation + core validation) |
| **Total scenarios** | 38 |

See `docs/PRD-vehicle-insurance-quote-app.md` for the full requirement set, test data, and entry/exit criteria.

---

## Check balance

```bash
kane-cli balance
```
