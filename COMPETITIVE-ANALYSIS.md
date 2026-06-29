# Competitive & Improvement Analysis — `first-aid-open`

> Open, plain-language, illustrated first-aid guides, paraphrased-and-cited to authoritative
> bodies (ILCOR/AHA/ERC/RC-UK, WHO, IFRC), clinician-signed-off, multilingual, offline-capable,
> for low-resource settings. HIGH-risk (safety-critical health).
> Analysis date: 2026-06-29. Sources are live URLs, cited inline.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong for a HIGH-risk health project. Its safety architecture — fail-closed
expert sign-off gate in tooling, provenance lint with zero-unsourced tolerance, dual-control review
for top-tier scenarios, author≠reviewer separation, mandatory "not a substitute" framing, region
fields, currency gate, errata-as-safety-incident — is the right spine and is mostly correct. The
findings below are refinements, with two material issues flagged.

### 1.1 CRITICAL finding — the currency model is built on an outdated cadence assumption

The plan repeatedly anchors currency to a **~5-year guideline cycle** ("e.g. the ILCOR/CPR cycle",
§1 constraint 4, D5, §15). This is **out of date and a safety-relevant design error**. ILCOR
**abandoned the 5-year batch-and-queue model in favour of Continuous Evidence Evaluation (CEE)**,
now publishing an **annual CoSTR** summary series; member councils (AHA, ERC) update on their own
rolling schedules off that evidence base
([AHA/ILCOR FAQ](https://cpr.heart.org/en/resuscitation-science/ilcor/ilcor-faqs);
[2025 Executive Summary CoSTR](https://ilcor.org/uploads/Executive-Summary-2025-COSTR.pdf);
[ILCOR publications](https://ilcor.org/publications)). Concrete evidence the world already moved:
the **2025 CoSTR** (published Oct 2025), the **IFRC International First Aid, Resuscitation and
Education Guidelines 2025** (launched 23 Mar 2025,
[IFRC](https://www.ifrc.org/document/ifrc-international-first-aid-resuscitation-and-education-guidelines-2025)),
**ERC Guidelines 2025 First Aid**
([Resuscitation Journal](https://www.resuscitationjournal.com/article/S0300-9572(25)00264-3/fulltext)),
and the **2024 AHA/American Red Cross Guidelines for First Aid**
([AHA](https://cpr.heart.org/en/resuscitation-science/2024-first-aid-guidelines)). **Implication:**
the freshness watcher must poll **annual CoSTR + per-council release feeds**, not a 5-year timer;
"review-by" windows pegged to a 5-year cycle would let content silently rot for years. This should
be corrected in §1, D5, §6.2, §13 and the schema (`guidelineCycle` must capture an annual/rolling
source, not a quinquennial edition). **Fix before M0 schema is frozen.**

### 1.2 CRITICAL finding — high-stakes clinical-accuracy specifics are deferred entirely to a yet-unsecured reviewer, with no interim accuracy floor

The whole clinical-accuracy guarantee rests on the credentialed-reviewer/clinical-steward roles,
all marked **TO BE SECURED (critical)** (§11, OQ-1), and the plan correctly refuses to ship clinical
content until M2. That is the right hard gate. But there is a subtler risk the plan does not fully
address: the **specific numeric/procedural facts** that kill when wrong — adult compression rate
100–120/min and depth 5–6 cm, 30:2 compression-to-ventilation for lay single rescuers, the
**compression-first (CAB)** good-practice statement now added for **drowning-related arrest** in the
2025 CoSTR, choking (back blows/abdominal thrusts; **not** abdominal thrusts in infants),
**catastrophic-haemorrhage-first** sequencing and tourniquet/wound-packing guidance, anaphylaxis IM
adrenaline auto-injector use and positioning, **20-minute cool-running-water** burn cooling
([IFRC 2025](https://www.ifrc.org/sites/default/files/2026-03/IFRC%20International%20First%20Aid,%20Resuscitation%20and%20Education%20Guidelines%202025.pdf)) —
are exactly where a paraphrase can drift by a word and become dangerous. The plan should add: (a) a
**structured fact table per scenario** (rate/depth/ratio/dose/time as discrete, individually-sourced
fields, not free prose) so the provenance lint and reviewer check **values**, not just "a citation
exists"; (b) an explicit rule that **AI must transcribe these numbers verbatim from the cited
guideline and flag, never interpolate or "round"**; (c) acknowledgement that automated gates cannot
detect a *plausible-but-wrong number* — only the human reviewer can — reinforcing why M1 deliberately
parks drafts in `review`. This is the single most important accuracy dimension and deserves its own
sub-section in §8.

### 1.3 Other correctness/completeness notes

- **"Not a substitute / call emergency services" boundary (G3, §8.1 gate 2): well-handled.** The
  framing-lint-fails-build approach is correct. Strengthen by requiring the **local emergency number
  to come from the region field**, never a hard-coded "911/112" in the template itself (the plan
  implies this via D4/NG7 but the framing template in TASKS first-aid-spec-003 should state it
  explicitly, or it will leak a US/EU default).
- **Medical-review gate: correct and enforced**, but two gaps. (i) Define **what "credentialed"
  means per scenario tier *before* M1** (OQ-6 currently defers it) — otherwise M1 produces a draft
  no one is qualified-by-rule to clear. (ii) The plan has no **re-sign-off-on-guideline-change**
  rule: when CEE updates a recommendation, a refreshed guide needs a *new* sign-off, not just a date
  bump. Add to §8/§15.
- **Regional variation: strong** (D4, NG7, region fields), but the plan under-specifies **drug-name
  divergence** (adrenaline vs. epinephrine; auto-injector availability/legality varies and in many
  low-resource settings auto-injectors are simply unavailable) and **aspirin-for-suspected-MI**
  caveats. The region model should carry "intervention availability," not just numbers/names.
- **Multilingual review (O5, M4, §11 regional reviewers): correct in principle** (no raw MT, regional
  clinical re-review). Add that **back-translation / numeric-integrity check** is mandatory — the
  highest translation risk is a transposed dose or rate, which a fluency review can miss.
- **Liability (OQ-8): appropriately flagged but unresolved.** Good-Samaritan and disclaimer wording
  is jurisdiction-specific; the plan correctly notes "informational, not legal advice." Recommend
  this become a **blocking gate item for any region's first ship**, not a general open question.
- **Licensing (CC BY-SA vs WHO CC BY-NC-SA): correctly identified tension** (§7.4, OQ-2). The
  paraphrase-only-facts mitigation is sound (facts aren't copyrightable). One addition: **IFRC 2025
  guidelines and WHO BEC are themselves copyrighted**; confirm even paraphrase-with-citation
  posture with the IP reviewer, and never imply the cited body endorses (D7 handles this well).
- **Completeness:** all 17 sections present, schema-mapped, internally consistent. No major omissions
  beyond §1.1/§1.2 above.

---

## 2. Competitive landscape (researched, cited)

| Competitor | What it is | Strengths | Weaknesses / gap for our beneficiary |
|---|---|---|---|
| **IFRC / Red Cross — First Aid app + 2025 Guidelines** | Official app (interactive, step-by-step) + the global evidence-based first-aid guidelines | Authoritative; the *source* we cite; brand trust; quizzes; 2025 evidence base; National-Society localisation ([IFRC app, Play](https://play.google.com/store/apps/details?id=com.cube.gdpc.fa); [IFRC 2025 guidelines](https://www.ifrc.org/document/ifrc-international-first-aid-resuscitation-and-education-guidelines-2025)) | App is **per-country, app-store-gated, not offline-print-reusable, not openly licensed**; guidelines PDF is **copyrighted, not CC**; emblem-protected; not freely re-hostable/derivable |
| **AHA + American Red Cross / ERC / RC-UK guidelines** | The clinical consensus documents (2024 AHA/ARC First Aid; ERC 2025) | Gold-standard accuracy; the canonical citation targets ([AHA 2024](https://cpr.heart.org/en/resuscitation-science/2024-first-aid-guidelines); [ERC 2025](https://www.resuscitationjournal.com/article/S0300-9572(25)00264-3/fulltext)) | Written **for clinicians/instructors**, paywalled training, copyrighted, dense, English-first, not plain-language for a panicked layperson |
| **WHO / ICRC — Basic Emergency Care (BEC) + Emergency Care Toolkit** | Open-source course + open-access pocket guide for low-resource settings ([WHO ECT](https://www.who.int/teams/integrated-health-services/clinical-services-and-systems/emergency-and-critical-care/emergency-care-toolkit)) | **Open-access**, designed for **low-resource** settings, evidence-based, WHO authority | Targets **first-contact health workers, not lay bystanders**; CC **BY-NC-SA** (non-commercial); not an illustrated lay library |
| **Hesperian — *Where There Is No Doctor* / HealthWiki** | Community-health manuals, free online, heavily illustrated | **100+ languages, 221 countries, 36M+ HealthWiki users**, low-literacy illustration tradition, low-resource focus ([Hesperian](https://en.hesperian.org/hhg/New_Where_There_Is_No_Doctor); [Wikipedia](https://en.wikipedia.org/wiki/Where_There_Is_No_Doctor)) | **Broad primary-care scope, not first-aid-specialised**; update cadence is slow (decadal); not tightly source-pinned to current resuscitation guidelines; bespoke copyright (free-use but not CC BY-SA) |
| **St John Ambulance (UK) / national bodies** | Free online first-aid advice + free app, clinically governed | Plain-language, accessible (BSL, easy-read w/ NHS), CQC-regulated clinical team ([SJA advice](https://www.sja.org.uk/first-aid-advice/); [accessible resources](https://www.sja.org.uk/get-advice/accessible-first-aid-resources/)) | **UK-centric** (999, UK drugs); **copyrighted, not reusable/derivable**; web/app only, not an openly-licensed corpus |
| **MedlinePlus (NIH/NLM)** | US-gov health-info portal incl. first aid, multi-language | **Public-domain (US gov)**, multi-language index, trusted ([First Aid](https://medlineplus.gov/firstaid.html); [multi-language](https://medlineplus.gov/languages/firstaid.html)) | **Portal/encyclopedia, not original illustrated step guides**; US-centric (911); not low-resource/offline-print optimised |
| **WikEM / WikiDoc (FOAM wikis)** | Crowd wiki emergency-medicine references | Large, open, fast-moving ([WikEM](https://wikem.org/); [Wikipedia](https://en.wikipedia.org/wiki/WikEM)) | **For clinicians, not lay**; **reliability concerns of wiki/no-credential model** (WikiDoc requires no credentials); not signed-off, not multilingual lay content |
| **App-store first-aid apps (generic)** | Many free/paid apps | Convenient | Variable/unsourced quality, no provenance, ad-driven, not openly licensed, not low-resource/offline-print |

**Landscape summary:** authoritative content exists but is **copyrighted and clinician- or
country-targeted** (IFRC/AHA/ERC/SJA); openly-licensed content is either **broad-not-first-aid**
(Hesperian), **portal-not-illustrated-guide** (MedlinePlus), **clinician-not-lay** (WHO BEC, WikEM),
or **unsourced** (generic apps). **No incumbent is simultaneously open-licensed for derivatives,
lay-plain-language, illustrated, current-guideline-pinned with auditable per-claim provenance,
clinician-signed-off, multilingual with regional re-review, and offline/print-first.** That precise
intersection is the white space.

---

## 3. Gaps `first-aid-open` can fill

1. **Open license *for derivatives* (CC BY-SA) on first-aid content.** Every authoritative source is
   copyrighted/NC; nobody offers a freely re-hostable, printable, translatable, remixable first-aid
   corpus. This is the core unfilled gap.
2. **Per-claim machine-readable provenance.** No incumbent exposes claim→source→guideline-cycle
   links that a third party can audit. This is genuinely novel for lay health content.
3. **Plain-language + illustrated + low-literacy, but tightly current-guideline-pinned.** Hesperian
   has the illustration/low-literacy tradition but not the resuscitation-guideline pinning; the
   guideline bodies have the rigour but not the plain-language/illustration/openness.
4. **Offline + print-first for low-connectivity contexts**, gated to the same clinical standard as
   web (most apps assume connectivity and an app store).
5. **Region-as-data** (emergency number, drug name/availability, locally-leading council) instead of
   one region hard-coded — neither SJA (UK) nor MedlinePlus (US) nor most apps do this.
6. **Currency as a tracked, auditable build gate** tied to the *actual* annual CEE/CoSTR cadence —
   no lay resource tracks "is this still the current recommendation?" as machine state.
7. **A reusable sourced-health-content engine** other low-resource health domains can inherit
   (Hesperian/WHO solved this organisationally but not as open tooling).

---

## 4. Differentiators to win

- **D-1 (strongest): Auditable, open, current-guideline-pinned provenance.** "Every step is
  paraphrased from a *named, dated, current* authority, machine-checkable, clinician-signed,
  freely reusable." No competitor can claim all of: open-for-derivatives + per-claim provenance +
  current-cycle currency + clinician sign-off. This is the defensible moat.
- **D-2: Clinician sign-off + provenance + currency *enforced in tooling*** (fail-closed), not
  promised in prose — a trust signal incumbents (esp. wikis/apps) structurally lack.
- **D-3: Offline/print-first, region-as-data, multilingual-with-clinical-re-review** — purpose-built
  for the low-resource bystander the IFRC app and SJA web do not serve well.
- **D-4: Honest scope.** Narrow-deep-verified core + unmistakable "not a substitute/take a course/
  call your local number," with cited-but-not-endorsed authorities — credibility through humility.
- **D-5: Composability.** Clean source-cited base that Elyos siblings (translations, phrasebooks,
  prepper, resource-maps) derive from — a platform play, not a single artifact.

---

## 5. Claude API leverage — and the hard limits

**Where Claude adds high value (all human-gated):**
- **Plain-language drafting from a cited guideline excerpt** into a fixed step structure, at a target
  reading level (e.g. CEFR A2 / grade-6), preserving the exact numbers from the source.
- **Reading-level / plain-language grading and rewriting** to pass the readability gate; producing
  easy-read and low-literacy variants for sibling projects.
- **Translation drafting + back-translation + numeric-integrity diffing** to surface where a dose/
  rate/ratio changed across languages (draft only — regional clinician re-review still ships it).
- **Provenance scaffolding:** extracting candidate claim→source mappings and structured fact tables
  (rate/depth/ratio/dose/time) for the reviewer to verify; drafting alt-text for illustrations.
- **Freshness triage:** summarising what changed in a new CoSTR/council release and flagging which
  guides it touches (proposes maintenance tasks; does not edit clinical content unsupervised).
- **Consistency/lint assistance:** detecting missing framing blocks, region hard-coding, tone drift.

**Where Claude must NOT decide (hard rules — must be enforced, not advisory):**
- **No medical content beyond what a cited current guideline says.** No interpolation, no "rounding,"
  no filling gaps, no adjudicating between councils, no inventing a recommendation.
- **Never the sign-off authority.** Claude drafts; a credentialed human clears. No fast lane, ever.
- **No fabricated citations or numbers.** A claim without a verifiable current source must be
  **flagged, not written**. Numbers transcribed verbatim from source, never generated from memory.
- **Current-guideline sourcing must be verified**, not assumed — Claude's training cutoff can lag the
  latest CoSTR; it must defer to the registry/source, not its own recall.
- **Must always carry the "not a substitute / call local emergency number" framing** — never produce
  content that reads as a substitute for care or as live triage of a specific person.
- **Flag-don't-improvise** under uncertainty (per CLAUDE.md): stop and surface, never guess on
  life-critical content.

(See `claude-api` skill for current model IDs/pricing if a funded drafting task is ever specced;
all listed tasks are donated-lane today.)

---

## 6. Ten concrete optimizations

1. **Re-base currency on annual CEE/CoSTR, not a 5-year cycle** (§1.1). Make the freshness watcher
   poll ILCOR CoSTR + AHA/ERC/IFRC release feeds; change schema `guidelineCycle` accordingly.
   *(Highest priority — fix before freezing the M0 schema.)*
2. **Add a per-scenario structured "critical fact table"** (rate/depth/ratio/dose/time/sequence as
   discrete individually-sourced fields). Lint validates presence; reviewer validates *values*.
3. **Add a re-sign-off-on-change rule:** a guideline update invalidates the prior sign-off and
   requires a fresh one, not just a date bump.
4. **Define "credentialed per scenario tier" before M1** (resolve OQ-6 early) so M1 drafts have a
   qualified clearer by rule.
5. **Make emergency number/drug strictly region-field-driven** in the framing template; CI fails on
   any literal "911/999/112" in shared content.
6. **Model intervention availability, not just names** (e.g. adrenaline auto-injector may be
   unavailable in low-resource settings) so guidance degrades gracefully by region.
7. **Mandatory numeric back-translation check** in the translation pipeline (a transposed dose is the
   top translation hazard a fluency review misses).
8. **Promote liability/disclaimer review (OQ-8) to a per-region blocking gate item**, not an open
   question, before that region's first ship.
9. **Seed an authoritative source-feed registry now** (ILCOR publications, AHA/ERC/IFRC release pages)
   as machine-pollable URLs — turns the freshness watcher from manual to automated.
10. **Pre-secure reviewer capacity by partnering with a National Red Cross/St John society or an
    EM-physician volunteer network** before M2; reviewer scarcity is the named critical-path risk.

---

## 7. Parallel & perpendicular spin-offs

- **Parallel (same engine, adjacent content):**
  - `emergency-phrasebooks` — first-aid-open's region/number/drug fields + the structured fact tables
    feed cross-language emergency phrasing; shared i18n base.
  - `vital-info-translations` — consumes the clean source-cited English base; regional re-review
    process is shared.
  - `wash-guides` (water/sanitation/hygiene) and a `food-safety-open` — **inherit the same
    sourced-health-content engine**: provenance schema, sign-off gate, currency watcher, framing
    template (PLAN G6 already anticipates this).
  - `easy-read-plus` — low-literacy/dyslexia-friendly renderings of the same verified guides.
- **Perpendicular (platform leverage):**
  - **A reusable "sourced-health-content engine"** (schema + provenance lint + fail-closed sign-off
    gate + freshness watcher + framing lint + offline/print renderers) as a standalone Elyos package
    that any HIGH-risk health-content project adopts — the highest-leverage spin-off.
  - `community-resource-maps` / `proper-prepper` — embed verified guides + map to local emergency
    numbers/facilities (a natural internal requestor to flip `verifiedNeed`).
- **Partnership path:** a **National Red Cross/Red Crescent society, St John Ambulance, or the IFRC
  Global First Aid Reference Centre / WHO emergency-care team** as content validator/distributor —
  noting the emblem/endorsement constraints (D7); cite-don't-co-brand unless formalised. Hesperian is
  a model and possible ally for the low-literacy/multilingual illustration tradition.

---

## 8. Open questions

1. **Currency cadence (new):** Will the freshness model track the **annual CEE/CoSTR + per-council
   releases**? (The plan's 5-year assumption is wrong — §1.1.) Who owns the source-feed registry?
2. **Numeric integrity:** Will critical facts be modelled as **discrete sourced fields** with verbatim
   transcription, and will translation enforce **numeric back-translation**? (§1.2)
3. **OQ-1 (plan's, unchanged, critical):** Who is the clinical steward + initial reviewer pool?
   Nothing clinical ships until secured. Can a Red Cross/St John/EM-volunteer partnership pre-empt the
   scarcity risk?
4. **Region anchor (OQ-4/5):** Which region/locale + which council leads for the first core, and who
   is the requestor (NGO vs. internal sibling)?
5. **WHO/IFRC license posture (OQ-2):** Confirm paraphrase-only-facts vs CC BY-SA output with the IP
   reviewer — including IFRC 2025 guidelines (copyrighted) and WHO BEC (CC BY-NC-SA).
6. **Credential definition (OQ-6):** What counts as "credentialed" per scenario tier, resolved
   *before* M1 drafting?
7. **Intervention availability:** How is "unavailable in this region" represented so guidance degrades
   safely rather than recommending an inaccessible drug/device?
8. **Liability wording (OQ-8):** Per-jurisdiction Good-Samaritan/disclaimer review — make it a
   blocking gate per region.
9. **Verifiable impact:** Without a partner study, can adoption (O4) and freshness (O6) credibly
   stand in for outcome, and which partner could later run a real evaluation?

---

### Sources
- ILCOR publications / CoSTR: https://ilcor.org/publications · https://ilcor.org/uploads/Executive-Summary-2025-COSTR.pdf · https://cpr.heart.org/en/resuscitation-science/ilcor/ilcor-faqs
- AHA 2024 First Aid Guidelines: https://cpr.heart.org/en/resuscitation-science/2024-first-aid-guidelines
- ERC 2025 First Aid Guidelines: https://www.resuscitationjournal.com/article/S0300-9572(25)00264-3/fulltext
- IFRC International First Aid, Resuscitation & Education Guidelines 2025: https://www.ifrc.org/document/ifrc-international-first-aid-resuscitation-and-education-guidelines-2025 · PDF: https://www.ifrc.org/sites/default/files/2026-03/IFRC%20International%20First%20Aid,%20Resuscitation%20and%20Education%20Guidelines%202025.pdf
- IFRC First Aid app: https://play.google.com/store/apps/details?id=com.cube.gdpc.fa · https://apps.apple.com/us/app/first-aid-ifrc/id1312876691
- WHO Emergency Care Toolkit / Basic Emergency Care: https://www.who.int/teams/integrated-health-services/clinical-services-and-systems/emergency-and-critical-care/emergency-care-toolkit
- Hesperian / Where There Is No Doctor: https://en.hesperian.org/hhg/New_Where_There_Is_No_Doctor · https://en.wikipedia.org/wiki/Where_There_Is_No_Doctor
- St John Ambulance first-aid advice / accessible resources: https://www.sja.org.uk/first-aid-advice/ · https://www.sja.org.uk/get-advice/accessible-first-aid-resources/
- MedlinePlus First Aid (+ multi-language): https://medlineplus.gov/firstaid.html · https://medlineplus.gov/languages/firstaid.html
- WikEM / WikiDoc: https://wikem.org/ · https://en.wikipedia.org/wiki/WikEM
