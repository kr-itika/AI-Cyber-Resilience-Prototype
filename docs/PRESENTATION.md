# ET AI Hackathon — Presentation Content
### ABDTS: AI-Driven Endpoint Cyber Resilience Platform
**Total estimated speaking time: ~11 minutes (fits a 12-slide, ~10-12 min slot)**

---

## Slide 1 — Title
**Title:** ABDTS — AI-Driven Endpoint Cyber Resilience Platform

**Bullet points:**
- On-device, explainable, MITRE-mapped Android threat detection
- Behavioral AI + Machine Learning + Automated Response
- 100% offline — zero telemetry

**Speaker notes:** "Good [morning/afternoon], we're presenting ABDTS — a
cybersecurity platform that learns how your apps behave, catches the ones
that don't, and explains exactly why, entirely on your phone, with no
data ever leaving the device."

**Suggested diagram:** App logo / hero shot of the Executive Dashboard.

**Suggested animation:** Simple fade-in of title, then dashboard
screenshot slides in from the right.

**Estimated speaking time:** 30 seconds

---

## Slide 2 — The Problem
**Title:** Mobile Threat Detection Is Stuck Between Two Bad Options

**Bullet points:**
- Signature-based antivirus: fast, but blind to novel/repackaged malware
- Cloud-based EDR: capable, but needs connectivity and ships your data offsite
- Users get permission prompts, not understanding
- Enterprises get fleets of Android devices with zero behavioral visibility

**Speaker notes:** "Existing approaches force a trade-off: either you get
signature matching that misses anything new, or you get real behavioral
detection that requires sending your data to someone else's cloud. Nobody
has solved this for Android specifically, on-device."

**Suggested diagram:** Two-column comparison (Signature-based vs
Cloud-EDR) with a red X on both, question mark in the middle.

**Suggested animation:** Build the two columns in sequentially, then
reveal the gap.

**Estimated speaking time:** 45 seconds

---

## Slide 3 — Our Solution
**Title:** Behavioral AI That Never Leaves Your Phone

**Bullet points:**
- Learns each app's own behavioral baseline
- Detects statistical deviations, not just known signatures
- Cross-validates with a trained ML model AND the MITRE ATT&CK framework
- Explains every verdict in plain language
- Fully offline, fully on-device

**Speaker notes:** "ABDTS solves this by putting the entire pipeline — 
detection, machine learning, correlation, and explanation — on the
device itself. No cloud round-trip, no telemetry, no compromise."

**Suggested diagram:** Simple funnel: Behavior → Anomaly → ML → MITRE →
Fusion → Verdict, all inside a phone outline.

**Suggested animation:** Funnel stages light up one at a time.

**Estimated speaking time:** 45 seconds

---

## Slide 4 — Architecture Overview
**Title:** Nine Engines, One Verdict

**Bullet points:**
- Behavior Baseline → Anomaly Detection → MITRE Mapping → Threat Fusion
- Machine Learning runs in parallel, feeding the same fusion point
- Explainable AI, Incident Timeline, Response Orchestrator, Threat Intelligence
- Clean, layered, dependency-checked architecture (verified acyclic)

**Speaker notes:** "This isn't one model doing everything — it's nine
purpose-built engines, each independently verifiable, correlating into
one confidence-scored verdict. We've actually run a dependency audit to
confirm there are no circular dependencies in this design."

**Suggested diagram:** The architecture graph from the README (behavior →
anomaly → mitre → fusion → explainability/threatintel/timeline/response),
with ML shown as a parallel independent branch.

**Suggested animation:** Build the pipeline left-to-right, ML branch
sliding in from below to join at Fusion.

**Estimated speaking time:** 1 minute

---

## Slide 5 — Behavioral Baseline & Anomaly Detection
**Title:** Learning What "Normal" Looks Like — Per App, Per Device

**Bullet points:**
- Running mean/standard-deviation across 12 behavioral dimensions
- Foreground/background time, session count, night usage, permission counts
- Deviation scored in standard deviations from that app's own history
- No static rulebook — the baseline is yours, not a vendor's

**Speaker notes:** "Instead of comparing your apps to some generic
rulebook, we build a statistical baseline for each app, on your device,
from your own usage. A flashlight app that suddenly starts running
overnight in the background gets flagged against *its own* history —
not someone else's assumptions."

**Suggested diagram:** A simple bell curve with a "normal" zone and an
outlier point highlighted, labeled with a real metric like "Night Usage
Time."

**Suggested animation:** Outlier point pulses/highlights in red.

**Estimated speaking time:** 1 minute

---

## Slide 6 — MITRE ATT&CK Mapping
**Title:** Speaking a Language Analysts Already Know

**Bullet points:**
- Behavioral evidence mapped to real MITRE ATT&CK for Mobile techniques
- Tactics: Persistence, Collection, Command and Control, and more
- Confidence-scored per technique, not a binary match
- Standardized vocabulary — not a proprietary black-box score

**Speaker notes:** "Rather than inventing our own threat taxonomy, we map
directly to MITRE ATT&CK for Mobile — the same framework enterprise SOC
teams already use. That means our output is immediately actionable by
anyone who already knows this standard."

**Suggested diagram:** A small ATT&CK matrix excerpt with 2-3 techniques
highlighted (e.g. T1398 Boot/Logon Init Scripts, T1437 Application Layer
Protocol).

**Suggested animation:** Highlight technique cells sequentially as
you name them.

**Estimated speaking time:** 45 seconds

---

## Slide 7 — Machine Learning Pipeline
**Title:** A Second, Independent Opinion — On-Device

**Bullet points:**
- Random Forest + XGBoost trained on behavioral features
- Cross-validated, hyperparameter-tuned, F1-optimized threshold
- Exported via knowledge distillation to a quantized TensorFlow Lite model
- Millisecond inference, fully offline, cached and lazy-loaded

**Speaker notes:** "Our rule-based engines are fully explainable by
design, but we didn't stop there — we also trained a machine learning
classifier on the same behavioral features, exported it to TensorFlow
Lite, and it runs directly on the device in single-digit milliseconds.
It's a second, independent signal feeding the same fusion engine."

**Suggested diagram:** Pipeline: CSV → Train (RF/XGBoost) → Evaluate →
Distill → TFLite → On-device inference. Include a small metrics table
(Accuracy/Precision/Recall/F1/ROC-AUC placeholders).

**Suggested animation:** Pipeline stages build left to right; metrics
table fades in last.

**Estimated speaking time:** 1 minute

---

## Slide 8 — Explainable AI
**Title:** No Black Boxes

**Bullet points:**
- Every verdict includes a natural-language explanation
- Ranked feature importance — global AND per-prediction
- Direct links to the specific evidence that drove the score
- Builds trust with both end users and enterprise security teams

**Speaker notes:** "A threat score with no explanation is just a number
nobody trusts. Every single verdict — whether from our rule engines or
our ML model — comes with a plain-English explanation and a ranked
breakdown of exactly which behaviors mattered most."

**Suggested diagram:** Screenshot mockup of the Threat Center's Feature
Importance section (horizontal bars).

**Suggested animation:** Bars grow in from left to right in importance order.

**Estimated speaking time:** 45 seconds

---

## Slide 9 — Threat Intelligence & Response
**Title:** From Detection to Action

**Bullet points:**
- Offline knowledge base of known malicious behavioral clusters
- Behavioral similarity matching — no cloud lookup required
- Automated, prioritized response playbooks
- Full chronological incident timeline for audit and review

**Speaker notes:** "Detection alone isn't enough — we match against a
bundled, offline knowledge base of known malicious patterns, then
generate a prioritized response plan: alert the user, revoke a
permission, recommend uninstall — all logged to a searchable timeline."

**Suggested diagram:** Simple 3-box flow: Match → Recommend → Log.

**Suggested animation:** Each box appears with a checkmark.

**Estimated speaking time:** 45 seconds

---

## Slide 10 — The Enterprise Dashboard
**Title:** Built Like Defender, Sized for a Phone

**Bullet points:**
- Material 3, dark/light, fully responsive (phone → tablet → desktop)
- Executive Dashboard, Threat Center, MITRE view, Behavior Analytics
- Interactive timeline, PDF/CSV reporting
- Riverpod state management, clean architecture throughout

**Speaker notes:** "All of this surfaces through a dashboard designed to
feel like an enterprise security console — Defender, Falcon, Cortex XDR
— but built mobile-first with Flutter, so it scales from a phone screen
up to a tablet or foldable without a second codebase."

**Suggested diagram:** Screenshot collage: Dashboard, Threat Center, MITRE
screen, side by side.

**Suggested animation:** Screens slide in like a carousel.

**Estimated speaking time:** 1 minute

---

## Slide 11 — Why This Wins
**Title:** Innovation + Rigor + Real-World Readiness

**Bullet points:**
- Genuinely novel: on-device behavioral ML + MITRE + explainability, combined
- Technically rigorous: verified acyclic architecture, real integration review completed
- Privacy-first: zero telemetry, fully offline, enterprise/government-viable
- Immediately demoable: full pipeline, live scan, real verdicts

**Speaker notes:** "This isn't a proof-of-concept glued together for a
demo — we performed a full integration review, found and fixed real
architectural issues, and every screen you'll see is backed by an actual
working pipeline, not a mockup."

**Suggested diagram:** Four-quadrant checklist graphic (Innovation /
Rigor / Privacy / Demo-ready), each with a checkmark.

**Suggested animation:** Checkmarks tick in one at a time.

**Estimated speaking time:** 45 seconds

---

## Slide 12 — Roadmap & Ask
**Title:** What's Next

**Bullet points:**
- Federated on-device model improvement
- Enterprise fleet-management console
- Expanded MITRE ATT&CK for Mobile technique coverage
- Ask: pilot partners, feedback, and (if applicable) funding/support to reach production

**Speaker notes:** "We're not stopping here — our roadmap includes fleet
management for enterprises and federated learning to improve the model
without ever centralizing raw data. Thank you — happy to answer
questions."

**Suggested diagram:** Simple roadmap timeline (Now → 3 months → 6 months → 12 months).

**Suggested animation:** Timeline draws left to right, ending on a
"Thank You" card.

**Estimated speaking time:** 45 seconds

---

**Total: ~11 minutes** (leaves 1-4 minutes of buffer within a typical
12-15 minute hackathon slot for setup/transition or Q&A overflow).
