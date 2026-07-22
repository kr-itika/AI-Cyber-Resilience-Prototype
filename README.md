# ABDTS — AI-Driven Endpoint Cyber Resilience Platform

**An on-device, explainable, MITRE-mapped Android threat detection platform combining behavioral analytics, machine learning, and automated response — built for the ET AI Hackathon.**

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Problem Statement](#problem-statement)
3. [Solution](#solution)
4. [Features](#features)
5. [Architecture](#architecture)
6. [Technology Stack](#technology-stack)
7. [AI Pipeline](#ai-pipeline)
8. [Machine Learning](#machine-learning)
9. [MITRE ATT&CK Integration](#mitre-attck-integration)
10. [Threat Intelligence](#threat-intelligence)
11. [Explainable AI](#explainable-ai)
12. [Installation](#installation)
13. [Usage](#usage)
14. [Screenshots](#screenshots)
15. [Future Scope](#future-scope)
16. [License](#license)
17. [Contributors](#contributors)

---

## Project Overview

ABDTS (AI-driven Behavioral Threat Detection System) is a fully on-device
Android security platform that detects malicious and privacy-abusive
applications not by matching known signatures, but by learning how *this
specific device's* apps normally behave, and flagging meaningful
deviations — cross-checked against a trained machine learning model, the
MITRE ATT&CK framework, and an offline threat-intelligence knowledge base.
Every verdict comes with a plain-English explanation of *why*, a
prioritized response plan, and a full audit trail — all without a single
byte of telemetry ever leaving the device.

## Problem Statement

Mobile threat detection today mostly falls into two camps:

- **Signature-based antivirus** — fast and cheap, but blind to anything
  novel: repackaged adware, zero-day spyware, or apps that only turn
  malicious after an update.
- **Cloud-based behavioral EDR** — more capable, but requires constant
  connectivity, ships device telemetry off-device (a privacy and
  compliance liability), and is usually built for corporate laptops, not
  the Android endpoints that now carry as much sensitive access as any
  desktop.

Meanwhile, users are given a wall of permission prompts and no way to
understand what an app is actually *doing* with them, and enterprises
deploying Android fleets have little visibility into behavioral drift
across thousands of endpoints without shipping data to a third party.

## Solution

ABDTS runs the entire detection, correlation, machine learning, and
explanation pipeline **on the device itself**:

- Learns a **per-app behavioral baseline** from real usage (not a
  static rulebook).
- Flags **statistical deviations** from that baseline (unusual
  background time, night-time activity, permission escalation).
- Cross-maps flagged behavior to **MITRE ATT&CK for Mobile** techniques
  and tactics.
- Runs those same behavioral features through a **trained Random
  Forest / XGBoost classifier**, exported to **TensorFlow Lite**, for a
  second, independent verdict.
- **Fuses** every signal (behavior, anomaly, MITRE, ML) into one
  confidence-scored threat verdict.
- Explains **why** in natural language and ranked feature importance —
  no black box.
- Cross-references an **offline threat-intelligence knowledge base** of
  known malicious behavioral clusters.
- Recommends and can help execute a **prioritized response playbook**.
- Records everything to an **interactive incident timeline**.
- Presents all of it in an **enterprise-grade Flutter dashboard**
  modeled on tools like Microsoft Defender and CrowdStrike Falcon —
  built for a phone screen.

## Features

| Capability | Description |
|---|---|
| Behavioral Baselining | Per-app running statistics (mean/σ) across 10+ behavioral dimensions, matured over historical scans |
| Anomaly Detection | Statistical deviation scoring against each app's own baseline |
| MITRE ATT&CK Mapping | Behavioral evidence mapped to real ATT&CK for Mobile techniques/tactics with confidence scoring |
| Threat Fusion | Weighted correlation of every signal into one severity + confidence verdict |
| Machine Learning | Random Forest + XGBoost trained on behavioral features, exported to on-device TensorFlow Lite |
| Explainable AI | Natural-language + ranked feature-importance explanation for every verdict |
| Threat Intelligence | Offline behavioral-similarity matching against known malicious app family clusters |
| Incident Timeline | Full chronological, filterable, searchable audit trail per app and device-wide |
| Response Orchestration | Prioritized, playbook-driven recommended actions |
| Enterprise Dashboard | Material 3 Flutter app: Executive Dashboard, Threat Center, Behavior Analytics, MITRE view, Reports (PDF/CSV) |
| 100% On-Device | No telemetry leaves the device; fully offline inference and correlation |

## Architecture

```
Android Detection Layer  →  Behavior Baseline  →  Anomaly Detection
        │                                              │
        └──────────────────────┬───────────────────────┘
                                ▼
                          MITRE Mapping
                                │
                                ▼
                        Threat Fusion Engine  ◀──── ML Inference (TFLite)
                                │
                    ┌───────────┼────────────┐
                    ▼           ▼             ▼
           Explainable AI   Threat Intel   Incident Timeline
                    │                          │
                    └───────────┬──────────────┘
                                ▼
                     Response Orchestrator
                                │
                                ▼
                  Native Bridge (MethodChannel)
                                │
                                ▼
                    Flutter Enterprise Dashboard
```

Nine independent, layered engines feed one fusion point, with the ML
pipeline running as a parallel, independent signal. See
`DEVELOPER_DOCUMENTATION.md` for the full dependency/execution graphs.

## Technology Stack

| Layer | Technology |
|---|---|
| Detection layer | Android (Java), AccessibilityService, UsageStatsManager, DevicePolicyManager |
| Persistence | Room (SQLite) |
| AI/Rule Engines | Pure Java, no third-party ML at runtime for the rule-based layer |
| Machine Learning (training) | Python, scikit-learn (Random Forest), XGBoost, pandas |
| Machine Learning (inference) | TensorFlow Lite, quantized on-device model |
| Native ↔ Flutter Bridge | Flutter `MethodChannel` |
| Mobile UI | Flutter, Material 3, Riverpod, go_router, fl_chart |
| Reporting | `pdf`, `csv`, `share_plus` (Flutter) |

## AI Pipeline

```
FeatureExtractor → BehaviorBaselineManager → AnomalyDetectionEngine
  → MitreAttackMapper → ThreatFusionEngine → ThreatIntelligenceAgent
  → ExplainableAIEngine → IncidentTimelineManager → ResponseOrchestrator
```

The Machine Learning pipeline runs independently off the same
`FeatureVector`, feeding its prediction into the same fusion point as an
additional signal.

## Machine Learning

- **Training**: CSV export of behavioral features → validation → cleaning
  → preprocessing (normalization, categorical encoding, feature
  selection) → stratified train/test split → K-Fold cross-validated
  Random Forest and XGBoost, best model selected by F1.
- **Evaluation**: Accuracy, Precision, Recall, F1, ROC-AUC, confusion
  matrix, tuned decision threshold (not a naive 0.5).
- **Export**: Knowledge-distilled into a small Keras network, quantized
  to TensorFlow Lite for on-device inference in single-digit
  milliseconds.
- **Explainability**: Global feature importance ranking + per-prediction
  feature contribution, surfaced directly in the UI.

## MITRE ATT&CK Integration

Behavioral evidence (overlay + accessibility combinations, boot receiver
usage, permission clusters) is mapped to specific ATT&CK for Mobile
techniques and tactics (e.g. Persistence, Collection, Command and
Control), each with independent confidence scoring, giving every verdict
a standardized, industry-recognized vocabulary rather than a proprietary
"risk score" with no external meaning.

## Threat Intelligence

An offline, bundled knowledge base of known malicious behavioral
clusters (adware, spyware, banking-trojan-style permission patterns) is
matched against each app's behavior profile via similarity scoring — no
internet connection or cloud lookup required, preserving the platform's
fully offline design.

## Explainable AI

Every verdict — rule-based and ML — comes with:
- A natural-language explanation of the dominant contributing factors
- A ranked feature-importance breakdown (global model importance ×
  this app's actual feature values)
- Direct links to the specific evidence (permissions, usage patterns)
  that drove the score

No verdict is ever a bare number with no justification.

## Installation

```bash
# 1. Clone / unpack the repository
git clone <repo-url> && cd abdts

# 2. Android backend
#    Open the android/ module in Android Studio, sync Gradle, run on a
#    device or emulator with Google Play Services (for Play Store
#    installer-source detection).

# 3. ML pipeline (optional — a pre-trained model is bundled)
cd ml/python
pip install -r requirements.txt --break-system-packages
python run_pipeline.py --csv abdts_dataset.csv --out ./export --tune

# 4. Flutter dashboard
cd flutter_app
flutter pub get
flutter run
```

See `USER_MANUAL.md` for permission setup and first-run instructions.

## Usage

1. Launch the app and grant the requested permissions (Usage Access,
   Accessibility, Overlay detection, Notification Access) — each is used
   only to *detect* other apps' use of that capability, not to exercise
   it on the user's behalf.
2. Run a scan from the Executive Dashboard's Quick Actions.
3. Review the Cyber Resilience Score, High Risk Apps, and Recent
   Timeline.
4. Tap any app to open its Threat Center for the full evidence,
   MITRE mapping, and recommended response.
5. Export an Executive Summary, Incident, Threat, or Behavior report as
   PDF or CSV from the Reports screen.

## Screenshots

> _Screenshots to be inserted here before submission:_
> - Executive Dashboard (light + dark)
> - Threat Center detail view
> - MITRE ATT&CK technique view
> - Behavior Analytics charts
> - Incident Timeline
> - Reports / PDF export preview

## Future Scope

- Federated on-device model improvement without centralizing raw data
- Enterprise fleet-management console (aggregate, anonymized rollups
  across managed devices)
- ONNX inference path alongside TensorFlow Lite for broader model
  portability
- Expanded ATT&CK for Mobile technique coverage
- Cross-device baseline transfer for a newly provisioned enterprise phone

## License

This project is submitted for the ET AI Hackathon. License terms:
_[insert chosen license — MIT/Apache 2.0/proprietary — before
submission]_.

## Contributors

_[Insert team member names, roles, and contact information here.]_
