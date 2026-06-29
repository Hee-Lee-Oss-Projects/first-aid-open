# first-aid-open — Task backlog (schema-mapped)

> **Status:** Draft · **Version:** 0.1.0 · **Last updated:** 2026-06-28 ·
> **Owner:** TBD (maintainer) · **Lane:** donated · **Risk tier:** HIGH

Companion to `PLAN.md`. Milestones mirror PLAN §9 (M0–M5). Every task maps to an Elyos Task JSON.

---

## How these tasks map to Elyos

Each row below becomes a Task JSON validated against `packages/schema/src/schemas.ts`. Field usage
for this project:

- **id** — stable slug `first-aid-<area>-NNN`.
- **title / project** — human title; `project: "first-aid-open"`.
- **type** — `code` (tooling/schema/renderers), `data` (source registry), `writing` (guides),
  `design-spec` (illustration system, framing template), `research` (source mapping),
  `maintenance` (freshness/refresh).
- **lane** — `donated` for all listed tasks (no funded tasks here; any future funded drafting task
  must add `fundedBudgetUsd` per the schema's conditional requirement).
- **priority** — `high|medium|low`.
- **domain** — array, e.g. `["health","safety","first-aid"]`.
- **riskTier** — `high` for any clinical content/illustration; `low|medium` for pure
  tooling/schema/non-clinical scaffolding.
- **urgent** — boolean (kept `false`; safety > speed here).
- **deliverable** — `pr` (code), `dataset` (source registry/metadata), `document` (guides/specs),
  `translation` (localised guides).
- **tokenEstimate** — `small|medium|large`.
- **status** — `open|in-progress|review|delivered|done`. **Clinical tasks may not pass `review`
  until the credentialed sign-off gate is satisfied (PLAN §8).**
- **context / objective / acceptanceCriteria[] / output** — as filled per task.
- **resources[]** — source registry entries, PLAN sections, sibling projects.
- **requestor** — `"TO BE SECURED"` until a partner is named.
- **verifiedNeed** — **`false`** for all clinical deliverables (no partner secured); may be `true`
  only for internal tooling explicitly needed by the project itself.
- **outputLicense** — `"MIT"` for code, `"CC-BY-SA-4.0"` for content/illustrations.

> **Hard rule reflected in every clinical task:** no `delivered`/`done` without recorded
> credentialed-clinician sign-off (PLAN §8.2). Reviewer column names the *gatekeeper*, not just a
> code reviewer.

---

## Milestone M0 — Foundation & guardrails (non-clinical)

Goal: stand up repo, schema, registry, guardrail framing, illustration system, and CI gates
**without shipping any clinical claim.**

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-schema-001 | Define guide + source + provenance + sign-off JSON Schemas | code | medium | low | pr | — | Maintainer |
| first-aid-data-002 | Build the authoritative source registry (`/sources/*.yaml`) w/ license + version fields | data | medium | medium | dataset | first-aid-schema-001 | License/IP reviewer |
| first-aid-spec-003 | Ratify the mandatory safety-framing + "not endorsed" template | design-spec | small | medium | document | — | Clinical steward (TBS) |
| first-aid-code-004 | Implement CI gates: provenance, framing, a11y, sign-off, currency (fail-closed) | code | large | low | pr | first-aid-schema-001 | Maintainer |
| first-aid-spec-005 | Illustration system + "originals only" provenance/attestation process | design-spec | medium | medium | document | — | License/IP reviewer |
| first-aid-code-006 | Renderers: static web + print PDF + offline bundle (framing-injected) | code | large | low | pr | first-aid-schema-001 | Maintainer |
| first-aid-writing-007 | Non-clinical pilot page ("how to use this library / call local emergency number") | writing | small | low | document | first-aid-code-004, first-aid-code-006 | Maintainer |

**Acceptance criteria (key tasks)**

- **first-aid-schema-001**
  - Guide frontmatter schema requires: per-claim `sourceRefs[]`, `region[]`, `sourceVersionStamp`,
    `reviewBy` (date), `signOff[]` (name, credential, date, scope, sourceCycleVerified),
    `safetyFraming` block.
  - Source schema requires: publisher, title, url, publicationDate, guidelineCycle, licenseNote,
    reusePosture (`paraphrase-only|open-adaptable`, default `paraphrase-only`), accessDate.
  - Sign-off schema models dual-control (array, `minItems` configurable per scenario tier).
  - All schemas validate with Ajv; invalid fixtures fail; `pnpm build && pnpm test && pnpm lint` pass.
- **first-aid-code-004**
  - Provenance lint **fails** if any clinical claim lacks a current registry source (zero tolerance).
  - Framing lint **fails** if any rendering omits the safety-framing/region block.
  - Sign-off gate **fails** any guide reaching `delivered`/`done` without a recorded sign-off
    (proven by a fixture that is correctly *blocked*).
  - Currency gate **fails** a guide past its `reviewBy`. All gates fail-closed (default deny).
- **first-aid-spec-003**
  - Template contains: "informational only — not a substitute for professional care or accredited
    training," "in an emergency call your local emergency number," region applicability, and the
    "cited organisations are sources, not endorsers" notice. No emblems/logos referenced.

**Definition of Done (M0):** repo builds; all schemas + fail-closed gates implemented and proven by
fixtures (including a *blocked* unsigned guide); framing template ratified; illustration provenance
process documented; the **non-clinical** pilot page renders to web+print+offline and passes all
non-clinical gates. **No clinical content shipped.**

---

## Milestone M1 — One verified guide (vertical slice, draft-only)

Goal: prove the full pipeline on one steward-chosen scenario, gate-ready but blocked on sign-off.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-research-101 | Map the chosen scenario's official guidance → registry sources (paraphrase notes) | research | medium | high | document | first-aid-data-002 | Clinical steward (TBS) |
| first-aid-writing-102 | Draft the first core guide (steward-chosen) w/ full per-claim provenance + framing | writing | large | high | document | first-aid-research-101, first-aid-spec-003 | Credentialed reviewer (TBS) |
| first-aid-design-103 | Original illustrations for the guide (no traced/copyrighted source; attested) | design-spec | medium | high | document | first-aid-spec-005, first-aid-writing-102 | Credentialed reviewer (TBS) |
| first-aid-code-104 | Wire the guide through all automated gates; demonstrate sign-off gate blocks ship | code | small | low | pr | first-aid-code-004, first-aid-writing-102 | Maintainer |

**Acceptance criteria (key tasks)**

- **first-aid-writing-102**
  - Every clinical step paraphrased (no copied expression) and linked to ≥1 current registry source.
  - Region fields populated (emergency number/drug/procedure not hard-coded as universal).
  - Safety framing + "not endorsed" notice present; plain-language readability check passes.
  - Passes provenance/framing/a11y/currency gates; **status capped at `review`** pending sign-off.
- **first-aid-design-103**
  - Each asset carries author/method/license + "not traced from / not a derivative of any
    copyrighted image" attestation; no emblems/logos; depicted procedure matches the verified text.
- **first-aid-code-104**
  - A test proves an unsigned guide **cannot** be promoted to `delivered`/`done` (gate refuses).

**Definition of Done (M1):** one core guide fully drafted, illustrated, and passing **all automated
gates**, sitting in `review` correctly **blocked on the human sign-off gate** — demonstrating the
pipeline refuses to ship unverified life-critical content. `verifiedNeed:false` throughout.

---

## Milestone M2 — Reviewer pool & first SHIPPED guide

Goal: secure ≥1 credentialed reviewer; ship the first fully signed-off guide.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-maintenance-201 | Onboard credentialed reviewer pool + clinical steward (COI + scope recorded) | maintenance | medium | high | document | — (human/partner action) | Maintainer + Clinical steward (TBS) |
| first-aid-writing-202 | Obtain + record clinical sign-off(s) for the M1 guide (dual-control for top tier) | writing | small | high | document | first-aid-writing-102, first-aid-maintenance-201 | Credentialed reviewer (TBS) |
| first-aid-code-203 | Ship the first guide: web+print+offline, sign-off ledger live | code | small | low | pr | first-aid-writing-202, first-aid-code-104 | Maintainer |

**Acceptance criteria (key tasks)**

- **first-aid-maintenance-201**
  - ≥1 named credentialed reviewer onboarded with credential, scope, and COI disclosure recorded;
    clinical steward role filled (OQ-1 resolved). Dual-control policy ratified for top-tier scenarios.
- **first-aid-writing-202**
  - Sign-off record(s) (name, credential, date, scope, source-cycle verified) stored in metadata;
    two independent sign-offs if the scenario is top-tier.
- **first-aid-code-203**
  - Guide meets the full Definition of Shipped (PLAN §8.2): all six gates pass + recorded sign-off +
    published in three renderings + sign-off ledger entry visible/auditable.

**Definition of Done (M2):** reviewer pool + steward secured; the first guide is **Shipped** with
recorded credentialed sign-off in all three renderings; sign-off ledger live. *First true deed
delivered.* (`verifiedNeed` may flip to `true` if a partner is also secured here.)

---

## Milestone M3 — Core library (8–12 verified scenarios)

Goal: ship the verified core; freshness watcher live.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-writing-301 | Draft + sign-off remaining core scenarios (CPR, choking, anaphylaxis, etc.) | writing | large | high | document | first-aid-code-203 | Credentialed reviewer (TBS) |
| first-aid-design-302 | Original illustrations for remaining core scenarios (attested) | design-spec | large | high | document | first-aid-spec-005, first-aid-writing-301 | Credentialed reviewer (TBS) |
| first-aid-code-303 | Freshness watcher: flag/unpublish guides past reviewBy or on source-cycle change | code | medium | low | pr | first-aid-code-004 | Maintainer |
| first-aid-maintenance-304 | Confirm ≥1 external/sibling adopter; start adoption log | maintenance | small | medium | document | first-aid-code-203 | Steward (last-mile, TBS) |

**Acceptance criteria (key tasks)**

- **first-aid-writing-301**
  - Each scenario independently signed off (dual-control where top tier); 100% provenance; region
    fields; framing. No scenario ships without its own sign-off.
- **first-aid-code-303**
  - Watcher detects an out-of-window `reviewBy` and a registry source-version bump, opens a
    maintenance task, and flags/unpublishes the affected guide automatically (proven by fixture).

**Definition of Done (M3):** ≥8 core scenarios **Shipped** with full sign-off; freshness watcher
operating; ≥1 confirmed adopter logged (O4).

---

## Milestone M4 — Reach: i18n, accessibility depth, partner distribution

Goal: make the verified core reusable across languages/channels with regional re-review.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-translation-401 | Derive ≥2 language editions w/ regional clinical/contextual re-review | translation | large | high | translation | first-aid-writing-301 | Regional reviewer (TBS) |
| first-aid-maintenance-402 | Full accessibility audit (WCAG 2.2 AA) across web/print/offline | maintenance | medium | low | document | first-aid-code-006 | Accessibility reviewer |
| first-aid-maintenance-403 | Confirm a distribution partner or sibling-project integration | maintenance | small | medium | document | first-aid-code-203 | Steward (last-mile, TBS) |

**Acceptance criteria (key tasks)**

- **first-aid-translation-401**
  - No raw machine-translation published; each locale re-reviewed for regional correctness
    (emergency numbers, drug names, procedures) by a regional credentialed reviewer; sign-off
    recorded per locale.
- **first-aid-maintenance-402**
  - AA checks pass across all three renderings; plain-language and print/offline verified; issues
    logged and fixed before sign-off.

**Definition of Done (M4):** ≥2 regionally-reviewed language editions shipped; AA audit passed;
distribution partner/integration confirmed; freshness SLA met (O6=100%).

---

## Milestone M5 — Sustainability & template

Goal: durable maintenance + publish the reusable safety-content pipeline template.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| first-aid-maintenance-501 | Stand up the maintenance rota + review-by cadence; run ≥1 refresh cycle | maintenance | medium | high | document | first-aid-code-303 | Clinical steward (TBS) |
| first-aid-spec-502 | Document the reusable HIGH-risk safety-content pipeline + guardrail template | design-spec | medium | low | document | first-aid-code-004 | Maintainer |
| first-aid-maintenance-503 | Report outcome metrics O1–O9; publish errata log process | maintenance | small | low | document | first-aid-code-203 | Maintainer |

**Definition of Done (M5):** maintenance rota operating with ≥1 completed refresh cycle on a shipped
guide; reusable pipeline/guardrail template published for other HIGH-risk Elyos health projects;
O1–O9 reported; errata process live.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| first-aid-spec-901 | Easy-read / dyslexia-friendly variants (with `easy-read-plus`) | design-spec | medium | medium | document | Needs plain-language + clinical re-check |
| first-aid-design-902 | Pictogram-only / low-literacy edition (with `open-pictograms`) | design-spec | medium | high | document | Illustration = clinical content; sign-off required |
| first-aid-data-903 | Region pack expansion (more locales' emergency numbers/services) | data | medium | medium | dataset | Per-region license + verification |
| first-aid-code-904 | Embeddable widget/export for `proper-prepper` + `community-resource-maps` | code | medium | low | pr | Must carry framing + provenance |
| first-aid-research-905 | Expand scenario set beyond core (steward-prioritised) | research | large | high | document | Only after core verified; respects NG3 bounds |
| first-aid-maintenance-906 | Annual ILCOR-cycle full re-review sweep | maintenance | large | high | document | Recurring; currency is the maintenance core |

---

## Example task JSON (first M0 task — schema-valid)

```json
{
  "id": "first-aid-schema-001",
  "title": "Define guide, source, provenance, and sign-off JSON Schemas",
  "project": "first-aid-open",
  "type": "code",
  "lane": "donated",
  "priority": "high",
  "domain": ["health", "safety", "first-aid", "schema"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "pr",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "first-aid-open is a HIGH-risk, safety-critical project publishing illustrated first-aid guides paraphrased from and cited to official sources (ILCOR/WHO/IFRC). Before any clinical content exists, the project needs machine-readable schemas that make the safety gates enforceable in tooling: every clinical claim must trace to a current source, every guide must carry safety framing and region applicability, and nothing may ship without a recorded credentialed-clinician sign-off. This task defines those schemas; it ships no clinical content.",
  "objective": "Define and validate JSON Schemas (Ajv) for: (1) guide frontmatter (per-claim sourceRefs, region[], sourceVersionStamp, reviewBy, signOff[] with name/credential/date/scope/sourceCycleVerified, and a mandatory safetyFraming block); (2) source-registry entries (publisher, title, url, publicationDate, guidelineCycle, licenseNote, reusePosture defaulting to paraphrase-only, accessDate); (3) the sign-off record supporting dual-control. These schemas are the foundation the fail-closed CI gates build on.",
  "acceptanceCriteria": [
    "Guide, source, and sign-off schemas defined as Ajv-validated JSON Schema with additionalProperties:false.",
    "Guide schema REQUIRES per-claim sourceRefs, region[], sourceVersionStamp, reviewBy, signOff[], and safetyFraming.",
    "Source schema includes a reusePosture enum defaulting to 'paraphrase-only' and a per-source licenseNote.",
    "Sign-off schema supports dual-control (array with configurable minItems for top-tier scenarios).",
    "Valid fixtures pass and invalid fixtures (missing source, missing sign-off, missing framing) fail.",
    "pnpm build && pnpm test && pnpm lint all pass; commit signed off (DCO); changeset added."
  ],
  "resources": [
    "PLAN.md#6-solution-approach--architecture",
    "PLAN.md#8-quality-review--risk-gates",
    "packages/schema/src/schemas.ts"
  ],
  "output": "A PR adding the guide/source/sign-off JSON Schemas, Ajv validation, fixtures (valid + invalid), and tests, with no clinical content included.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```

> All other clinical-content tasks follow the same shape with `riskTier:"high"`,
> `outputLicense:"CC-BY-SA-4.0"`, `deliverable:"document"`/`"translation"`, `verifiedNeed:false`,
> and a Reviewer that is the **credentialed sign-off gatekeeper** — never promoted past `review`
> without a recorded sign-off.
