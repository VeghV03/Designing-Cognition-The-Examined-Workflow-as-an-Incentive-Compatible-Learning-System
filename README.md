# Designing Cognition: The Examined Workflow as an Incentive-Compatible Learning System

**Type:** Design paper + conceptual framework + generalised template

---

## Abstract

Most personal knowledge systems fail not from poor tooling but from poor mechanism design: the behaviours they produce are not the behaviours they intend. Highlighting feels like understanding; summarising feels like encoding; having notes feels like knowing. Each is an incentive compatibility failure — a case where deviation from the desired epistemic behaviour is the dominant strategy. Generative AI makes this worse: AI assistance improves observable output while systematically degrading metacognitive accuracy (Fernandes et al. 2026, N=698; Koch 2026) and eroding the metacognitive monitoring function that would otherwise detect the gap. We present Life OS: a personal learning system designed from three intersecting theoretical frames — mechanism design (Hurwicz 1972), metacognitive monitoring theory (Nelson & Narens 1990), and zone of proximal development scaffolding (Vygotsky 1978) — to produce incentive-compatible epistemic behaviour in AI-augmented knowledge work. We describe the system's architecture, the IC/IR conditions of each component, a generalised design template, and a research agenda for empirical validation.

---

## 1. Introduction

### 1.1 The Problem with Personal Knowledge Systems

Personal knowledge management (PKM) systems are among the most discussed productivity tools of the past decade. Notion, Roam Research, Obsidian, Zettelkasten implementations — all promise to externalise knowledge in ways that compound over time. The empirical record is less flattering. Most systems are abandoned within months. The standard explanation invokes friction or discipline failure. The mechanism design explanation is more precise: the desired behaviours are not equilibria.

Consider three common PKM actions:

| Action | What the user believes | What actually happens |
|---|---|---|
| Highlighting text | "I've captured this knowledge" | Fluency illusion — re-exposure without retrieval |
| Summarising in own words | "I've processed this" | May encode surface structure, not deep structure |
| Having a notes file | "I can find this later" | Rarely consulted; no retrieval practice |

In Hurwicz's (1972) sense, each of these is an IC violation: the user has an incentive to perform the action that signals learning rather than produce learning itself. The mechanism does not penalise the deviation — it rewards it with reduced effort.

### 1.2 AI Amplifies the Problem

AI assistance adds a new dimension: it improves observable output while degrading the internal monitoring that would otherwise detect the gap. Fernandes et al. (2026) found that AI assistance improved LSAT performance by 3 points while participants overestimated their performance by 4 points (N=246+452, published *Computers in Human Behavior*). Higher AI literacy predicted *worse* self-assessment accuracy — the usual response of "just educate users" is directly contradicted. Koch (2026) formalises this as a four-variable decoupling: output quality, genuine understanding, confidence calibration, and self-assessed ability can all diverge independently.

The design challenge is therefore not "how do I take better notes" but "how do I design a system where good epistemic behaviour is the path of least resistance?"

### 1.3 Contribution

This paper makes four contributions:

1. A formal mechanism-design framing of personal knowledge systems — the first such treatment we are aware of
2. Life OS: a concrete implementation with observable IC/IR conditions for each component
3. A generalised design template for researchers and practitioners
4. A research agenda for empirical validation

---

## 2. Theoretical Background

### 2.1 Mechanism Design

A mechanism maps agent strategies to outcomes (Hurwicz 1972). A mechanism is *incentive compatible* (IC) if the desired strategy is a dominant strategy; *individually rational* (IR) if participation dominates exit. Applied to personal learning: the "outcome" is epistemic quality — accuracy, calibration, knowledge transfer. The "strategy" is the user's behaviour in a session. The mechanism is the set of protocols that structure the session.

The key result: desired epistemic behaviour must be the equilibrium of the designed system, not an aspiration. A system that makes active processing effortful and passive consumption easy has designed the wrong equilibrium.

### 2.2 Metacognition: Monitoring and Control

Nelson and Narens (1990) distinguish two metacognitive functions: *monitoring* (assessing one's own knowledge state) and *control* (adjusting strategy based on that assessment). Both are active, effortful processes. AI externalises the monitoring function: the user's confidence is now a function of the AI's output quality, not their own discriminative ability. This is why meta-d' < d' under AI assistance — the monitoring function has been delegated.

Flavell's (1979) framework adds three components: metacognitive knowledge (about self, task, and strategies), metacognitive experience (real-time awareness during a cognitive task), and metacognitive goals. A properly designed system creates metacognitive experiences that support accurate knowledge assessment, not comfortable ones.

### 2.3 Zone of Proximal Development

Vygotsky (1978) defines the ZPD as the gap between what a learner can do independently and what they can do with support. Effective scaffolding operates at the ZPD boundary — not below it (spoon-feeding, producing dependency) and not above it (confusion, producing disengagement). The critical corollary: *fading*. Scaffolding that does not decrease as competence increases produces permanent dependency, which is the dominant failure mode of AI-assisted learning.

Applied to AI: the AI must operate at the ZPD boundary and gradually reduce support as independent competence is demonstrated. An AI that always answers fully is operating below the ZPD and producing dependency rather than capability.

### 2.4 Self-Regulated Learning

Zimmerman (2000) and Pintrich (2000) describe the SRL cycle: forethought (goal-setting, planning) → performance (monitoring, strategy use) → self-reflection (evaluation, attribution). Life OS formalises the self-reflection phase as the calibration log and epistemic observation block — the component most consistently absent from existing PKM systems.

### 2.5 Why AI Changes the Stakes

Three empirical findings converge on the same conclusion:
- AI assistance improves output while degrading metacognitive accuracy (Fernandes et al. 2026)
- Higher AI literacy predicts *worse* self-assessment — knowledge about AI is not the solution
- Calibration interventions can counteract this (Ma et al. 2024) — but only if they are structurally enforced

A personal learning system used alongside AI must actively counteract metacognitive degradation. Without structural countermeasures, AI integration will systematically weaken the epistemic accuracy it appears to improve.

---

## 3. System Architecture

### 3.1 Seven Design Principles

| Principle | Theoretical ground | Implementation |
|---|---|---|
| P1: Good epistemic behaviour must be the equilibrium | IC — mechanism design | Elicitation-first; session protocols enforce prior articulation |
| P2: Scaffold at the ZPD boundary, then fade | ZPD — Vygotsky | ZPD scaffolding table; fading criterion: 3 correct independent applications |
| P3: Claims over papers | Encoding specificity; retrieval utility | CLAIMS_MAP: one declarative claim per row, not paper summaries |
| P4: Every prediction is a calibration event | SRL self-reflection; Brier scoring | Calibration log: predictions extracted per session, approved, logged |
| P5: AI externalisation must be structurally prevented | CS-C004 — Koch 2026 | 20-minute rule; AI debt ledger; bypass log |
| P6: Processing state must be visible | Information design | Pipeline done conditions; TRIAGE.md existence as processing signal |
| P7: Failure modes must be observable and logged | AI debt auditing | Cognitive Debt Ledger; bypass log; weekly review |

### 3.2 Input Layer

Five parallel intelligence agents run on a regular cadence: paper-scout (arXiv/Semantic Scholar), protocol-auditor (domain-specific protocol monitoring), citation-verifier, calendar-synthesizer (injected by main agent — sub-agents cannot access calendar APIs), and knowledge-gap-finder. Outputs land in `inbox/YYYY-MM-DD/`.

Every input type has a defined triage route with a *done condition* — a structural signal that processing has occurred. The done condition for inbox folders is the existence of `TRIAGE.md`. Without a done condition, processing is invisible and the illusion of having processed is the default state (a Type III information design failure).

Reading logs (3 minutes post-session: core thing, still unclear, connection) follow the same pattern: a brief mandatory entry prevents the illusion of having processed without actually logging.

### 3.3 Claims Layer

The CLAIMS_MAP system stores knowledge as declarative claims, not paper summaries. Each claim is in standard form: `[Actor] [does/does not] [X] [under conditions Y]`. Papers exist to support or contradict claims; claims are the primary epistemic unit.

This design choice has a structural rationale: paper summaries encourage storage and retrieval of "what did Smith say?" Claims encourage storage and retrieval of "is X true, and under what conditions?" The latter is what writing and reasoning require.

### 3.4 Session Layer

Sessions have three structural components that counteract IC violations:

**Elicitation-first:** Before any substantive output, the AI asks clarifying questions. Two functions: request precision (better-targeted output) and forced articulation (stating the problem is itself epistemic processing). This makes passive request-and-receive behaviour structurally harder than active engagement.

**ZPD scaffolding:** Five canonical situations, each with a defined scaffolding move and a defined failure mode (when to switch from scaffold to direct answer). The table is explicit: "If the learner can't answer after one scaffolding prompt, provide the answer, then explain the gap. Do not keep scaffolding past the point of productive friction."

**Metacognitive monitoring:** Trigger-based (not periodic) interventions when passive consumption is detected: 3+ agreement-only responses, sharp drop in response complexity, topic shift mid-task, prediction step skipped. Dosing rule: max 2 monitoring interventions per 30-minute block (from CS-C009 — metacognitive prompting increases cognitive load).

### 3.5 Output and Feedback Layer

Four feedback mechanisms close the SRL self-reflection loop:

1. **Epistemic observation block** (per session): demonstrated concepts, gaps surfaced, ZPD movement, AI-debt impact. This is the system's primary learning signal.
2. **Calibration log** (per session): predictions extracted from session, approved, logged. The manual precursor to Spectre's automated calibration tracking.
3. **Cognitive Debt Ledger**: known AI-dependent claims not yet independently verified; bypass violations log.
4. **Weekly review**: reading cadence, handoff coverage, calibration log movement, debt movement.

The Saturday puzzle (30 minutes, AI-free, block-aligned) provides an external validity signal: a performance output that cannot be faked by recognition or AI delegation.

---

## 4. Mechanism Analysis

### 4.1 IC Conditions by Component

| Component | Desired behaviour | IC condition | How it holds |
|---|---|---|---|
| Elicitation protocol | State understanding before receiving answer | Elicitation is required, not optional — answer is gated | Protocol enforcement |
| 20-minute rule | Independent thinking before AI assistance | Pre-commitment device; bypass is logged | Bypass log creates accountability |
| ZPD scaffolding | Engage with scaffold rather than demand answer | Scaffold is the first response; full answer requires waiting | Structural sequencing |
| Calibration log | Make falsifiable predictions | Predictions extracted from session, not self-reported | AI extracts from session transcript |
| Saturday puzzle | Produce AI-free output | 30-minute hard cap; AI-free by design | Structural constraint |

### 4.2 Common IC Violations and Mitigations

The four most common failure modes, their mechanism type, and structural mitigations:

| Failure | Type | Mitigation |
|---|---|---|
| Passive consumption — agreeing without processing | Type III (false belief of understanding) | Metacognitive monitoring triggers; "restate in your own words" prompt |
| Bypass accumulation — 20-minute rule never enforced | Type I IC violation (deviation is easier) | Bypass log; weekly review accountability check |
| ZPD drift — AI operates below ZPD indefinitely | Type IV (wrong cognitive load) | Fading protocol; epistemic observation blocks track movement |
| Calibration stagnation — no predictions made | IR failure (system not producing value) | Session start prompts: "what do you expect the answer to be?" before any analysis |

### 4.3 The 20-Minute Rule as a Commitment Device

A commitment device (Elster 1979; O'Donoghue & Rabin 1999) binds future self to a constraint the present self prefers but predicts will be violated. The 20-minute rule is precisely this: in the moment, asking Claude is the dominant strategy (faster, less effortful, higher immediate quality). The rule makes independent thinking the required first step, enforced by social accountability (bypass log is visible at weekly review).

The rule fails if it becomes nominal — logged as "done" without genuine independent work. The diagnostic: does the "what I found" answer to the elicitation question actually reflect independent thinking? The ZPD scaffolding steps (1-2 diagnostic questions after "I've thought about this") probe this.

---

## 5. Design Template

The minimal viable Life OS requires three components. Start here; add complexity only when the minimal version is working.

**Component 1: Inbox → Triage → Claims**

Define at least two knowledge streams relevant to your work (e.g., a domain of theory + a domain of practice). For each, create a CLAIMS_MAP file with the standard schema. Set up a weekly intake ritual: new inputs → extract claims → update the map. The done condition (TRIAGE.md or equivalent) makes processing state visible.

**Component 2: Session scaffolding**

Two rules only:
1. State your expectation before receiving any analysis: "I expect X because Y." Even one sentence.
2. After every session touching theory, write one sentence: "The most important thing I just processed is ___." If you can't complete it, you haven't processed.

**Component 3: Calibration feedback**

After any session where you formed a belief, write: "I believe X. I'll know I was wrong if Y." This is the minimal Brier seed. Review these after 2-4 weeks and note which ones you can now evaluate.

**Failure mode table for new implementers:**

| Week | Common failure | Warning sign | Fix |
|---|---|---|---|
| 1-2 | Too much system, too little use | Building tools instead of using them | 20-minute hard cap on setup; start the intake ritual immediately |
| 3-4 | Claims accumulate, nothing feeds writing | CLAIMS_MAP grows but is never queried | One writing query per session: "what does the corpus say about X?" |
| 5-8 | Scaffolding collapses into Q&A | Elicitation questions answered without thinking | Re-enforce the prediction step; log bypasses |

---

## 6. Research Agenda

Six empirical questions the system raises but cannot answer:

1. **Does ZPD-calibrated scaffolding reduce AI dependency over time?** Prediction: bypass rate decreases across blocks as ZPD boundary moves. Observable: bypass log + AI debt ledger movement.

2. **Does the 20-minute rule actually improve calibration?** Prediction: users who complete independent thinking before AI consultation show better Brier scores at block end. Testable with calibration log data.

3. **What is the optimal fading threshold?** Current: 3 correct independent applications. Is this correct, or domain-dependent?

4. **Does the claims-centric corpus produce better retrieval for writing?** Prediction: users with CLAIMS_MAP can locate a supporting claim faster than users with paper summaries. Testable with a retrieval task.

5. **Does metacognitive monitoring dosing matter?** CS-C009 suggests max 2 interventions per 30 minutes. Does violating this actually degrade performance? Testable with session quality signals.

6. **Can Life OS counteract the CS-C004 metacognitive decoupling failure?** Primary research question: measure M-ratio before and after 8 weeks of structured Life OS use vs. unstructured AI assistance. This would be the first direct empirical test of the system's core design claim.

---

## 7. Conclusion

The core insight is that a personal learning system is a mechanism. The question is not "how do I take better notes" but "is the behaviour I want an equilibrium of this system?" Most PKM systems fail because they never ask this question. AI integration makes the failure more acute — better-looking outputs mask degraded metacognitive accuracy, and the usual epistemic safety nets (feeling confused, noticing gaps) stop firing.

Life OS is one implementation. Section 5 is the generalisation. Neither is complete — the research agenda in Section 6 is the honest statement of what remains empirically unestablished. What is established: the theoretical argument that these three frames (mechanism design, metacognitive monitoring, ZPD) compose into a coherent design rationale, and that this rationale is implementable, observable, and empirically testable.
