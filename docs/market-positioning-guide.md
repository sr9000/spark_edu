# Market Positioning Guide for Spark ❇️

> A practical, decision-oriented guide to figure out **how to position Spark on the market** — even if the end goal is to give the app away for free.

This guide is written specifically for the current Spark stack (FastAPI + SQLite + React Native + Gemini/Groq + Cloudinary + Docker) and the constraints already visible in the repo (privacy-first, 152-ФЗ, single guest account, micro-VPS optimization).

---

## 0. Why "free" still needs positioning

A common trap: *"It's free, so I don't need to position it."*

Wrong. Positioning answers four questions, regardless of price:

1. **Who** is it for? (audience)
2. **What** does it replace / compete with? (alternative)
3. **Why** would they switch? (unique value)
4. **How** do they find it and start using it? (distribution)

If a free product can't answer these, it doesn't get adopted — it just sits on GitHub. The hardest part of a free P2P app is not the price (it's already zero), it's **distribution and trust**.

---

## 1. First decision: what kind of "free" do you mean?

There are at least five different things people call "free". Pick exactly one — they imply very different positioning.

| Mode | Example | What it means for you |
|---|---|---|
| **A. Free SaaS** (you host, users pay nothing) | Telegram, early Notion | You pay all the costs (AI, storage, VPS). Needs future monetization or sponsor. |
| **B. Freemium SaaS** | Duolingo, Notion today | Free tier + paid features. Most realistic default for Spark. |
| **C. Open-source, self-hosted** | Moodle, Mattermost | You give away the code; users run it. You can sell support/cloud later. |
| **D. Open-core** | GitLab, Sentry | OSS core + paid enterprise features. Common monetization for OSS. |
| **E. Free as a public good / non-profit** | Wikipedia, Khan Academy | Funded by grants/donations/foundation. Needs a legal entity and a story. |

> **Action:** Before reading further, write down on paper which of A–E you're choosing **and why**. This single choice removes 70% of downstream ambiguity.

---

## 2. Positioning framework (the 5-line statement)

Force yourself to fill in **one** version of this statement. If you can't, you don't have positioning yet — you have a product.

```
For   <specific audience>
who   <specific problem / job-to-be-done>,
Spark is a <category>
that   <unique value>,
unlike <named alternative>, which <its weakness>.
```

### Bad example (what NOT to write)
> *"For everyone who wants to learn, Spark is an AI-powered education platform that helps share knowledge, unlike other platforms."*

This says nothing. Every word is replaceable.

### Good examples (pick *one* direction)

- **Tutor-focused freemium:**
  > For private tutors preparing students for OGE/EGE, who waste hours rewriting the same explanations for each student, Spark is a mobile micro-lesson builder that turns rough notes into structured, shareable lessons in 2 minutes using AI, unlike Stepik, which is built for full-length courses and takes days to author.

- **Small-school on-prem:**
  > For private schools and tutoring centers in Russia under 152-ФЗ, who need a learning platform but can't store student data abroad, Spark is a self-hosted micro-learning app that runs on a single 1 GB VPS with all data on-premises, unlike Moodle, which is heavy, desktop-first, and has no AI authoring.

- **Free public good (P2P):**
  > For self-taught learners in regions with poor internet and no money for paid courses, Spark is a peer-to-peer micro-learning app where anyone can publish a 5-minute lesson, unlike YouTube, which is full of ads, has no progress tracking, and isn't structured for learning.

Notice: **each one names a different audience, a different alternative, and a different unique value.** You cannot serve all three at once with the same go-to-market.

---

## 3. Choosing the audience (ICP)

Two-sided platforms (authors + learners) have a chicken-and-egg problem. The way to break it is to pick **one tight initial audience** that brings *both sides* with them, then expand.

### Candidate ICPs and their trade-offs

| ICP | Brings authors? | Brings learners? | Pays? | Distribution channel |
|---|---|---|---|---|
| Private tutors (RU, EGE/OGE) | ✅ tutor = author | ✅ each tutor brings 5–30 students | Tutors will pay for time-saving | Tutor communities in Telegram/VK |
| Small online schools / "школы при экспертах" | ✅ owner is the author | ✅ they already have students | ✅ B2B | Direct sales, expert influencers |
| University TAs / department methodists | ⚠️ slow | ✅ captive audience | ❌ usually no budget | Pilot with one department |
| Corporate L&D in SMB | ⚠️ HR creates content | ✅ employees | ✅ B2B | LinkedIn, HR communities |
| Hobbyist micro-experts (cooking, fitness, code) | ✅ love sharing | ❌ hard to acquire | ❌ rarely | Social media, slow organic |
| Schoolchildren self-learners | ❌ they consume only | ✅ huge | ❌ parents pay | Hardest channel |

**Heuristic:** the best ICP is the one where **a single user brings both content and an audience** (tutors, school owners, expert-led schools).

### Picking exercise

Ask of each candidate ICP:

1. Can I **name 10 real people** in this group whom I could talk to next week?
2. Do they have **money or budget** (if your model is B/D, this matters)?
3. Is there a **channel** where ≥ 1000 of them already gather?
4. Can I demo Spark and have them say *"yes, I'd use this tomorrow"* — without me explaining the value for 20 minutes?

If any answer is "no", it's not your starting ICP. Move on.

---

## 4. Mapping the competitive landscape

Position relative to *named* alternatives, not abstract categories. For Spark, the real alternatives are:

### Direct competitors
- **Stepik** — closest analog in RU, has authoring, has AI now. *Their weakness:* built for long courses, web-first, slow authoring.
- **GetCourse / Skillspace / АнтиТренинги** — for course-business owners. *Their weakness:* expensive, heavy, not mobile-first, no AI authoring.
- **Moodle** — open-source LMS giant. *Their weakness:* desktop-era UX, no AI, painful to install/maintain, not micro-learning.

### Indirect but bigger competitors (the ones that actually take attention)
- **YouTube / Shorts / TikTok** — where micro-learning *actually* happens today. *Their weakness:* no progress tracking, no structure, ads, distractions.
- **Telegram channels + ChatGPT** — the modern self-learning loop. *Their weakness:* no curation, no authoring tools for non-AI experts, no accountability.
- **Notion / Obsidian Publish / Teletype** — where structured knowledge gets published. *Their weakness:* not interactive, no learning loop, no mobile UX.

### Adjacent-but-different
- **Quizlet / Anki** — spaced repetition, flashcards. Different category; can be a *partner* (export to Anki) rather than competitor.

### Positioning axes worth considering

Pick 2 axes where Spark is on the strong side. Examples:

- **Authoring speed** (Spark fast) vs **course depth** (Stepik deep)
- **Mobile-first** (Spark) vs **desktop-LMS** (Moodle)
- **Data locality / 152-ФЗ** (Spark on-prem) vs **foreign cloud** (Notion, Coursera)
- **Structured progress** (Spark) vs **chaotic feed** (YouTube/TikTok)
- **AI-assisted authoring** (Spark) vs **manual content** (most LMS)

> **Action:** Draw a 2×2 with the two axes you picked. Place Stepik, Moodle, YouTube, and Spark on it. If Spark ends up in the same quadrant as a giant — **change your axes**, you have no differentiation.

---

## 5. Distribution model decision tree

Use this to pick A–E from §1 in a structured way.

```
Q1. Do you have (or can you get) ≥ 1 year of runway to cover AI + infra costs without revenue?
    ├── YES → Q2
    └── NO  → C (OSS self-hosted) or B (Freemium with hard limits) — never A.

Q2. Is your ICP willing to pay (B2B, tutors, schools, corp L&D)?
    ├── YES → Q3
    └── NO  → C or E (non-profit / grant-funded). Pure free SaaS without funding will collapse.

Q3. Is data-locality / on-prem a real requirement for your ICP?
    ├── YES → D (open-core) or paid on-prem licenses. Spark's Docker setup already supports this.
    └── NO  → B (freemium SaaS) is the default.

Q4. Do you want long-term control of the codebase, or community contributions?
    ├── Control + monetization → B or D.
    └── Community + adoption first, money later → C.
```

### What this means concretely for Spark today

Given the repo state (Docker-ready, SQLite, single-VPS optimized, 152-ФЗ awareness, small team):

- **Most realistic primary mode:** **B (Freemium SaaS) + D (open-core / paid on-prem)** as a second track.
- **Least realistic:** A (free hosted SaaS for everyone) — variable AI/Cloudinary costs will kill it.
- **Strongest underused asset:** the existing Docker setup makes the on-prem path almost free to start.

---

## 6. The "free distribution" path (if that's the goal)

If the explicit goal is **"give away a good P2P app for free"**, you still need positioning, just of a different kind. Treat the project like an OSS product, not a SaaS.

### Free-distribution positioning checklist

- [ ] **Pick a license** (MIT / Apache 2.0 / AGPL). AGPL protects against someone forking and SaaS-ifying you; MIT maximizes adoption.
- [ ] **Define "who is it for"** in the README's first paragraph. Today the README talks about tech stack — that's not positioning.
- [ ] **One-line value prop at the top** of README. (See §2.)
- [ ] **Clear self-host quickstart** — `docker compose up` and you're running. Currently the repo is close, but `docker-compose.yml` and env-var setup need to be the first thing a new user sees.
- [ ] **Remove hardcoded URLs/IPs** in the React Native client (currently `192.168.88.163` is in CORS) — a free P2P app must be trivially deployable by anyone.
- [ ] **Replace mandatory Cloudinary** with a default that works without external accounts (local FS or MinIO). External paid services in a "free" project are friction.
- [ ] **Pick how AI works in self-hosted mode:** BYO-key (user supplies Gemini/Groq), local model (Ollama), or AI-optional. Without this decision, "free" becomes "free except you still need a paid API key", which alienates users.
- [ ] **Define a contribution path** (CONTRIBUTING.md, issues labeled `good first issue`).
- [ ] **Pick a distribution channel** for awareness (Habr post, Telegram channel — already exists, ProductHunt, Reddit r/selfhosted, awesome-selfhosted list).
- [ ] **Decide your sustainability story.** Free projects die from maintainer burnout, not from lack of users. Options: GitHub Sponsors, Boosty, future paid hosted tier, future paid support, grant.

### Anti-pattern: "free + maybe paid later"
Don't ship a free version *and* claim "we'll figure out monetization later". Either:
- Ship free + clearly-named **future paid features** (open-core), or
- Ship free + **donations only** (and accept slow growth), or
- Ship free + **paid hosted version from day one** (freemium).

Vague "free now, money later" frightens both users (worried about rug-pull) and contributors (worried about license bait-and-switch).

---

## 7. Pricing options (only if you chose B or D)

When/if you do charge, the three viable shapes for Spark are:

| Model | Who pays | Typical price | Fits Spark when |
|---|---|---|---|
| **AI quota** for authors | Author | 200–500 ₽/mo for N AI generations | Most authors, lowest barrier |
| **Pro for learners** | Learner | 200–400 ₽/mo (offline, no ads, advanced tracking) | Once content library is rich |
| **Org / on-prem license** | School/company | 10k–50k ₽/mo per org | When you have ≥ 1 case study |

Avoid: per-seat learner pricing in B2C (kills virality), one-time payments (no recurring revenue), and ads (incompatible with "education" brand and 152-ФЗ).

---

## 8. Putting it together — your worksheet

Fill this in. Each blank is one decision. Stop guessing the others until these are written down.

```
1. Distribution mode (A/B/C/D/E):  _______________________

2. ICP — one sentence, naming a real group:
   _____________________________________________________

3. Top alternative they use today (not Spark):
   _____________________________________________________

4. Why they would switch (one sentence, concrete):
   _____________________________________________________

5. Two positioning axes (Spark wins on both):
   axis 1: _____________________________________________
   axis 2: _____________________________________________

6. First channel to reach 100 of these users:
   _____________________________________________________

7. Sustainability plan for the first 12 months:
   _____________________________________________________

8. Smallest visible product change needed before going public:
   _____________________________________________________
```

When all 8 lines are filled and you'd be willing to read them out loud to a stranger without flinching — you have a position. Until then, you have a codebase.

---

## 9. Recommended next concrete steps for Spark

Based on the current state of the repo (April 2026):

1. **Choose the mode now**: a defensible default is **B + D** (freemium SaaS for tutors/expert-schools + paid on-prem for private schools). If the goal is *truly* free distribution, choose **C (OSS self-hosted)** with AGPL.
2. **Write the 5-line positioning statement** (§2) and put it at the top of README, replacing the current tech-stack-first opener.
3. **Pick an ICP** (§3) and find 10 real people in 1 week. Show them a 5-minute demo. If 7+ say "I'd use this", you have a market. If not, change the ICP, not the product.
4. **Fix the on-prem blockers** even if you don't sell on-prem yet — they also help OSS adoption: configurable backend URL in the RN client, optional Cloudinary, optional local AI.
5. **Stake a single channel** (one Telegram community, one tutor forum, one Habr article) and post a real demo. Free apps still need launches.
6. **Decide the AI cost question** (BYO-key vs hosted) before public launch — this is the single biggest hidden cost.

---

## 10. References & further reading

- April Dunford, *Obviously Awesome* — the canonical book on B2B positioning. The "5-line statement" in §2 is adapted from her template.
- Geoffrey Moore, *Crossing the Chasm* — for the ICP / beachhead concept used in §3.
- *The Mom Test* by Rob Fitzpatrick — for how to actually validate with the 10 real people in step 3.
- Joel Spolsky, *Strategy Letter V* — on commoditizing your complement (relevant to free-as-a-good-public-good).
- `awesome-selfhosted` on GitHub — the de-facto distribution channel for OSS self-hosted apps.
