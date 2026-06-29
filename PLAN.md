# first-aid-open — Open, Illustrated First-Aid Guides Aligned to Official Guidance

> **Status:** Draft · **Version:** 0.1.0 · **Last updated:** 2026-06-28 ·
> **Owner:** TBD (maintainer) · **Lane:** donated · **Risk tier:** HIGH (safety-critical, medical)

> **Positioning:** The open, plain-language, illustrated first-aid library that *teaches the
> official answer* — every step paraphrased from and cited to recognised authorities (ILCOR/
> resuscitation councils, WHO, IFRC/national Red Cross & Red Crescent societies), reviewed and
> signed off by credentialed clinicians before it ships, and framed unmistakably as **information,
> not a substitute for professional care or hands-on training.** Freely reusable (CC BY-SA),
> offline-capable, accessible, and translatable — so the right first action is available to anyone,
> in any language, with or without a connection.

> **In one line:** *Authoritative first-aid knowledge is locked behind paywalls, copyright, and
> course fees; first-aid-open turns the public, official consensus into a free, illustrated,
> expert-verified library that anyone can read, print, translate, and trust — without ever
> pretending to replace a real responder or a real course.*

---

## Constraints as identity

This is a HIGH-risk, safety-critical medical project. Its constraints are not friction to be
engineered away — they **are** the product. A first-aid guide that is fast but wrong can kill.
The following five refusals define what first-aid-open *is*:

1. **Nothing ships without credentialed-clinician sign-off.** No "delivered" deed, ever, bypasses
   the expert review gate. AI drafts; humans with medical credentials verify; only then does it
   ship. This is non-negotiable and enforced in tooling, not just policy.
2. **We paraphrase and cite the official consensus; we never invent it, and never copy it.** Every
   clinical claim traces to a named, current, authoritative source. No copyrighted text, no
   copyrighted illustrations, no trademarked logos.
3. **We are explicit about what we are not.** Every page carries clear "informational only — not a
   substitute for professional medical care or accredited training; in an emergency call your local
   emergency number" framing. We do not diagnose, prescribe, or replace a course.
4. **We track currency aggressively.** Guidelines change (e.g. the ILCOR/CPR cycle). Stale
   life-critical content is a safety defect, not tech debt. Every page has a review-by date and a
   source-version stamp.
5. **We localise meaning, not just words.** Emergency numbers, drugs, and procedures differ by
   region. We never blindly translate a US dosage or "call 911" into a context where it is wrong.

A project that promises "first aid for everything, instantly" promises something dangerous.
first-aid-open promises a *narrow, deep, verified, current* core — done to a clinical standard.

---

## 1. Executive summary

first-aid-open produces a library of **open-licensed, illustrated, plain-language first-aid
guides** for common life-threatening and common-injury scenarios (e.g. CPR, choking, severe
bleeding, anaphylaxis, burns, recovery position, stroke/heart-attack recognition). Each guide
**paraphrases and cites** current guidance from recognised authorities — the International Liaison
Committee on Resuscitation (ILCOR) and its member councils (AHA, ERC, Resuscitation Council UK,
etc.), the World Health Organization (WHO), and the International Federation of Red Cross and Red
Crescent Societies (IFRC) / national societies — and is **reviewed and signed off by credentialed
clinicians** before it is published.

The output is built as a structured content repository: source-cited Markdown/MDX guides, an
original (non-infringing) illustration set, machine-readable provenance and review metadata, and
print/offline/web renderings. Code is **MIT**; content is **CC BY-SA 4.0** (share-alike to keep
derivatives open, with attribution to first-aid-open and acknowledgement that guidance derives from
the cited authorities).

This is the highest-risk tier Elyos defines. Accordingly the plan front-loads three gates —
**provenance**, **clinical expert sign-off**, and **currency/freshness** — into the pipeline and
the Definition of Shipped. It does **not** assume a partner is in place: a clinical reviewer pool, a
medical advisory steward, and any distribution partner are all marked **TO BE SECURED**, and **no
guide may be marked `delivered`/`done` until at least one credentialed reviewer is secured and signs
off.** Until then the project can do non-clinical foundation work (schema, tooling, source registry,
guardrail framing, illustration system) but **cannot ship clinical content**.

---

## 2. Problem & beneficiaries

**The problem.** When a person collapses, chokes, bleeds heavily, or has an anaphylactic reaction,
the first few minutes — usually before professionals arrive — decide the outcome. Bystander CPR
roughly doubles survival from out-of-hospital cardiac arrest, yet most bystanders do nothing,
often because they do not know what to do or fear doing it wrong. The *correct* first action is
not secret — it is published consensus — but it is fragmented across:

- **Paywalled courses and copyrighted manuals** (good, but cost/access-limited and not reusable).
- **Copyrighted webpages** that cannot be legally re-hosted, printed at scale, or translated.
- **Unsourced, contradictory, or outdated web content** (the dangerous default a panicked person
  finds via search), including AI-generated content with no provenance or review.

The gap is a **free, trustworthy, reusable, current, illustrated, translatable** layer that states
the official first action plainly and cites where it comes from — without copying anyone's
copyrighted material and without pretending to be a substitute for training or professional care.

**Who is helped (beneficiaries).**

- **Lay bystanders / the general public** — the primary beneficiary: someone who needs the right
  first action *now*, possibly offline, possibly not a native speaker of the dominant local language.
- **Community educators, CERT/disaster-prep groups, schools, NGOs, clinics in low-resource
  settings** — who need printable, translatable, freely-licensed material they can legally
  distribute (today they often cannot reuse copyrighted manuals).
- **Translators and accessibility projects** within Elyos (e.g. `vital-info-translations`,
  `emergency-phrasebooks`, `easy-read-plus`) — who need a clean, source-cited English base to
  derive from.
- **Downstream Elyos projects** — `proper-prepper` (disaster-prep toolkit) and
  `community-resource-maps` can embed verified guides.

**Verified need:** **TO BE SECURED.** The *general* need is well-evidenced (bystander-intervention
survival data, WHO/IFRC emphasis on first-aid access). However, a **specific named requestor or
partner organisation** that has asked for this deliverable and will help validate and distribute it
**does not yet exist** and must be secured. All Task JSON for clinical deliverables therefore carry
`verifiedNeed: false` until a partner (e.g. a national first-aid NGO, a community-health
organisation, or a low-resource-setting clinic network) confirms the need and target scope. Do not
overstate demand: we have a strong *general* case, not yet a *specific committed* one.

**Partner / requestor:** **TO BE SECURED** — see §11. Candidate categories: a national Red Cross/
Red Crescent society or community-first-aid NGO; a global-health education nonprofit; an Elyos
sibling project acting as internal requestor (`proper-prepper`).

---

## 3. Goals and non-goals

**Goals**

- **G1 — A small, deep, verified core.** Ship a high-quality core of the highest-impact scenarios,
  each paraphrased from and cited to current official guidance, illustrated, and **clinician-signed-
  off**, before broadening.
- **G2 — Provenance you can audit.** Every clinical claim links to a named, dated, versioned
  authoritative source; the chain is machine-readable and publicly inspectable.
- **G3 — Unmistakable safety framing.** Every artifact states it is informational, not a substitute
  for professional care/training, and tells the reader to call local emergency services.
- **G4 — Genuinely reusable & accessible.** CC BY-SA content, original illustrations, offline/print
  renderings, WCAG-conscious, structured for translation (the strings/structure are i18n-ready).
- **G5 — Currency by design.** Each guide carries a source-version stamp and a review-by date; a
  freshness process flags guides when their upstream guidance changes (e.g. a new ILCOR cycle).
- **G6 — A reusable safety-content pipeline.** The schema, provenance model, review gate, and
  guardrail framing become a template other HIGH-risk Elyos health projects can adopt.

**Non-goals (explicit)**

- **NG1 — Not a replacement for training or certification.** We do not certify anyone, issue course
  credit, or claim to make the reader competent. We point people *to* accredited courses.
- **NG2 — Not clinical/medical advice for an individual.** No diagnosis, no triage of a specific
  person's specific situation, no prescribing, no dosing tailored to an individual.
- **NG3 — Not a comprehensive medical encyclopedia.** Not wilderness/tactical/advanced-provider
  medicine, not chronic-disease management, not drug references. A bounded first-aid core only.
- **NG4 — No copying of copyrighted material.** We never reproduce AHA/ERC/Red Cross manual text,
  figures, photographs, or logos. Paraphrase + cite only; original illustrations only.
- **NG5 — Not an authority itself.** We are a faithful, cited *secondary* presentation of official
  consensus. Where authorities disagree or guidance is regional, we surface that — we do not
  adjudicate or invent a "first-aid-open recommendation."
- **NG6 — No unverified shipping.** We never publish clinical content that has not passed expert
  sign-off, however small or "obvious." There is no fast lane for life-critical content.
- **NG7 — No region-blind content.** We do not ship a single global guide that hard-codes one
  region's emergency number or drug name as if universal.

---

## 4. Success metrics (outcomes)

Outcome-based and beneficiary-centric, not vanity counts. "Guides published" is an output, not an
outcome; it appears only as a capacity indicator.

| # | Outcome metric | Baseline | Target (12 mo) | How measured |
|---|---|---|---|---|
| O1 | Verified core guides **shipped with full expert sign-off** | 0 | 8–12 core scenarios | Review-gate records (signed-off count) |
| O2 | Clinical claims with complete, current provenance | n/a | 100% (hard gate) | Automated provenance lint; 0 unsourced claims permitted |
| O3 | Guides past expert sign-off **with named credentialed reviewer recorded** | 0 | 100% of shipped | Sign-off ledger entries |
| O4 | Reuse by beneficiaries (orgs/projects that adopt or redistribute) | 0 | ≥3 confirmed adopters (e.g. an NGO, a school, an Elyos sibling) | Adoption log / partner confirmation |
| O5 | Translations derived from the base (meaning-localised, re-reviewed) | 0 | ≥2 languages with regional review | Linked translation deeds w/ regional sign-off |
| O6 | Freshness: shipped guides within their review-by window | n/a | 100% (else auto-flagged & un-published) | Freshness job; stale = safety incident |
| O7 | Accessibility conformance of published renderings | n/a | WCAG 2.2 AA checks pass; print + offline render verified | a11y CI + manual audit |
| O8 | Safety-framing presence | n/a | 100% of artifacts carry the "not a substitute" + call-emergency framing | Render lint (build fails without it) |
| O9 | Correctness incidents post-publication (errata) | n/a | 0 critical; any → published erratum + root-cause within 7 days | Errata log |

> **Honest caveat.** True end-outcome (lives/health improved by a bystander acting correctly) is
> not directly attributable to a document and we will **not** claim it. We measure the proxies we
> can defend: verified-correct, current, accessible, reusable content actually adopted by
> beneficiaries. Any survival/impact statements would require a partner-run study and are out of
> scope to claim.

---

## 5. Scope

**In scope**

- A bounded **core scenario set** (initial candidates, subject to clinical-steward prioritisation):
  adult CPR + AED use, infant/child CPR, choking (adult & infant), severe external bleeding,
  anaphylaxis (recognition + epinephrine auto-injector use per official guidance), recovery
  position, recognising stroke (FAST) and heart attack, burns/scalds, seizure care, shock,
  hypothermia/heatstroke recognition. **Final list and order set by the clinical steward.**
- **Paraphrase-and-cite** authoring from official sources; an auditable provenance record per claim.
- An **original illustration system** (non-infringing): commissioned/AI-assisted-then-human-redrawn
  diagrams, abstract/inclusive figures, no traced copyrighted images, no logos.
- **Renderings:** accessible web (static), print-ready PDF, and an **offline** bundle.
- **i18n-readiness:** content structured/stringified so translation deeds can derive cleanly
  (translation itself is partly delegated to sibling projects, with regional re-review — see §3 NG7).
- **Machine-readable metadata:** schema for sources, claim→source links, review/sign-off records,
  source-version stamps, review-by dates, region applicability.
- A reusable **safety-content pipeline & guardrail template** (§3 G6).

**Out of scope**

- Diagnosis/triage/treatment of a specific individual (NG2); certification/credentialing (NG1).
- Advanced/provider-level, wilderness, tactical, veterinary, or chronic-care content (NG3).
- Drug dosing references / a pharmacopeia; pediatric weight-based dosing calculators.
- Reproducing or re-hosting any copyrighted manual text, figure, photo, or trademarked logo (NG4).
- Original clinical research, novel recommendations, or adjudicating between authorities (NG5).
- Telling a specific person what to do in a live emergency (we are static reference, not a hotline).
- Auto-publishing translations without regional clinical/contextual re-review (NG7).
- Any collection of person-level/PII data about users (see §14).

---

## 6. Solution approach & architecture

A **content-and-pipeline** project (not a runtime service). The "architecture" is the authoring
pipeline, the content schema, the gates, and the renderers.

**6.1 Content pipeline (authoring → verified publication)**

```
 source registry         draft (AI-assisted)        clinical review gate        render & publish
 ┌───────────────┐  →   ┌──────────────────┐   →   ┌────────────────────┐  →  ┌──────────────────┐
 │ authoritative │      │ paraphrase + per- │       │ credentialed       │     │ web / print PDF / │
 │ sources w/    │      │ claim citations,  │       │ clinician sign-off │     │ offline bundle;   │
 │ version+date  │      │ illustrations,    │       │ + provenance +     │     │ provenance + a11y │
 │ (registry)    │      │ safety framing    │       │ currency checks    │     │ + framing lints   │
 └───────────────┘      └──────────────────┘       └────────────────────┘     └──────────────────┘
        ▲                                                    │ fail → back to draft (never ships)
        └──────────────── freshness watcher (re-opens guides when upstream guidance changes) ───────┘
```

**6.2 Components**

- **Source registry** (`/sources/*.yaml`): each authoritative source with publisher, title, URL,
  publication/version date, guideline cycle, license/terms-of-use note, and access date. The single
  source of truth for provenance.
- **Guide authoring format** (MDX + YAML frontmatter): the guide body plus structured metadata —
  per-claim source references, region applicability, review-by date, source-version stamp,
  reviewer/sign-off record, and the mandatory safety-framing block.
- **Provenance & claim-linking schema** (`packages/schema`-style JSON Schema): validates that every
  clinical claim references at least one current source in the registry; build fails otherwise.
- **Illustration system**: an originals-only asset library with per-asset provenance
  (author/method/license) and a "no traced/copyrighted source" attestation per asset.
- **Review-gate tooling**: encodes the sign-off workflow — a guide cannot reach `delivered`/`done`
  without a recorded credentialed-reviewer sign-off (name/credential/date/scope) stored in metadata
  and verified in CI.
- **Renderers**: static web (e.g. Astro/Eleventy or Next static export), print PDF, offline bundle
  (service-worker / downloadable archive). All renderers inject the safety framing and fail the
  build if it is missing.
- **Freshness watcher**: scheduled check comparing each guide's source-version stamp / review-by
  date against the registry and upstream guideline cycles; opens a maintenance task and **flags the
  guide as "verify currency"** (and can auto-unpublish past the hard expiry).

**6.3 Tech stack**

- TypeScript, ESM, pnpm workspaces (per Elyos conventions).
- Content: MDX + YAML frontmatter; JSON Schema (Ajv) for metadata validation (mirrors the existing
  `packages/schema` approach).
- Static site generator (decision in M0; lean toward Astro/Eleventy for static, accessible,
  offline-friendly output). PDF via a headless-render or a Markdown→PDF toolchain.
- CI: `pnpm build && pnpm test && pnpm lint` plus custom gates (provenance lint, framing lint,
  a11y check, sign-off check, freshness check).
- No backend, no database, no telemetry, no user accounts (see §14).

**6.4 Key decisions (locked)**

- **D1 — Paraphrase + cite, never copy.** Original prose and original illustrations only.
- **D2 — CC BY-SA 4.0 for content, MIT for code.** Share-alike keeps derivatives open; attribution
  required; the cited authorities are acknowledged as the source of guidance (not as endorsers).
- **D3 — Hard expert-sign-off gate in tooling.** Enforced in CI/metadata, not just in process docs.
- **D4 — Region-aware content.** Emergency numbers, drug names, and regionally-varying procedures
  are explicit fields, never hard-coded as universal.
- **D5 — Currency is a build gate.** A guide past its review-by date is treated as broken.
- **D6 — Narrow-and-deep before broad.** Quality bar over coverage; the core ships fully verified
  before expansion.
- **D7 — Authorities are not endorsers.** We cite them as sources; we never imply they reviewed,
  approved, or partnered with us unless a formal agreement exists.

---

## 7. Data, licensing & compliance  *(CRITICAL — conservative by default)*

This section governs whether the project is legal and ethical to ship. When in doubt, **stop and
escalate** (per CLAUDE.md).

**7.1 Sources & their status**

| Source | Use | Copyright / terms posture | Our handling |
|---|---|---|---|
| ILCOR & member councils (AHA, ERC, RC-UK, etc.) — CoSTR, guidelines | Clinical consensus for steps | Guidelines/manuals are **copyrighted**; many summaries are freely *readable* but **not freely re-licensable** | **Paraphrase facts + cite**; never copy text/figures/logos. Facts/procedures aren't copyrightable; specific expression is. |
| WHO publications | Some first-aid-relevant guidance | Often **CC BY-NC-SA 3.0 IGO** (note: **NC** — non-commercial) | Cite; if quoting/adapting WHO expression, comply with its NC/SA terms and **flag the NC tension** with our CC BY-SA output (see 7.4). Prefer paraphrase to avoid NC contamination. |
| IFRC / national Red Cross & Red Crescent first-aid guidance | First-aid practice consensus | **Copyrighted**; "Red Cross"/red-cross emblem are **protected** (Geneva Conventions + trademark) | Paraphrase + cite; **never** use the emblem, the name as a logo, or imply endorsement. Emblem misuse is a legal/IHL issue, not just trademark. |
| Government health agencies (e.g. NHS, CDC, state EMS) | Regional specifics (numbers, services) | Mixed; some Crown copyright / OGL, some US-gov public domain | Per-source license note in registry; prefer PD/open-licensed; paraphrase otherwise. |

**7.2 Provenance model**

- Every clinical claim → ≥1 registry source with publisher, title, URL, version/publication date,
  guideline cycle, and access date. Enforced by provenance lint (build fails on any unsourced
  clinical claim).
- Each source carries an explicit **license/terms note** and a **"reuse posture"** field
  (paraphrase-only vs. open-licensed-adaptable). Default posture: **paraphrase-only**.
- Each guide stores a **source-version stamp** (which guideline cycle/edition it reflects) and a
  **review-by date**.

**7.3 Illustrations & emblems**

- Originals only; per-asset provenance + a "not traced from / not a derivative of any copyrighted
  image" attestation. AI-assisted drafts must be human-redrawn/verified and attested.
- **No protected emblems** (red cross, red crescent, red crystal), **no organisation logos**, **no
  brand names used as marks**. Generic, inclusive, non-infringing depictions only.
- Illustrations depicting procedures are themselves **clinical content** and pass the same expert
  sign-off (a wrong hand position in a diagram is a safety defect).

**7.4 Licensing decision & the NC tension**

- **Code:** MIT. **Content & illustrations:** CC BY-SA 4.0.
- **Risk:** WHO material is frequently **CC BY-NC-SA** (non-commercial). CC BY-SA 4.0 (which permits
  commercial reuse) is **incompatible** with incorporating NC-licensed *expression*. Mitigation:
  rely on **paraphrased facts** (uncopyrightable) from WHO rather than adapting its text/figures; if
  any WHO expression must be adapted, that artifact is segregated and carries the NC terms — and the
  **legal/license reviewer must approve** before ship. This is an **open question for the steward**
  (see §16, OQ-2).

**7.5 Privacy / PII**

- The project collects **no person-level data**: no user accounts, no analytics that identify
  individuals, no submitted personal health information. Illustrations depict no real identifiable
  people. (See §14.)

**7.6 Attribution & "not endorsed" notice**

- Each guide attributes first-aid-open (CC BY-SA) and lists its cited authorities **as sources of
  the underlying guidance**, with an explicit notice: *"Cited organisations are the source of the
  underlying guidance; they have not reviewed, endorsed, or partnered with this material unless
  stated."* (Removes any false-endorsement implication — D7.)

---

## 8. Quality, review & risk gates

**Risk tier: HIGH** (health/safety; per good-deed-definition.md → **credentialed expert sign-off
required before merge/ship**). This is the spine of the project.

**8.1 The gates (all must pass for a clinical deed to ship)**

1. **Provenance gate** — 100% of clinical claims cite a current registry source; no unsourced
   claims; sources within their currency window. (Automated lint.)
2. **Safety-framing gate** — the "informational only / not a substitute for professional care or
   training / call your local emergency number" block + region applicability are present in every
   rendering. (Automated lint; build fails without it.)
3. **Clinical expert sign-off gate (mandatory, human).** A **credentialed reviewer** (see §11 —
   e.g. physician, registered nurse, paramedic, or accredited first-aid instructor, appropriate to
   the scenario) reviews the *content and the illustrations*, and records a sign-off
   (name, credential, date, scope, source-cycle verified) in the guide metadata. **No sign-off →
   no ship. No exceptions, no fast lane.**
4. **License/IP gate** — illustration provenance attestations present; no copyrighted text/figures/
   logos/emblems; license compatibility confirmed (incl. the WHO-NC check). Legal/license reviewer
   approves anything non-paraphrase.
5. **Accessibility gate** — WCAG 2.2 AA checks pass; print + offline renderings verified; plain-
   language readability check.
6. **Currency gate** — source-version stamp + review-by date present and in-window.

**8.2 Definition of Shipped (per guide)**

> A guide is **Shipped** when: acceptance criteria met **and** CI green (build/test/lint) **and**
> all six gates pass **and** a named credentialed reviewer's sign-off is recorded in metadata
> **and** (per the verifiedNeed rule) a partner/requestor has confirmed need or it is explicitly
> handed to a beneficiary/sibling project **and** it is published in web + print + offline form
> with provenance and framing intact. "Delivered, not merged."

**8.3 Reviewer independence & dual control**

- The clinician who signs off must **not** be the same agent/person who authored the draft.
- For the highest-stakes scenarios (CPR, anaphylaxis, severe bleeding, infant/child), require
  **two independent credentialed sign-offs** (dual control), or one clinician + one accredited
  instructor.
- Disagreements between reviewers are resolved by the **clinical steward** (§11) and logged.

**8.4 Errata & incident response**

- A public **errata log**; any reported clinical error triggers immediate review and, if confirmed,
  **un-publish or correct within a defined SLA** (critical: same-day flag, 7-day root-cause).
- A correctness incident is a **safety incident**, handled with the same seriousness as a security
  incident in software.

---

## 9. Roadmap & milestones

Phased; each milestone has a measurable **exit criterion**. M0 is a thin, **non-clinical**
foundation that can proceed **before** a reviewer/partner is secured; **clinical content cannot
ship until M2's reviewer pool exists.**

| Phase | Goal | Exit criteria (measurable) |
|---|---|---|
| **M0 — Foundation & guardrails (non-clinical)** | Stand up the repo, schema, source registry, guardrail framing, illustration system, and the CI gates — *without shipping any clinical claim.* | Repo builds; Task/guide + source + provenance + sign-off **schemas** defined & validated; provenance/framing/a11y/sign-off **lint gates** implemented and failing-closed; safety-framing template ratified; illustration provenance process defined; **1 non-clinical pilot page** (e.g. "how to use this library / call your local emergency number") renders to web+print+offline and passes all *non-clinical* gates. **No clinical content shipped.** |
| **M1 — One verified guide (vertical slice)** | Prove the full pipeline end-to-end on **one** scenario, drafted and gate-ready, *pending* reviewer. | One core guide (steward-chosen, e.g. severe bleeding or adult CPR) fully drafted with complete provenance, original illustrations, framing, region fields; passes all **automated** gates; sits in `review` **blocked on the human sign-off gate**. Demonstrates the gate correctly **refuses to ship** unsigned content. |
| **M2 — Reviewer pool & first SHIPPED guide** | Secure ≥1 credentialed reviewer; ship the first fully signed-off guide. | ≥1 credentialed clinical reviewer **secured** and onboarded (COI + scope recorded); the M1 guide receives recorded sign-off(s) (dual control for top-tier scenarios) and is **Shipped** per §8.2 in web+print+offline; sign-off ledger live. *(This is the first true "deed delivered.")* |
| **M3 — Core library** | Ship the 8–12-scenario verified core. | ≥8 core scenarios Shipped with full sign-off; freshness watcher live and flagging; ≥1 confirmed external/sibling adopter (O4). |
| **M4 — Reach: i18n, accessibility depth, partner distribution** | Make the verified core reusable across languages and channels with regional re-review. | ≥2 languages derived **with regional clinical/contextual re-review** (not raw MT); accessibility audit (AA) passed across renderings; a distribution partner or sibling-project integration confirmed; freshness SLA met (O6=100%). |
| **M5 — Sustainability & template** | Hand off to durable maintenance; publish the reusable safety-content pipeline template. | Maintenance rota + review-by cadence operating; ≥1 review-cycle refresh completed on a shipped guide; pipeline/guardrail template documented for reuse by other HIGH-risk Elyos health projects; outcome metrics (O1–O9) reported. |

**Dependencies / sequencing:** M0→M1 are agent-doable now (donated lane, no reviewer needed to
*draft*). **M2 gates everything clinical** and depends on securing a credentialed reviewer (the
critical-path human dependency). M4 depends on M3 core + translation siblings + regional reviewers.

---

## 10. Work breakdown

The itemised, schema-mapped backlog lives in **`TASKS.md`**, organised by the M0–M5 milestones
above. Each task maps to an Elyos Task JSON (§ schema), carries a `riskTier`, an explicit reviewer,
and — for all clinical deliverables — `verifiedNeed: false` until a partner is secured and the
clinical sign-off gate is satisfied. TASKS.md contains milestone task tables, acceptance criteria
for the key tasks, per-milestone Definitions of Done, a backlog, and a schema-valid example Task
JSON for the first M0 task.

---

## 11. Governance, roles & stakeholders

| Role | Who | Status | Responsibility |
|---|---|---|---|
| **Maintainer** | TBD | **TO BE SECURED** | Owns the repo, schema, CI gates, releases; ensures no clinical content ships unsigned. |
| **Clinical steward (medical advisory owner)** | TBD — must be a senior credentialed clinician (e.g. EM physician / paramedic lead) | **TO BE SECURED (critical)** | Sets/approves the scenario list & priority, arbitrates reviewer disagreements, owns the clinical quality bar and currency cadence. *The project should not ship clinical content without this role filled.* |
| **Credentialed reviewer pool** | TBD — physicians, RNs, paramedics, accredited first-aid instructors | **TO BE SECURED (critical)** | Perform the mandatory sign-off gate; verify content + illustrations + source currency; record sign-off. Rotation to avoid single-reviewer bias/fatigue. |
| **License/IP reviewer** | TBD (may be Elyos-shared) | **TO BE SECURED** | Approves license posture, WHO-NC checks, illustration/emblem attestations. |
| **Accessibility reviewer** | TBD (may be Elyos-shared, e.g. `a11y-alttext-commons`) | TBD | Verifies WCAG/print/offline/plain-language. |
| **Steward (last-mile / distribution)** | TBD partner or sibling-project owner | **TO BE SECURED** | Ensures shipped guides actually reach beneficiaries; owns the adoption log. |
| **Partner / requestor** | TBD — first-aid NGO / community-health org / Elyos sibling | **TO BE SECURED** | Confirms the specific need (flips `verifiedNeed`), validates scope, distributes. |
| **Regional reviewers (per locale)** | TBD per language/region | TO BE SECURED at M4 | Re-review translations for regional correctness (numbers/drugs/procedures). |

> **Conflict of interest:** reviewers and stewards record affiliations; anyone with a commercial
> first-aid-training conflict is disclosed and may be recused per the Elyos COI/veto checklist.

---

## 12. Dependencies & integrations

- **Authoritative sources** (read/cite only): ILCOR & councils, WHO, IFRC/national societies, govt
  health agencies. Dependency risk: guidelines change on cycles → handled by the freshness watcher.
- **Elyos pieces:** Task schema (`packages/schema`), CLI workspace/PR flow (donated lane), registry,
  governance/COI process, CI/governance workflows.
- **Sibling Elyos projects:** `vital-info-translations` / `emergency-phrasebooks` (translation),
  `a11y-alttext-commons` (alt-text/accessibility), `proper-prepper` (embeds guides; candidate
  internal requestor), `easy-read-plus` (plain/dyslexia-friendly versions),
  `community-resource-maps` (distribution).
- **Tooling:** static site generator (TBD M0), PDF renderer, Ajv schema validation, a11y checker,
  CI runner. No external runtime services; no databases; no third-party telemetry.
- **Human dependency (critical path):** the credentialed reviewer pool (§11) — the single most
  important external dependency; clinical shipping is blocked until secured.

---

## 13. Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Clinically wrong content reaches a user (harm) | Low (post-gate) / High (if gate bypassed) | Critical (life-safety) | Mandatory dual-control expert sign-off enforced in tooling; no fast lane; errata SLA; dual review for top-tier scenarios | Clinical steward |
| Shipping clinical content **before** a reviewer is secured | Medium | Critical | Hard tooling gate fails-closed; M2 explicitly gates all clinical ship; `verifiedNeed:false` + status capped at `review` until sign-off | Maintainer |
| Copyright/figure/text infringement from a source | Medium | High (legal + reputational) | Paraphrase-only default; illustration originals + attestations; license/IP review gate | License/IP reviewer |
| Red Cross/Red Crescent **emblem** misuse (IHL-protected) | Medium | High | Explicit ban on emblems/logos/marks; lint + review check; no implied endorsement | License/IP reviewer |
| WHO **NC** license contaminates CC BY-SA output | Medium | Medium–High | Rely on paraphrased facts; segregate/flag any adapted NC expression; legal approval required | License/IP reviewer |
| Stale guidance after a guideline cycle change | High (over time) | High | Source-version stamp + review-by dates; freshness watcher auto-flags/unpublishes; review cadence | Clinical steward |
| Region-blind content (wrong emergency number/drug) | Medium | High | Region fields mandatory; no universal hard-coding; regional re-review for locales | Clinical steward |
| Implying official endorsement/partnership | Medium | Medium–High | "Not endorsed" notice (D7); never use names as marks; only claim partnership if formalised | Maintainer |
| False sense of competence (reader skips training) | Medium | Medium | Prominent "not a substitute for training; take a course" framing; link to accredited courses | Clinical steward |
| Reviewer scarcity / bottleneck stalls shipping | High | High | Recruit a pool early; rotation; partner with NGO/training bodies; size scope to reviewer capacity | Maintainer |
| No partner/verified need → low real-world adoption | High (currently) | Medium | Secure partner before scaling; internal sibling requestor as interim; honest `verifiedNeed:false` | Steward (last-mile) |
| AI draft hallucinates a plausible-but-wrong step | Medium | Critical | Provenance lint (every claim sourced) + human clinical sign-off catch; authors flag uncertainty | Clinical steward |
| Translation drift introduces clinical error | Medium | High | Regional clinical re-review mandatory; never auto-publish MT (NG7) | Regional reviewers |

---

## 14. Security & privacy

- **Threat surface** is small by design: a static content repo with no backend, no accounts, no DB.
  Main surfaces are (a) the repo/CI supply chain and (b) content integrity (malicious or accidental
  introduction of wrong steps).
- **No PII / no person-level data.** No user accounts, no health data collection, no
  individual-identifying analytics. If any usage analytics are ever added, they must be
  privacy-preserving and aggregate-only — default is **none**. Illustrations depict no real
  identifiable individuals.
- **Secrets:** none required for the donated lane; no API keys or tokens in logs, receipts, or
  committed files (CLAUDE.md). Any funded-lane drafting runs under a hard per-task budget cap via
  `packages/runner` and writes no secrets.
- **Content integrity / abuse:** signed-off content is the trusted state; CI gates + branch
  protection + required reviews prevent unsigned/unsourced content reaching publication. The
  sign-off ledger is auditable. Tampering with a sign-off record is treated as a security incident.
- **Misuse prevention:** scope refuses weaponisable/harm content (per CLAUDE.md refusal
  guardrails); first-aid scope is inherently protective, but we still refuse e.g. requests to frame
  content as a substitute for emergency services or to remove safety framing.
- **Supply chain:** pinned deps, lockfile, minimal dependencies, CI on PRs.

---

## 15. Sustainability & maintenance

- **Currency is the maintenance core.** Each guide has a review-by date tied to its source's
  guideline cycle; the freshness watcher opens maintenance tasks and flags/unpublishes stale guides.
  Funding a guide once is not enough — life-critical content must be *kept* current.
- **Maintenance rota:** maintainer + clinical steward run a recurring review cadence; reviewer pool
  rotation prevents fatigue/bias. Re-reviews are first-class deeds (`maintenance` tasks).
- **Outcome tracking:** O1–O9 reported per release; adoption log records real beneficiaries/orgs;
  errata log tracks correctness over time.
- **Handoff:** the reusable pipeline + guardrail template (G6) lets other Elyos HIGH-risk health
  projects (e.g. `food-safety-open`, `wash-guides`) inherit the gates rather than rebuild them.
- **Bus-factor:** schema + gates encode the rules in tooling so the project's *safety* does not
  depend on any one person remembering them.

---

## 16. Open questions

- **OQ-1 (critical):** Who is the **clinical steward** and the initial **credentialed reviewer
  pool**? Nothing clinical ships until secured. *(Human decision required.)*
- **OQ-2:** License posture for WHO **CC BY-NC-SA** material vs. our CC BY-SA output — confirm the
  paraphrase-only approach and segregation rule with a license reviewer. (§7.4)
- **OQ-3:** Final **core scenario list and order** — owned by the clinical steward; the §5 list is a
  candidate.
- **OQ-4:** Which **region(s)/locale(s)** does the first core target? (Drives emergency numbers,
  drug names, which council's guidance leads.) Needs a partner/requestor to anchor.
- **OQ-5:** Partner/requestor identity — NGO vs. sibling-project-as-internal-requestor for the
  interim. (Flips `verifiedNeed`.)
- **OQ-6:** Should top-tier scenarios require **two** credentialed sign-offs by default (dual
  control), and what counts as "credentialed" per scenario (physician vs. paramedic vs. accredited
  instructor)? Steward to ratify.
- **OQ-7:** Illustration production model — commissioned human illustrators vs. AI-assisted-then-
  human-redrawn — and how the "originals only" attestation is verified.
- **OQ-8:** Liability/disclaimer wording — review of the "not a substitute" framing with someone
  qualified on jurisdictional Good-Samaritan/liability nuances (informational, not legal advice).

---

## 17. References

- Elyos `CLAUDE.md` (work rules, lanes, quality bar, refusal guardrails).
- Elyos `docs/good-deed-definition.md` (5 criteria + risk tiers; HIGH = expert sign-off before merge).
- Elyos `packages/schema/src/schemas.ts` (Task JSON schema this plan maps to).
- Elyos `planning/ROADMAP.md` (portfolio; first-aid-open listed Track 6, ⚪ selected, **high** risk).
- ILCOR / International Liaison Committee on Resuscitation — Consensus on Science with Treatment
  Recommendations (CoSTR) and member-council guidelines (AHA, ERC, Resuscitation Council UK, etc.).
- World Health Organization — first-aid-relevant public-health guidance (note license terms,
  frequently CC BY-NC-SA 3.0 IGO).
- IFRC / national Red Cross & Red Crescent Societies — international first-aid guidance (note
  emblem protection under the Geneva Conventions).
- Relevant government health agencies for regional specifics (e.g. NHS, CDC, local EMS).

> *Source URLs/versions are recorded authoritatively in the project's machine-readable source
> registry (`/sources/*.yaml`), not hard-coded here, so provenance stays current and auditable.*

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the initial draft and **applied** to
the plan and tasks above (not merely proposed).

1. **Fail-closed tooling gate, not policy.** Made the expert sign-off a CI/metadata gate that
   blocks `delivered`/`done` (§6.2, §8.1) rather than a process promise — encoded so safety doesn't
   rely on memory.
2. **Dual-control sign-off for top-tier scenarios.** Added a requirement for two independent
   credentialed sign-offs (or clinician + accredited instructor) for CPR/anaphylaxis/severe-
   bleeding/infant-child (§8.3, risk table).
3. **Author≠reviewer separation.** Made reviewer independence explicit (§8.3) to prevent self-
   review of life-critical content.
4. **M2 as the hard clinical-ship gate.** Restructured the roadmap so M0–M1 are non-clinical/
   draft-only and *no clinical content ships until a reviewer is secured at M2* (§9).
5. **Illustrations are clinical content.** Stated that procedure diagrams pass the same sign-off (a
   wrong hand position is a safety defect) (§7.3, §8.1).
6. **Red Cross emblem treated as IHL-protected, not just trademark.** Called out Geneva-Conventions
   protection and banned emblem/logo/mark use explicitly (§7.1, §7.3, risk table).
7. **WHO non-commercial (NC) license conflict surfaced.** Flagged the CC BY-NC-SA → CC BY-SA
   incompatibility, with paraphrase-only mitigation and a legal gate (§7.4, OQ-2).
8. **"Not endorsed" notice.** Added an explicit notice that cited authorities are sources, not
   endorsers/partners (D7, §7.6) to prevent false-endorsement implication.
9. **Currency as a build gate + freshness watcher.** Added source-version stamps, review-by dates,
   and an automated freshness job that flags/unpublishes stale guides (D5, §6.2, §9 M3, §15).
10. **Region-aware fields, no universal hard-coding.** Made emergency number/drug/procedure region
    fields mandatory (D4, NG7, risk table) so content isn't dangerously region-blind.
11. **Honest outcome metrics with a caveat.** Replaced any implied "lives saved" claim with
    defensible proxies + an explicit caveat that true impact needs a partner study (§4).
12. **`verifiedNeed:false` everywhere clinical, partner TO BE SECURED.** Applied the honest-need
    rule across §2/§11/TASKS rather than inventing demand.
13. **Provenance lint with zero-unsourced tolerance.** Made 100% claim-sourcing a hard automated
    gate, not an aspiration (O2, §8.1).
14. **Errata = safety incident with SLA.** Added a public errata log and same-day-flag / 7-day
    root-cause SLA (§8.4, O9).
15. **Offline + print as first-class renderings.** Made offline bundle and print PDF required
    outputs (panicked/low-connectivity contexts), gated like web (§5, §6.2, §9).
16. **Plain-language readability gate.** Added a readability/plain-language check (§8.1 a11y gate)
    so content is usable under stress and by low-literacy readers.
17. **Translations require regional clinical re-review.** Forbade raw machine-translation publishing
    (NG7) and added regional reviewers (§11, §9 M4) to prevent translation-induced clinical error.
18. **Reviewer-scarcity risk + scope-to-capacity.** Added the bottleneck risk and the mitigation of
    sizing scope to reviewer capacity and recruiting a pool early (risk table, §11).
19. **AI-hallucination risk named explicitly.** Added "plausible-but-wrong step" risk with the
    provenance-lint + human-sign-off double catch (risk table).
20. **COI checklist for reviewers/stewards.** Required affiliation disclosure and recusal for
    commercial-training conflicts (§11).
21. **Narrow-and-deep decision locked.** Made "verified core before breadth" an explicit locked
    decision (D6) and roadmap shape, resisting premature scope expansion.
22. **Reusable safety-content pipeline as an explicit goal.** Elevated the gates/schema/template to
    a deliverable (G6, §15) so other HIGH-risk health projects inherit safety.
23. **"Constraints as identity" section.** Added an Ofelia-style framing that the five refusals
    *are* the product, setting the safety-first tone up front.
24. **Bounded scope vs. encyclopedia.** Sharpened NG3 to exclude wilderness/tactical/provider/
    chronic/drug-reference content, keeping the safety surface small.
25. **Sign-off ledger auditability + tamper = security incident.** Made the sign-off record
    machine-stored, auditable, and its tampering a security incident (§8.1, §14).

---

## Review sign-off

**Reviewer:** Senior staff engineer + TPM (drafting author, self-review pass) · **Date:** 2026-06-28

**Completeness check (against PLAN_SPEC 17 sections):** All 17 required H2 sections present and in
order (Executive summary → References), plus the spec'd metadata header, an Ofelia-style positioning
block, a "Constraints as identity" section, Appendix A (25 applied improvements), and this sign-off.
Risks table uses the required columns (Risk | Likelihood | Impact | Mitigation | Owner). TASKS.md
maps every task to the Task JSON schema with a schema-valid example.

**Correctness fixes applied during review:**
- Verified every Task JSON field against `packages/schema/src/schemas.ts` (enums for `type`, `lane`,
  `priority`, `riskTier`, `deliverable`, `tokenEstimate`, `status`; required fields incl.
  `verifiedNeed`; `fundedBudgetUsd` required only for `lane:"funded"`). Confirmed the example JSON
  uses only allowed fields and `additionalProperties:false` compliance.
- Confirmed the HIGH-risk gate from `good-deed-definition.md` ("credentialed expert sign-off before
  merge") is encoded both in the Definition of Shipped (§8.2) and in tooling (§6.2, §8.1), not just
  prose.
- Ensured every clinical deliverable carries `verifiedNeed:false` and reviewer assignment, and that
  partner/requestor/steward are marked **TO BE SECURED**, consistent across PLAN and TASKS.
- Checked the license posture is conservative (paraphrase-only default; WHO-NC tension flagged;
  emblem ban) and that no copyrighted text/figure/logo reuse is anywhere permitted.
- Verified the roadmap exit criteria are measurable and that clinical shipping is correctly gated
  behind M2 (reviewer secured), so the plan cannot accidentally authorise unsigned shipping.

**Outstanding (require human decision):** OQ-1 (clinical steward + reviewer pool), OQ-2 (WHO-NC
license confirmation), OQ-4/OQ-5 (target region + partner/requestor). These are blockers for
*clinical* shipping (M2+), not for the non-clinical M0–M1 foundation.

**Verdict:** Plan is internally consistent, schema-aligned, and conservative on the HIGH-risk
guardrails. Approved as a Draft (v0.1.0) to proceed with M0 foundation work; clinical work blocked
pending OQ-1.
