# RespiDx Research Studio v3

**A local-first, explainable respiratory-pattern research sandbox with configurable heuristics, independent warning-sign routing, browser-based signal measurements, reproducible scenario experiments, and exportable reports.**

> [!CAUTION]
> **Educational and software-research use only.** RespiDx is **not** a medical device, clinical decision support product cleared for patient care, AI-trained diagnostic model, validated pneumonia detector, or substitute for a healthcare professional. Its percentages are **not** probabilities of disease. Its severity index is **not** a validated clinical risk score. **Do not use its results to determine treatment, prescribe antibiotics, exclude serious illness, or delay medical care.**
>
> In the UK, call **999** for severe breathing difficulty, blue/grey skin, acute confusion or other signs of a medical emergency; use **NHS 111** or an appropriate urgent clinical service for less immediately life-threatening concerns. The application's warning flags are illustrative and cannot rule out danger when absent.

**Version:** 3.0.0  
**Engine:** `HEURISTIC-3.0` (human-authored rules; no fitted ML model)  
**Distribution:** One self-contained application file (`.html`) containing its HTML, CSS and JavaScript  
**Data processing:** In-browser; no application backend  
**Licence:** **Not specified** in the supplied project files (see [Licence](#licence))

---

## Contents

1. [Overview](#overview)
2. [Screenshots](#screenshots)
3. [Key features](#key-features)
4. [Quick start](#quick-start)
5. [System requirements and dependencies](#system-requirements-and-dependencies)
6. [Application guide](#application-guide)
7. [Research Lab: reproducible experimentation](#research-lab-reproducible-experimentation)
8. [How the heuristic engine works](#how-the-heuristic-engine-works)
9. [Microphone and imaging: what is actually analysed](#microphone-and-imaging-what-is-actually-analysed)
10. [Data, privacy, backups and migration](#data-privacy-backups-and-migration)
11. [Exports and sharing](#exports-and-sharing)
12. [Architecture](#architecture)
13. [Testing and quality assurance](#testing-and-quality-assurance)
14. [Reproducibility and validation](#reproducibility-and-validation)
15. [Known limitations](#known-limitations)
16. [Troubleshooting](#troubleshooting)
17. [Roadmap](#roadmap)
18. [Contributing](#contributing)
19. [Clinical information and references](#clinical-information-and-references)
20. [Licence and acknowledgements](#licence)

---

## Overview

RespiDx Research Studio is a browser-based environment for investigating **how a transparent, hand-weighted set of respiratory rules reacts to different inputs**. It combines manually entered symptoms, observations, laboratory values, microbiology labels, selected imaging descriptions and risk factors in an interactive interface.

The central distinction is between:

- **Experimental pattern support:** the application ranks four authored rule categories and visualises their *relative support*; and
- **Safety-oriented warning-sign routing:** a separate set of rules identifies entered signs that merit emergency or prompt clinical attention, irrespective of the highest-ranked pattern.

The v3 Research Lab extends the application from a simple demonstration dashboard to an **inspectable software experiment**. Users can compare hypothetical inputs without changing the original form, perform leave-one-input-out sensitivity tests, and retain evaluation snapshots with the weight configuration required to replay a historical rule state.

### What RespiDx is

- A single-file, local-first interactive demonstration.
- A transparent model-prototyping and reproducibility tool.
- A useful teaching aid for browser UI engineering, explainability, experimental design and safety-state separation.
- A foundation that could later be benchmarked against suitably licensed, adjudicated research datasets.

### What RespiDx is not

- A trained neural network, LLM-based diagnosis system or validated statistical classifier.
- A predictor of actual pneumonia probability, clinical deterioration or antibiotic benefit.
- An analyser of chest X-rays, ultrasound pixels, DICOM data or recorded cough aetiology.
- A live connection to clinical equipment, medical records, wearables or NHS systems.
- A clinician-approved or regulated medical workflow.

## Screenshots

The repository-ready bundle includes the following image assets:

**Assessment dashboard**

![RespiDx Research Studio v3 assessment dashboard](assets/dashboard.png)

**Research Lab**

![RespiDx v3 Research Lab with scenario and sensitivity tools](assets/research-lab.png)

> If adding this README to an existing repository, copy the `assets/` directory alongside it or update the paths to the screenshots.

## Key features

| Area | Implemented functionality | Interpretation boundary |
|---|---|---|
| Clinical inputs | Age, temperature, SpO₂, respiratory rate, heart rate, blood-pressure notes and optional measured pressures/baseline SpO₂ | User-entered values; not sensor measurements |
| Symptoms and context | Respiratory symptoms, emergency cues, age/chronic-lung/immune/smoking/asthma/pregnancy factors | Rules are demonstrative, not clinically validated |
| Laboratory context | CRP, procalcitonin, WBC, lymphocytes, illustrative breath VOC score and D-dimer note | No medical-test integration |
| Microbiology | Manually selected pathogen and resistance labels | No actual test processing or resistance interpretation |
| Imaging | File selection and manual imaging/ultrasound interpretation labels | Uploaded files are **not** image-analysed |
| Acoustic tools | Preserved synthetic visualizer **and** five-second real-microphone recording with signal descriptors | No cough classification |
| Assessment | Four relative rule categories, severity index, independent escalation messages, missing-data observations, and explanatory signals | No calibrated probability, diagnosis or medical risk score |
| Charts | Six existing chart canvases: rule support, feature radar, symptom bar/radar, risk pie and history trend | Rule visualisations only |
| Research Lab | Hypothetical scenario comparison, leave-one-out sensitivity, snapshots, fingerprint and engineering self-tests | Tests measure code behaviour, not clinical correctness |
| Personal tools | Journal, local rules assistant, synthetic wearable display, voice output/commands, optional notifications | No connected clinical assistant or live wearables |
| Export | PDF, TXT, CSV, backups/snapshots JSON, print, clipboard, handout and explicit sharing controls | Outputs may contain sensitive health information |
| Experience | Dark mode, responsive layouts, keyboard-aware tabs, motion-reduction support, local autosave | Browser compatibility varies |

### Preserved legacy functionality

v3 retains the five v2 assessment tabs, existing element IDs and named JavaScript functions, four example presets, chart locations, settings, symptom/risk forms, local journal, mock wearables, synthetic acoustic animation, real-microphone path, report actions, local assistant, local storage and prior backups. A static preservation check and exercised Chromium workflows support that conclusion; **this is not a guarantee of identical behaviour in every browser or on every device**.

## Quick start

### Option A — Open the HTML directly

1. Download or clone the project files.
2. Open `RespiDx_Research_Studio_v3.html` in a modern browser.
3. Read the **EXAMPLE / DEMO INPUTS** banner. The initial entries are fictional.
4. Select **New blank case** before entering non-demo information.
5. Enter only the information you actually have. Leave unknown measurements **blank**.
6. Select **Evaluate**, then open **4. Decision Dashboard** for the output and charts.
7. Open **6. Research Lab** to compare hypothetical scenarios or run the built-in engineering checks.

**No installation, npm, Python packages, database, account or API key is required for normal use.**

### Option B — Run from localhost

Using a local development server is helpful for browser permissions and repeatable development:

```bash
# From the directory containing the HTML file
python -m http.server 8000
```

Then navigate to:

```text
http://localhost:8000/RespiDx_Research_Studio_v3.html
```

Alternatively, run a server provided by your IDE. Use `Ctrl+C` to stop the Python server.

### Example repository layout

```text
RespiDx-Research-Studio/
├── README.md
├── RespiDx_Research_Studio_v3.html
└── assets/
    ├── dashboard.png
    └── research-lab.png
```

The HTML application does not require the images in `assets/`; those are README screenshots only.

## System requirements and dependencies

| Requirement | Notes |
|---|---|
| Browser | Current Chromium-based browser recommended; Firefox is also a reasonable target but not exhaustively verified |
| Operating system | Any platform with a capable browser; tested workflow used headless Chromium on Linux |
| JavaScript | Required |
| Internet | **Not required for core functionality**; optional CDNs improve charts/PDF presentation |
| Server | Not required for standard use |
| Microphone | Optional; needs supported media APIs, browser permission and normally a secure origin (`https://` or `http://localhost`) |
| Browser storage | Optional for persistence; if blocked, the app uses a session-memory fallback |

### Optional runtime libraries

The HTML references:

- **Chart.js**, via `https://cdn.jsdelivr.net/npm/chart.js`, for richer charts.
- **jsPDF 2.5.1**, via `https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js`, for enhanced PDF reports.

If those scripts cannot load, the application falls back to native Canvas chart drawing and a built-in **text-only PDF 1.4** export routine. The offline fallback was exercised in Chromium.

**Supply-chain note:** the Chart.js URL currently does **not** pin an exact version. A future reproducible release should pin and locally bundle audited dependency versions. Loading optional libraries from a CDN also makes network requests to those providers; see [Privacy](#data-privacy-backups-and-migration).

## Application guide

The main interface contains **six tabs**, while the toolbar exposes common controls such as **Save**, **Restore**, **New blank case**, **Export backup**, **Clear local data**, **Theme**, **Help**, **Settings**, **Journal** and **Evaluate**.

### 1. Clinical & Risk

Enter demographics and observations including optional **systolic/diastolic blood pressure** and baseline oxygen saturation. Select symptoms such as cough, fever, wheeze, pleuritic discomfort, shortness of breath and warning signs; choose contextual risk factors.

The form has four fictional presets:

- **Viral bronchitis-like**
- **Pneumonia-like**
- **COPD flare-like**
- **Severe / red flag**

**Apply preset** replaces the case controls with a consistent example state, avoiding stale fields from a previous preset. Presets do not depict real patients. Use **Reset section** controls where appropriate.

Input validation checks configured ranges and rejects measured diastolic blood pressure that is not below systolic. For example, the implemented ranges are temperature **30–44°C**, SpO₂ **50–100%**, respiratory rate **4–80/min**, heart rate **25–240/min**, CRP **0–500 mg/L**, and procalcitonin **0–100 ng/mL**. These are **software input bounds, not clinical reference intervals**.

### 2. Biomarkers & Microbiology

Manually enter CRP, procalcitonin, total white-cell count, lymphocyte percentage and the illustrative breath VOC proxy. Select an optional D-dimer note, pathogen label and resistance marker.

A selected pathogen is an **input label**, not a verified test result. A selected viral organism does not exclude pneumonia or coinfection; elevated inflammatory markers do not independently prove a bacterial cause or antibiotic need. Resistance labels are not a susceptibility or treatment recommendation engine.

### 3. Imaging & Acoustic

Two distinct acoustic paths are present:

1. **Start acoustic capture** runs the inherited **synthetic animation**; it does **not** use the microphone.
2. **Record Cough (5 sec)**, available through the Decision Dashboard, requests actual microphone access and displays basic waveform descriptors.

The imaging upload accepts filenames/metadata for common imaging-related file types. The contents of images, videos, PDFs or DICOM files are **not processed for diagnostic findings**. The **Imaging pattern** and **Lung ultrasound cue** selectors are manually chosen descriptive labels used by the heuristic engine.

### 4. Decision Dashboard

An explicit **Evaluate** triggers the processing overlay and records a manual evaluation. The display contains:

- Leading experimental pattern and relative rule support.
- A **0–100 heuristic severity index** (not a clinical score).
- Relative **score lead** (the margin between the first and second rule classes; not model confidence).
- Independent warning-sign escalation and recommendations.
- Model explanations, missing-data messages and optional CRB65 context.
- Six preserved chart canvases and the report/export controls.

If **Auto-evaluate** is enabled, changes to form inputs update a **preview** without adding a manual history record. The preview does not replace an explicit saved evaluation.

The adult-oriented ranking is **suppressed for ages under 16**, although safety messages remain active. This does **not** constitute a paediatric assessment.

### 5. Comparison & Reference

Provides written comparisons of bronchitis-type illness and pneumonia symptoms, a side-by-side table and expandable educational detail. These summaries illustrate overlapping symptoms; **symptom patterns alone cannot reliably identify the cause of an illness**.

### 6. Research Lab

See the full workflow below. It is intended for software experiments, not patient decision-making.

### Additional panels

- **Evaluation statistics:** aggregates manual rule-score differences, not health outcomes.
- **Wearable Dashboard:** generates explicitly labelled random simulated observations, with no device connection.
- **Local rules assistant:** responds using fixed local logic; **not** a connected LLM or clinical chatbot.
- **Journal:** saves typed entries in the browser and can export a text journal.
- **Settings:** changes symptom/pneumonia/risk-factor weights, voice and preview preferences, update interval and ticker speed. This modifies the experimental scoring behaviour, not scientific validity.

## Research Lab: reproducible experimentation

The Research Lab operates on a snapshot of form inputs and, where appropriate, the current editable weights. It is designed so users can examine how source-code rules behave without accidentally overwriting the active case.

### Counterfactual scenario comparison

1. Enter or load an adult fictional case.
2. Open **6. Research Lab**.
3. Select one variable (for example, **SpO₂** or **Respiratory rate**).
4. Enter a hypothetical value and select **Compare scenarios**.
5. Compare the original and hypothetical severity index, leading rule class, score lead and independent safety-gate label.

Supported changes include selected numeric observations, two checkboxes (wheeze and breathlessness) and the manually chosen imaging pattern.

**Important:** this is a *model counterfactual*, not a patient-specific forecast. It does not predict what would happen to someone if their oxygen saturation or symptoms changed. The live form is intentionally unchanged.

### Leave-one-input-out sensitivity

Select **Analyse model sensitivity**. The application temporarily removes each currently supplied observation or selected flag, reruns the rule engine, and reports:

- Difference in the heuristic severity index.
- Difference in support for the original top-ranked class.
- Whether the independent safety-routing category changed.

Rows are sorted by the size of rule-output changes. The visible table displays up to **25** entries; the CSV export includes the calculated result set. A large sensitivity value reveals **dependence on authored rules**, not clinical feature importance, causal effect or measured model accuracy.

Use **Export results CSV** to save the output. Formula-like spreadsheet strings are escaped to reduce CSV injection risk.

### Evaluation snapshots and replay

Each **explicit** evaluation produces a timestamped snapshot containing:

- Input values and selected options.
- Whether the case was a **sample** or a **blank/user case**.
- `HEURISTIC-3.0` model identifier.
- The corresponding editable weight vectors.
- A compact recorded result (pattern, index, rule lead, escalation).

The browser keeps at most **60 snapshots**. The Research Lab can **Inspect**, **Restore**, **Export snapshots JSON** or **Clear snapshots**. Restoring a snapshot reinstates its saved inputs and weights and refreshes the preview without adding another manual evaluation.

The displayed case fingerprint uses **FNV-1a**, a deterministic non-cryptographic hash for spotting changes to an input state. It is **not** a security signature, a tamper-proof audit trail or a guarantee of unique identification.

### Built-in engineering self-tests

The **Run self-tests** button executes **14 deterministic assertions** against isolated input snapshots. These check expected software invariants such as non-mutation, blank-case behaviour, urgent-warning overrides and rule normalisation. They are intentionally distinct from a medical validation study.

## How the heuristic engine works

### Four experimental classes

The engine computes authored rule-support scores for:

1. **Viral bronchitis**
2. **Bacterial lower respiratory tract infection (LRTI)**
3. **Pneumonia**
4. **Reactive airway / COPD flare**

Each class begins with a manually selected baseline and receives additions or reductions based on entered observations. Some contributions are scaled by the weights editable in Settings. For example, checked wheeze, high respiratory rate, manually selected focal imaging, CRP and selected pathogen labels change particular class scores.

If the raw class scores are \(s_1, s_2, s_3, s_4\), the application clamps each to at least 0.5 and computes relative support:

$$
q_i=\frac{\max(0.5,s_i)}{\sum_{j=1}^{4}\max(0.5,s_j)}\times100.
$$

These four numbers sum to **100% by construction**. **They must not be called disease probabilities or posteriors**: the model has no fitted likelihood function, training dataset, outcome-based calibration or clinically tested discrimination.

The displayed **score lead** is:

$$
L=q_{(1)}-q_{(2)},
$$

where \(q_{(1)}\) and \(q_{(2)}\) are the two highest relative supports. This expresses **ranking separation**, not diagnostic confidence.

### Heuristic severity index

A separate manually specified severity tally accumulates weighted warning signals. It is clamped to **0–100** for display. It is **not** a validated mortality, sepsis, hospitalisation or pneumonia severity score.

### Safety gate and missing information

The app also examines entered emergency and warning indicators **independently of the top class**. For example, manually checked severe respiratory distress, cyanosis or acute confusion may trigger emergency-oriented messaging even if the rule ranking favours a non-pneumonia category.

Missing numerical fields do not automatically count as positive threshold findings. A blank form returns **insufficient information**. The dashboard reports missing tracked measurements and avoids implying that an absent flag excludes serious illness.

The current threshold rules are **illustrative software logic**, not a complete NICE/NHS pathway. In particular, users with chronic low oxygen baselines or complex coexisting conditions require individual clinical interpretation; the dashboard cannot handle this robustly.

### CRB65 context

Where age, respiratory rate and measured systolic/diastolic pressures are provided for an adult, the app can show the conventional four-item **CRB65 context**. This is included for educational comparison only. CRB65 has a specific role in **clinical management of diagnosed community-acquired pneumonia** and is not a test that detects pneumonia or replaces an examination.

## Microphone and imaging: what is actually analysed

### Microphone signal path

The actual **Record Cough (5 sec)** button uses the browser's microphone APIs (`getUserMedia`, `MediaRecorder`, and `AudioContext`/`AnalyserNode`) when available. It collects waveform/spectrum samples over approximately five seconds and displays:

| Descriptor | Meaning |
|---|---|
| RMS amplitude | Average sampled-window signal magnitude, in full-scale audio units |
| Peak amplitude | Maximum sampled absolute signal magnitude, in full-scale units |
| Spectral centroid | Approximate mean frequency centre of sampled spectra, in hertz |
| Window count | Number of processing samples included in the estimate |

The processing path samples windows periodically, not every decoded sample. It does **not** identify cough events, segment respiratory phases, estimate pathogens, classify pneumonia, train a neural network or deliver a medical interpretation.

Audio data is held transiently during recording and deliberately **discarded after capture**; audio is not part of backup or saved case history. Descriptors are for user inspection only. Stop browser microphone access using your browser's permission controls if needed.

### Imaging-file path

Imaging input stores **file names, sizes and similar metadata**, not image analysis results. Selecting `Focal lobar consolidation` or another interpretation label is a manual research input, **not** an automated observation from an uploaded image.

## Data, privacy, backups and migration

### Local persistence

RespiDx uses browser **`localStorage`**, where available, to keep the current inputs, weights, preferences, evaluation history, snapshots and journal. It also uses additional legacy keys for current/last evaluation and selected factors. If `localStorage` is unavailable, it falls back to a memory-backed session state that disappears when the page is closed.

Relevant implemented keys include:

```text
respidx_state
respidx_theme
evaluationResult
lastEvaluation
selectedSymptoms
selectedRiskFactors
journalEntries
```

These entries are **not encrypted**. Anyone with access to the same browser profile or local storage may be able to read them. Do not enter identifiable patient data in shared or untrusted environments. Browser profiles, extensions, backups and operating-system account security remain relevant.

**No app-specific backend receives your form values**, but the optional CDN script requests, browser sharing services and external sites opened by your choice have their own data practices. The repository does not include a network privacy assessment or formal security audit.

### Save, restore and clear

- **Save:** persist current form/settings/history to browser storage.
- **Restore:** reload an existing local state.
- **New blank case:** clear form observations without deleting the existing history or journal.
- **Clear local data:** after confirmation, remove the application's known browser storage keys and reset the in-memory case/history. **This cannot delete previously downloaded files or copies elsewhere.**

### JSON backup / v2 migration

Select **Export backup** to download `RespiDx_backup.json`, including the state and journal. The current backup schema is **version 3**, and the import path accepts appropriately formed **v2 or v3** backups.

To migrate from v2:

1. Open v2 and export its JSON backup.
2. Open v3 in your preferred browser/profile.
3. Use the **Import backup** file control.
4. Confirm the replacement of current browser state.
5. Review restored measurements, weights, journal and evaluation history before running a new evaluation.
6. Export a fresh v3 backup for safekeeping.

The importer limits input JSON backup size to **2 MB** and checks a basic application identifier and schema. This is **not** a cryptographic authenticity check. Do not import backups from untrusted parties.

**Retention limits in code:** up to **300** evaluation history/record entries, **60** snapshots and **50** imaging metadata entries in stored state. Snapshot JSON and full-backup JSON are distinct exports.

### Sharing precautions

Copy, PDF/TXT/CSV, native OS sharing and backup files may disclose health-related information. **Share** requests confirmation before passing the summary to the browser's native share API; the generic **X/Twitter** action opens a prewritten research message rather than embedding the current health assessment.

## Exports and sharing

| Action | Output / behaviour | Important detail |
|---|---|---|
| Export PDF | `RespiDx_Research_Report.pdf` | Enhanced charts with jsPDF when available; basic text-only multi-page PDF offline |
| Download TXT | `RespiDx_Research_Report.txt` | Human-readable assessment summary |
| Export CSV | `RespiDx_evaluation_trends.csv` | Manual evaluation history; **not** real patient outcome trends |
| Copy summary | Clipboard text | Can include sensitive entered context |
| Print | Browser print layout | Print styles hide interface controls |
| Share | Native browser/OS sharing if supported | Requires explicit confirmation; behaviour varies by browser |
| X / Twitter | Generic research-oriented post | Does **not** include the current measurements/result text |
| Speak result | Browser speech synthesis | Depends on browser speech support and settings |
| Patient handout | `RespiDx_Research_Handout.txt` | Research summary, **not** clinician-endorsed instructions |
| Journal export | Text file | Local journal contents |
| Export backup | `RespiDx_backup.json` | Full supported saved state and journal |
| Research sensitivity | `RespiDx_v3_sensitivity.csv` | Leave-one-out rule differences |
| Research snapshots | `RespiDx_v3_snapshots.json` | Historical inputs, weights and compact results |

No export is evidence that the underlying assessment is medically correct.

## Architecture

All runtime application code is embedded in a single HTML file. Conceptually, the application is divided into the following subsystems:

```text
┌─────────────────────────────────────────────────────────┐
│  Browser UI: forms, six tabs, charts, settings, journal │
└───────────────────────────┬─────────────────────────────┘
                            │ entered state
               ┌────────────▼──────────────┐
               │ Validation and snapshots  │
               └────────────┬──────────────┘
                            │
             ┌──────────────▼──────────────────┐
             │ HEURISTIC-3.0 rule evaluation   │
             │  • four pattern-support scores │
             │  • independent escalation gate │
             │  • missing-data / safety notes │
             └──────────────┬──────────────────┘
                            │
          ┌─────────────────┴──────────────────┐
          ▼                                    ▼
┌────────────────────┐             ┌──────────────────────┐
│ Decision dashboard │             │ Research Lab         │
│ charts & reports   │             │ scenario / ablation  │
└──────────┬─────────┘             │ snapshots / tests    │
           │                       └──────────┬───────────┘
           └────────────────┬─────────────────┘
                            ▼
                   ┌─────────────────┐
                   │ Browser storage │
                   │ + file exports  │
                   └─────────────────┘

Other separate paths:
  Microphone → local sampled waveform descriptors → discard audio
  Synthetic wearables/acoustic animation → labelled UI demonstration
  Imaging file picker → file metadata only
```

### Main internal modules

The current script is organised around these responsibilities (rather than separate imported ES modules):

- `state`, `collectState()`, `applyState()`, `saveState()` — application state and persistence.
- `validateInputs()`, `startBlankCase()`, `setPreset()` — form correctness and example control.
- `calculateScores()` — authored differential support, severity tally, warnings and explanations.
- `evaluate()`, `renderCharts()`, `updateTextResult()` — assessment orchestration and display.
- `recordCoughDetailed()`, `stopCoughRecording()` — browser microphone path.
- `exportPdf()`, `exportBasicPdf()`, `downloadTxt()`, `exportTrendCSV()` — report outputs.
- `renderScenario()`, `runSensitivity()`, `makeCaseSnapshot()`, `runLabTests()` — v3 research methods.
- `exportBackup()`, `importBackup()`, `clearLocalData()` — data control and migration.

The scoring function supports an **input override**, allowing Research Lab experiments to compute alternative results without changing the current DOM fields. Restored historical snapshots include the editable weight vectors to support reproducing the prior configuration.

### Design trade-offs

**Advantages:** near-zero deployment overhead, offline resilience, source inspectability, no backend health-data ingestion, easy archiving.  
**Costs:** large monolithic source, limited separation of concerns, browser-specific media support, unencrypted local persistence, no automatic central updates, and reliance on authored rules without clinical evidence.

## Testing and quality assurance

The following **recorded test results** accompany the v3 development artefacts. They reflect the tested build and conditions, **not** universal correctness:

| Check group | Recorded result | Coverage |
|---|---:|---|
| JavaScript syntax | Passed | Node 22 parser check |
| Chromium main smoke suite | **29/29 passed** | Six tabs/charts, blank case, live and manual evaluation, safety/under-16 behaviour, scenario analysis, snapshot/backup, offline export, mock audio and theme |
| Chromium extended suite | **18/18 passed** | Original IDs/functions, presets, settings, rules assistant, journal, imaging metadata and v2 backup migration |
| Built-in Research Lab tests | **14/14 passed** | Determinism and software invariants |
| Synthetic microphone-stream test | Passed | Real media-processing path exercised using a synthetic oscillator stream, not a physical microphone |
| v3 JSON backup integrity check | Passed | Case snapshots preserve input values and editable weights |
| Native PDF validation | Passed | A4 PDF opened successfully, with extractable text |
| Unhandled JavaScript exceptions in exercised browser flows | **None observed** | Chromium test scenarios only |

These groups overlap and cannot meaningfully be combined into a single measured percentage of overall product quality. External CDN/jsPDF execution, every supported browser release, screen-reader accessibility, real hardware microphone permissions and medical performance **have not been exhaustively verified**.

### Run the built-in checks

1. Open the app.
2. Go to **6. Research Lab**.
3. Select **Run self-tests**.
4. Inspect the per-check PASS/FAIL list and the aggregate result.

### Suggested reproducible developer checks

If you have Node.js installed, extract the inline script and run a syntax check (no npm installation needed):

```bash
python - <<'PY'
from pathlib import Path
from bs4 import BeautifulSoup
html = Path('RespiDx_Research_Studio_v3.html').read_text(encoding='utf-8')
soup = BeautifulSoup(html, 'html.parser')
scripts = [s.get_text() for s in soup.find_all('script') if not s.get('src')]
Path('respidx-inline.js').write_text('\n'.join(scripts), encoding='utf-8')
PY
node --check respidx-inline.js
```

This *example* extraction command uses **Beautiful Soup** (`python -m pip install beautifulsoup4`) only for this optional developer check; the app itself does not need it. If you prefer no third-party Python dependency, extract the inline script manually or use a standard-library HTML parser.

Recommended additional tests for future releases:

1. **Baseline parity:** compare v2 and v3 UI controls, named functions and visible behaviour for the same cases.
2. **Storage migration:** restore v2/v3 backups, reject malformed/untrusted JSON and confirm correct retention boundaries.
3. **Safety invariants:** verify that severe warning signs always override benign-looking pattern rankings.
4. **Data-absence invariants:** ensure missing values never become measured positives or artificial reassurance.
5. **Microphone:** test permissions denied, permission revoked, device missing, interrupted capture, and repeated start/stop.
6. **Browsers:** test current Chrome, Edge, Firefox and Safari on desktop/mobile, including offline mode.
7. **Accessibility:** keyboard-only workflows, reduced motion, focus management, colour contrast, screen readers, ARIA states and print contrast.
8. **Exports:** compare online jsPDF and offline fallback for pagination, unicode/encoding, and content completeness.
9. **Security:** investigate XSS/import handling, local-data retention, content-security policy and dependency version pinning.
10. **Performance:** test responsiveness and chart export with long manual histories and maximum snapshot counts.

## Reproducibility and validation

The Research Lab makes **the current code's outputs** repeatable under a fixed input/weight configuration. It does **not** validate the relationship between those outputs and real-world disease states.

To reproduce a particular rule result:

1. Use the **same v3 source file/model revision**.
2. Restore the same snapshot, including **its saved weights**.
3. Avoid changing Settings between comparisons.
4. Compare the output categories, score lead, severity index and escalation gate.
5. Export case snapshots to preserve an inspectable JSON record.

The display fingerprint only covers the input state and is not cryptographic or a substitute for preserving the exact HTML version. File checksums (e.g. SHA-256) and versioned release tags would improve reproducibility in a future release.

### What meaningful clinical validation would require

Before treating future versions as medical classifiers:

- Define the intended patient population, care setting, target condition and reference standard.
- Obtain appropriate permissions for **licensed, de-identified, clinician-adjudicated data**.
- Establish a reproducible protocol and separate development, calibration and untouched external test sets.
- Compare the current heuristic baseline with simpler statistical models and any proposed ML approach.
- Report discrimination, calibration, sensitivity/specificity at predeclared thresholds, uncertainty intervals and subgroup/error analyses.
- Assess data leakage, distribution shift, missingness, disease prevalence, prevalence sensitivity and false reassurance.
- Obtain relevant clinical, governance, legal, privacy, ethics and medical-device regulatory review before any patient-facing deployment.

**No such study or performance dataset accompanies the present release.**

## Known limitations

1. **No validated diagnosis.** The four classes and the safety gate are authored rules, not clinically trained or tested systems.
2. **No meaningful disease probability or confidence.** Percentages are normalised score shares; score lead measures rank separation.
3. **No automatic imaging interpretation.** Image/video/PDF/DICOM uploads are metadata-only.
4. **No medically useful cough classification.** Microphone analysis measures only generic acoustic descriptors.
5. **No real wearable integration.** Wearable readings and lung-sound values are random simulated displays.
6. **No clinical NLP.** The local assistant uses predefined response logic, not a connected model.
7. **Adult orientation.** No paediatric score; ages under 16 are blocked from adult differential output.
8. **Incomplete clinical context.** Baseline illness, comorbidity, observation uncertainty, interpretation of tests and real examination cannot be modelled adequately.
9. **Offline differences.** Native fallback charts and PDFs are less rich than CDN-assisted rendering, particularly PDF charts and text fidelity.
10. **Browser-dependent APIs.** Speech, microphone, notifications, printing and sharing vary by browser and permission model.
11. **Storage is not encrypted.** Browser data and exported files can be sensitive.
12. **Not comprehensively regression-tested.** Recorded Chromium checks do not cover every hardware/browser/input combination.
13. **Limited model reproducibility across arbitrary edits.** Snapshots preserve inputs and weights, but identical output also requires the same source-code revision and supporting environment.
14. **A single-file codebase is harder to maintain** than a modular, test-driven architecture at larger scale.
15. **No medical-device regulatory clearance, formal security audit, independent clinical evidence or operational monitoring** is provided.

## Troubleshooting

| Symptom | Likely explanation | Action |
|---|---|---|
| Page opens but no charts | Browser scripts disabled or renderer unavailable | Enable JavaScript, try a current browser; check browser console |
| Chart.js or jsPDF unavailable | CDN blocked / offline | Use built-in fallback; reconnect for richer rendering |
| Blank case shows “Insufficient information” | Missing input is intentionally not inferred | Enter known observations; keep unknown values blank |
| Red safety warning with non-pneumonia top class | Safety gate is independent of class ranking | Do **not** interpret the pattern ranking as reassuring |
| Evaluate refuses to run | Numeric range or pressure-order validation failed | Correct flagged fields or leave genuinely missing values blank |
| Microphone capture unavailable | Unsupported API, insecure origin, blocked permission or absent device | Serve on `localhost`, grant permission, check browser/media settings |
| No real cough features on “Start acoustic capture” | That is the intentionally synthetic legacy control | Use **Record Cough (5 sec)** for actual signal descriptors |
| Uploaded X-ray is not interpreted | Application only records file metadata | Supply manual observation labels only for research demonstration; do not treat them as automated findings |
| Auto-preview does not add a history point | Deliberate distinction between preview and manual run | Press **Evaluate** to record a snapshot and manual history entry |
| Previous data disappears after reload | Storage blocked or private session expired | Enable persistent browser storage and export a local JSON backup |
| PDF lacks charts / typography differs | Offline text-only fallback is running | Restore optional CDN access for enhanced jsPDF presentation |
| Import reports incompatibility | JSON is malformed, oversized, unknown schema or from another app | Use the app's v2/v3 Export backup; maximum import size is 2 MB |
| Clearing data did not remove downloaded exports | Browser storage controls cannot erase files already saved outside the app | Delete exported files separately through your operating system |

## Roadmap

The following are **proposed future work**, not features already implemented:

**Near-term engineering**

- Move to an ES-module architecture while preserving a distributable standalone HTML build.
- Pin or vendor third-party dependencies; add CSP and a dependency-review process.
- Expand automated test coverage across browsers, adverse input cases and accessible interaction paths.
- Add opt-in encrypted local exports and explicit per-case retention controls.
- Improve report templates, audit provenance, schema migration and portable regression fixtures.
- Add a visual rule editor, change log and unit tests for every individual threshold.

**Research infrastructure**

- Implement a blinded benchmark pipeline for approved, de-identified cases.
- Compare the heuristic to calibrated reference classifiers using appropriate medical evaluation metrics.
- Conduct external validation, subgroup analysis and uncertainty assessment.
- Investigate locally executed, privacy-governed audio/image models only with appropriate training data and suitable validation.
- Keep clinician review and regulatory assessment as mandatory steps before any deployment in real healthcare.

These milestones deliberately prioritise **evidence and safety** over adding unsupported “AI diagnosis” claims.

## Contributing

Contributions are welcome in principle, subject to the repository owner's eventual contribution and licence policies. High-value changes include reproducible bug fixes, cross-browser tests, clearer scientific labelling, accessibility improvements, privacy protections and controlled experiments that **retain existing functionality**.

Recommended contribution workflow:

1. Open an issue describing the feature, bug or research question.
2. Include reproduction steps and the exact source version/browser.
3. Add or update tests, especially for changed safety rules and storage migration.
4. Preserve existing controls and data schemas unless a migration is explicitly implemented.
5. Report any known limitation or performance regression.
6. Clearly separate a **software assertion** from a **clinically validated finding**.

Do not submit identifiable patient data, copyrighted medical datasets without permission, unreviewed clinical claims or credentials/API secrets to a public repository.

## Clinical information and references

These are useful **external clinical context**, **not evidence validating this application's engine**:

- [NICE NG250 — Pneumonia: diagnosis and management](https://www.nice.org.uk/guidance/ng250/chapter/Recommendations)
- [NICE NG237 — Suspected acute respiratory infection in people aged 16 and over](https://www.nice.org.uk/guidance/ng237/chapter/Recommendations)
- [NHS — Shortness of breath](https://www.nhs.uk/symptoms/shortness-of-breath/)
- [NHS — Pneumonia](https://www.nhs.uk/conditions/pneumonia/)

See the appropriate current professional guidance when developing a genuine clinical protocol. Software thresholds and heuristic class weights here are illustrative and should **not** be attributed to NICE or the NHS.

## Licence

**No software licence was provided with the supplied v3 source.** Until the copyright holder adds an explicit `LICENSE` file, prospective contributors and redistributors should **not assume** this project is open-source or licensed for unrestricted reuse. This README does not grant additional rights.

If the project is intended for public GitHub distribution, the repository owner should choose and add an appropriate licence and define third-party asset/data usage rights.

## Acknowledgements

The prototype uses standard browser technologies and optionally loads **Chart.js** and **jsPDF**. Medical reference links are informational only; neither the NHS nor NICE endorses this software.

---

**RespiDx Research Studio v3 · `HEURISTIC-3.0`**  
*Explore the rules. Preserve the evidence boundary. Never confuse an interactive demonstration with a diagnosis.*
