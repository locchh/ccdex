# Software Development: Philosophies, Methodologies & Practices

This document covers the full landscape of how people think about and organize software development — from the broadest worldviews down to specific coding rules.

There are four levels, each narrower in scope than the one above:

```
Philosophy   — mindset & values (Systems Thinking, Lean, Agile, DevOps, SOLID, DRY…)
  └── Methodology — how you organize your team & process (Scrum, Kanban, Waterfall…)
        └── Practice — specific techniques you apply while coding (TDD, pair programming…)
              └── Design approach — how you model and structure code (DDD, SoC…)
```

These don't compete — they operate at different levels and **stack**:

```
Systems Thinking  (philosophy — broadest worldview)
  └── Lean        (philosophy — eliminate waste across any system)
        └── Agile (philosophy — how teams respond to change)
              └── DevOps        (philosophy — dev-to-production pipeline)
              └── Scrum/Kanban  (methodology — concrete process for Agile teams)
                    └── TDD/BDD (practice — how you write code within the process)
                          └── DDD / SoC / SOLID / DRY / KISS / YAGNI
                              (design approaches & coding principles)
```

---

## Philosophies

A **philosophy** is the highest level — it defines *how you think* about building software. It doesn't tell you which tools to use or what meetings to run. It shapes your mindset and values, which then influence the methodologies and principles you choose.

Below are the major philosophies in software, sorted from **largest scope** (broadest worldview) down to **smallest scope** (affects a single line of code).

---

### 1. Systems Thinking
**Scope: Universal worldview — affects how you understand any complex system**

The root philosophy that underpins Lean, Agile, and DevOps. The idea: **a system's behavior emerges from the interactions between its parts, not just the parts themselves**. You cannot understand or fix a system by looking at each piece in isolation.

In software, this means: optimizing one team, one service, or one phase in isolation often makes the whole system *worse*. A bottleneck in deployment makes fast development pointless. A slow QA process makes fast coding pointless.

**Key idea:** Always ask "what does the whole system look like?" before optimizing any one part.

**Scope of apply:** The broadest — applies to organizations, teams, software architecture, and society. Every other philosophy on this list is a specific application of Systems Thinking to a narrower domain.

**Origin:** Peter Senge's *The Fifth Discipline* (1990); W. Edwards Deming's work on quality in manufacturing.

---

### 2. Lean Philosophy
**Scope: Organization & team — affects how work flows and waste is eliminated**

Adapted from Toyota's manufacturing system (1950s). Lean is Systems Thinking applied to production: **most time in any system is waste, not value-adding work**. Find it, eliminate it.

Seven principles:
1. Eliminate waste
2. Amplify learning
3. Decide as late as possible
4. Deliver as fast as possible
5. Empower the team
6. Build integrity in
7. See the whole *(the Systems Thinking principle, embedded directly)*

**Scope of apply:** How organizations and teams manage work, make decisions, and measure value. Lean is the philosophical foundation that Agile, Kanban, and DevOps all borrowed from.

**Relationship to Systems Thinking:** Lean *is* Systems Thinking applied to manufacturing and knowledge work. "See the whole" (principle 7) is literally Systems Thinking.

---

### 3. Agile Philosophy
**Scope: Team-wide — affects how a team plans and works together**

A response to rigid, slow, plan-heavy processes. Defined in the [Agile Manifesto (2001)](https://agilemanifesto.org/) by 17 developers who borrowed heavily from Lean. Four core values:

1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

Agile doesn't tell you *how* to work — it tells you *what to value*. Scrum, Kanban, XP, and SAFe are all concrete methodologies that apply the Agile philosophy.

**Scope of apply:** How a team plans, communicates, and delivers. Does not dictate how individual code is written.

**Not to be confused with:** Agile ≠ Scrum. Scrum is one way to *implement* Agile. You can be "Agile" without doing Scrum.

**Relationship to Lean:** Lean came first (1950s). Agile (2001) is Lean thinking applied specifically to software teams.

---

### 4. DevOps Philosophy
**Scope: Organization-wide — affects how development and operations teams collaborate**

The idea that **development teams and operations teams should not be separate**. Traditionally, developers wrote code and "threw it over the wall" to an operations team to deploy and maintain. DevOps tears down that wall.

- Developers own their code all the way to production
- Everything is automated: testing, deployment, monitoring
- Failure is expected and planned for — you build resilient systems, not fragile ones

**Key values:** Collaboration, automation, continuous delivery, shared responsibility.

**Scope of apply:** How engineering organizations are structured, how code goes from a developer's laptop to production. Narrower than Agile — Agile is about *any* team process, DevOps is specifically about the dev-to-production pipeline.

**Relationship to Agile:** DevOps extends Agile thinking into the operations domain. Agile fixed planning and development. DevOps fixed deployment and operations.

**Famous adopters:** Netflix, Amazon, Google. Amazon famously deploys to production thousands of times per day.

---

### 5. Unix Philosophy
**Scope: System design — affects how software components are designed**

Formulated by Ken Thompson and Doug McIlroy at Bell Labs in the 1970s when building Unix. Three rules:

1. **Write programs that do one thing and do it well**
2. **Write programs to work together**
3. **Write programs that handle text streams**, because that is a universal interface

**Scope of apply:** How you design software systems and components. A program (or function, or service) should have a single, clear purpose. If it does too many things, split it up.

**Modern relevance:** Microservices architecture is the Unix Philosophy applied to distributed systems — each service does one thing and communicates with others through simple interfaces.

**Famous adopters:** The entire Unix/Linux ecosystem. Tools like `grep`, `awk`, `curl` each do one thing perfectly and compose with others via pipes.

---

### 6. Separation of Concerns (SoC)
**Scope: System and code design — affects how you divide a system into parts**

**SoC = Separation of Concerns**

Different parts of a system should be responsible for different things, and those responsibilities should not overlap. First described by Edsger Dijkstra in 1974.

In practice:
- A web app separates UI, business logic, and database access (the classic **MVC** pattern — Model, View, Controller)
- A function that fetches data should not also format it for display
- A module that handles payments should not also handle user authentication

**Scope of apply:** Architecture (how you split a system into layers or services) down to individual functions.

**Relationship to Unix Philosophy:** SoC is the general principle; Unix Philosophy is one specific application of it. Unix says: separate programs. SoC says: separate *any* concerns, at any level.

---

### 7. Convention over Configuration
**Scope: Framework and tool design — affects how much you need to configure things**

**CoC = Convention over Configuration**

Popularized by Ruby on Rails (2004). The idea: instead of requiring developers to configure every detail, a framework should make *sensible default decisions* and only require configuration when you want to deviate from the norm.

**Example:** In Rails, if you have a `User` model, the framework automatically assumes the database table is called `users`, the controller is `UsersController`, and the views are in `app/views/users/`. You don't configure any of this — it just works by convention.

**Scope of apply:** Framework and tool design. Affects how much setup and decision-making a developer needs to do before writing actual product code.

**Why it matters:** Without conventions, developers waste enormous time making trivial decisions. With conventions, they can focus on what makes their app unique.

**Famous adopters:** Ruby on Rails, Django, Laravel, Next.js — all built on strong conventions.

---

### 8. SOLID Principles
**Scope: Code design — affects how classes and modules are structured**

Five principles for writing clean, maintainable object-oriented code, coined by Robert C. Martin ("Uncle Bob"):

| Letter | Full name | Plain meaning |
|---|---|---|
| **S** | Single Responsibility Principle | A class should do one thing only |
| **O** | Open/Closed Principle | Open for extension, closed for modification |
| **L** | Liskov Substitution Principle | Subclasses should be replaceable for their parent class |
| **I** | Interface Segregation Principle | Don't force a class to implement interfaces it doesn't use |
| **D** | Dependency Inversion Principle | Depend on abstractions, not concrete implementations |

**Scope of apply:** How individual classes and modules are written. Smaller scope than Agile or Lean — these are rules for the code itself, not the team process.

**Why it matters:** Code that violates SOLID becomes hard to change, test, and understand over time.

---

### 9. Fail Fast
**Scope: Code and system design — affects how errors are handled**

Don't let errors silently propagate through a system. **Surface them as early and loudly as possible** — at startup, at the boundary of a function, at the edge of a service — so they are caught before they cause larger, harder-to-debug problems downstream.

**Example:** A function that expects a non-null user ID should throw an error immediately if it receives null — not pass null along silently until something crashes five steps later with a confusing error message.

**Scope of apply:** Individual functions, services, and system startup sequences.

**Why it matters:** Silent failures are the hardest bugs to debug. Fail Fast turns invisible errors into visible ones immediately.

**Relationship to SOLID:** The Single Responsibility Principle (S in SOLID) makes Fail Fast easier — when a function does one thing, it's clear what it should validate and when to fail.

---

### 10. DRY Principle
**Scope: Code — affects how you handle duplication in your codebase**

**DRY = Don't Repeat Yourself**

Coined by Andrew Hunt and David Thomas in *The Pragmatic Programmer* (1999):

> *"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."*

If the same logic exists in two places, and one changes, you must remember to change the other — and you will eventually forget. DRY says: extract it, name it, reference it from one place.

**Scope of apply:** Individual code — functions, modules, configuration.

**Common mistake:** DRY is often misunderstood as "never copy-paste code." It's actually about *knowledge* duplication, not just textual duplication. Sometimes two pieces of code look the same but represent different concepts — forcing them into one function is wrong.

---

### 11. KISS Principle
**Scope: Universal — affects every design decision at every level**

**KISS = Keep It Simple, Stupid** (sometimes softened to *Keep It Simple and Straightforward*)

The simplest solution that works is almost always the best one. Complexity is a liability — it makes code harder to read, test, debug, and change.

**Scope of apply:** Every level — system architecture, class design, function implementation, variable naming. The most universally applicable principle on this list.

**Famous quote:** *"Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it."* — Brian Kernighan

---

### 12. YAGNI Principle
**Scope: Code and product — affects what you decide to build**

**YAGNI = You Aren't Gonna Need It**

Originated in XP (Extreme Programming). Don't build features or abstractions "just in case" you might need them later. Build what you need *now*, and add more when you actually need it.

**Scope of apply:** Both product decisions (don't build the feature nobody asked for yet) and code decisions (don't write the abstraction layer you might need someday).

**Why it matters:** Most "future-proofing" code never gets used, but it does get in the way of understanding the codebase and making changes today.

**Relationship to KISS:** YAGNI and KISS reinforce each other. KISS says keep things simple. YAGNI explains *why* people add unnecessary complexity — because they're guessing about future needs.

---

### Summary: Scope at a Glance

```
Systems Thinking        ████████████████████████  Universal worldview — the whole system
Lean                    ██████████████████████    Organization + team — eliminate waste
Agile                   ████████████████████      Team — how to plan and deliver
DevOps                  ██████████████████        Org structure — dev-to-production pipeline
Unix Philosophy         ████████████████          System design — how components interact
Separation of Concerns  ██████████████            System + code — how to divide responsibilities
Convention over Config  ████████████              Framework design — reduce trivial decisions
SOLID                   ██████████                Code design — how classes are structured
Fail Fast               ████████                  Code + system — surface errors early
DRY                     ██████                    Code — eliminate knowledge duplication
KISS                    ████████████████████      Universal reminder — applies at every level
YAGNI                   ██████                    Code + product — build only what's needed now
```

**Key insight:** These philosophies don't conflict — they work at different levels and they *stack*. A team can simultaneously follow Systems Thinking (worldview), apply Lean + Agile (team process), adopt DevOps (delivery pipeline), and write code that follows Unix Philosophy, SOLID, DRY, KISS, and YAGNI — all at the same time.

---

## Overview of Methodologies

Methodologies are concrete processes — they tell you *how* to organize your team and your work day-to-day. This is different from philosophies (which tell you *what to value*) and practices (which tell you *how to write code*).

| Methodology | Approach | Best for |
|---|---|---|
| Waterfall | Linear — one phase at a time, no going back | Fixed requirements, unlikely to change |
| V-Model | Linear — like Waterfall with paired testing at each phase | Safety-critical systems (medical, aerospace) |
| RUP | Iterative — structured phases with heavy documentation | Enterprise projects with formal governance |
| Scrum | Iterative (Agile) — short sprints, fixed roles and ceremonies | Most teams, most projects |
| XP | Iterative (Agile) — fast feedback, rigorous coding practices | Teams prioritizing code quality |
| SAFe | Iterative at scale (Agile) — Scrum coordinated across many teams | Large organizations, 50–500+ engineers |
| Kanban | Continuous flow (Agile) — no sprints, limit work in progress | Support, maintenance, unpredictable workloads |
| Shape Up | Fixed cycles — 6-week bets, no backlog | Small autonomous product teams |

> **Not in this table:** Lean, TDD, BDD, and DDD are covered in the **Philosophies** section above — they define *how to think*, not *how to run your process*.

---

## 1. Waterfall

**Full name:** Waterfall Model

**The idea:** Do everything in order, one phase at a time. You cannot move to the next phase until the current one is fully complete.

```
Requirements → Design → Development → Testing → Deployment → Maintenance
```

**Analogy:** Building a house. You lay the foundation before the walls, walls before the roof. You can't go back and change the foundation once the walls are up (without enormous cost).

**When to use it:** When requirements are very clear and unlikely to change — for example, a government contract with a fixed specification.

**When NOT to use it:** When you're building a product and expect to learn and change your mind along the way (which is most software).

**Famous examples:**
- **NASA Space Shuttle software** — Mission-critical flight software built with strict sequential phases and exhaustive documentation
- **Healthcare systems** — Hospital record systems procured by governments under fixed contracts
- **Microsoft Windows (early versions)** — Windows NT and early Windows releases used Waterfall-style planning with long multi-year cycles

**Connection to AI tools:** Spec Kit borrows Waterfall's discipline — write the full spec before writing any code.

---

## 2. V-Model

**Full name:** Verification and Validation Model

**The idea:** An extension of Waterfall where each development phase is paired with a corresponding testing phase. The shape of the process looks like a "V."

```
Requirements ←————————————→ Acceptance Testing
   Design ←————————————→ System Testing
      Architecture ←————→ Integration Testing
         Coding ←————→ Unit Testing
```

**Analogy:** For every decision you make, you also write down how you'll prove it worked. Like a checklist: "I said the bridge can hold 10 tons — here's how I'll test that."

**When to use it:** Safety-critical software — medical devices, aviation systems, nuclear plants — where you must prove correctness at every level.

**Famous examples:**
- **Airbus flight control systems** — Every requirement maps directly to a test case; nothing ships without verified proof
- **Medical device firmware** (pacemakers, insulin pumps) — FDA regulations require traceability from requirement to test
- **Nuclear plant control software** — Correctness at every level is legally required, not optional

**Connection to AI tools:** Not directly used by any of the four tools, but the principle (every spec should be verifiable) is related to BDD and Spec Kit's clarification step.

---

## 3. Scrum

**Full name:** Scrum (originally a rugby term — a tight formation to restart play)

**The idea:** Break work into short cycles called **sprints** (usually 1–2 weeks). At the end of each sprint, you have working software. A small team works from a **backlog** (a prioritized list of work).

**Key roles:**
- **Product Owner (PO)** — decides what to build and in what order
- **Scrum Master (SM)** — keeps the process running smoothly, removes blockers
- **Developer** — builds the thing

**Key ceremonies:**
- **Sprint Planning** — decide what to work on this sprint
- **Daily Standup** — short daily sync (what did I do, what will I do, any blockers?)
- **Sprint Review** — show what was built
- **Retrospective** — how can we improve as a team?

**Analogy:** Instead of planning a year-long road trip in detail upfront, you plan week by week. After each week, you adjust based on what you learned.

**When to use it:** Most software teams. It's the most widely adopted agile methodology in the industry.

**Famous examples:**
- **Spotify** — Built its entire engineering culture on Scrum squads (teams), then evolved into the famous "Spotify Model"
- **Google** — Uses Scrum-based sprints across many product teams
- **Amazon** — Two-pizza teams (small enough that two pizzas can feed the team) running sprints
- **Salesforce** — Manages thousands of engineers using Scrum at scale

**Connection to AI tools:** BMAD-METHOD is directly inspired by Scrum — it has a PM (Product Manager, similar to Product Owner), a Scrum Master agent, Developer agents, and produces stories and epics (Scrum artifacts).

---

## 4. Kanban

**Full name:** Kanban (Japanese: 看板, meaning "signboard" or "billboard")

**The idea:** Visualize all your work on a board, limit how much work is in progress at once (called **WIP limits**), and let work flow continuously — no fixed sprints.

```
| To Do | In Progress (max 3) | Review | Done |
|-------|---------------------|--------|------|
| Task A | Task C             | Task E | Task F |
| Task B | Task D             |        | Task G |
```

**Analogy:** A restaurant kitchen. Food orders come in continuously. The chef doesn't say "we only cook on Tuesdays" — work flows through the kitchen as capacity allows.

**When to use it:** Support teams, bug fixing, maintenance work — anything where new tasks arrive constantly and unpredictably.

**Famous examples:**
- **Microsoft (Visual Studio Team)** — One of the earliest large-scale software Kanban adoptions, documented publicly by David Anderson
- **Zara (fashion supply chain)** — Not software, but Kanban's origin: Toyota's physical card system that Zara adapted to replenish store inventory in real time
- **GitHub** — Uses Kanban-style project boards for their own internal engineering work

**Connection to AI tools:** Not directly implemented by the four tools, but GSD's backlog management is Kanban-influenced.

---

## 5. SAFe

**Full name:** Scaled Agile Framework

**The idea:** Take Scrum/Agile and make it work for large organizations with 50–500+ people across many teams. Adds coordination layers on top of individual team Scrum.

**Key levels:**
- **Team** — individual Scrum teams working in sprints
- **Program** — multiple teams synchronized into a longer cycle called a **Program Increment (PI)**, typically 10 weeks
- **Portfolio** — strategic alignment across all programs

**Analogy:** Scrum is a single restaurant kitchen. SAFe is a restaurant chain — each location runs its own kitchen, but they're all aligned on the same menu and brand standards.

**When to use it:** Large enterprises where many teams need to coordinate and deliver together.

**Famous examples:**
- **Lego** — Used SAFe to coordinate 30+ teams building digital products simultaneously
- **Cisco** — Adopted SAFe across its engineering org to align hundreds of teams
- **US Air Force** — Adopted SAFe for large government software programs
- **John Deere** — Uses SAFe to coordinate software development across hardware and software teams

**Connection to AI tools:** BMAD's scale-adaptive intelligence and modular ecosystem were designed with SAFe-like complexity in mind.

---

## 6. XP

**Full name:** Extreme Programming

**The idea:** Take good coding practices and turn them up to the extreme. XP is defined by a set of specific technical practices:

- **Pair programming** — two developers share one keyboard; one writes, one reviews in real time
- **Test-Driven Development (TDD)** — write tests before writing code (see Practices & Design Approaches section)
- **Continuous Integration (CI)** — merge and test code multiple times per day
- **Small releases** — ship frequently, in tiny increments
- **Refactoring** — continuously improve code quality as you go
- **Simple design** — always use the simplest design that works

**Analogy:** Instead of waiting until the end of a long road trip to check if you're going the right way, you check the map every few minutes.

**When to use it:** Teams that care deeply about code quality and want very fast feedback loops.

**Famous examples:**
- **Chrysler Comprehensive Compensation System (C3)** — The project where Kent Beck invented XP in 1996; it's the original XP project
- **Facebook (early years)** — "Move fast and break things" era used many XP practices: continuous integration, small releases, refactoring
- **Pivotal Labs** — The consulting firm famous for practicing strict XP (pair programming all day, every day) with client teams

**Connection to AI tools:** GSD's philosophy is XP-influenced — small, clean contexts, frequent execution, and continuous refinement.

---

## 7. Shape Up

**Full name:** Shape Up (created by Basecamp, described in their free book *Shape Up* by Ryan Singer)

**The idea:** Work in **6-week cycles** with a structured process:

1. **Shape** — a small senior group defines the *problem and rough solution* (not detailed specs) before any team works on it
2. **Bet** — leadership explicitly *bets* on which shaped work to fund this cycle (no backlog piling up)
3. **Build** — small teams (1–2 people) have full autonomy to figure out the implementation within 6 weeks
4. **Cool-down** — 2 weeks after each cycle for bug fixes, experiments, and rest

**Key difference from Scrum:** There is **no backlog**. Ideas that don't get bet on in a cycle are discarded, not queued. "If it's not worth betting on now, it probably never was."

**Analogy:** Instead of a restaurant with an ever-growing order queue, the chef decides at the start of each week exactly what dishes will be made — and only those. Anything not on the menu this week simply isn't served.

**When to use it:** Small, autonomous product teams that want to avoid the chaos of a never-ending backlog and want meaningful, focused work cycles.

**Famous examples:**
- **Basecamp** — Shape Up was invented here and is still how the Basecamp and HEY products are built today
- **37signals** — Same company as Basecamp; all products use Shape Up
- **Podia** — Online course platform that publicly adopted Shape Up and documented their transition from Scrum

**Connection to AI tools:** The "shaping" concept (define the problem and constraints before the team touches it) is similar to how Spec Kit's `constitution` + `specify` steps work.

---

## 8. RUP

**Full name:** Rational Unified Process (developed by Rational Software, acquired by IBM)

**The idea:** An iterative software development process that is more structured and document-heavy than Scrum, but more flexible than Waterfall. It defines four phases:

1. **Inception** — understand the scope, feasibility, and risks
2. **Elaboration** — define the architecture and resolve major risks
3. **Construction** — build the system iteratively
4. **Transition** — deploy to users, gather feedback, finalize

Unlike Waterfall, you iterate within each phase. Unlike Scrum, you still produce heavy documentation and formal artifacts.

**Analogy:** Building a skyscraper. You first confirm the project makes sense (Inception), then design the structural frame (Elaboration), then fill in all the floors (Construction), then hand over the keys (Transition).

**When to use it:** Large enterprise or government projects where formal documentation, traceability, and governance are required.

**Famous examples:**
- **IBM WebSphere** — Developed internally at IBM using RUP; IBM was both the creator of the process and the primary user
- **Siemens enterprise software** — Large industrial software systems built under RUP for formal traceability
- **US Department of Defense projects** — Many DoD software contracts in the 2000s mandated RUP-compliant processes

**Connection to AI tools:** BMAD's multi-phase structure (brainstorm → PRD → architecture → stories → dev loop) loosely mirrors RUP's four phases, but executed with AI agents instead of human teams.

---

## Practices & Design Approaches

These are **not methodologies** — they don't tell you how to run your team or plan your sprints. They tell you *how to write code* (practices) or *how to model and structure it* (design approaches). They sit inside any methodology.

---

### TDD — Test-Driven Development (Practice)

**Full name:** Test-Driven Development

**The idea:** Write a failing test first, then write just enough code to make it pass, then clean up the code. Repeat.

```
Red → Green → Refactor
(write failing test) → (make it pass) → (clean it up)
```

**Analogy:** Imagine writing the exam questions before studying. You study specifically to pass those questions — and you know exactly when you're done.

**When to use it:** Any project where correctness matters. Works inside any methodology — Scrum, Kanban, XP, Shape Up.

**Famous examples:**
- **Ruby on Rails** — DHH built Rails with TDD as a core practice; made TDD mainstream in web development
- **Django** — Python web framework, built and maintained with TDD throughout
- **JUnit / RSpec** — The testing frameworks themselves were built TDD-first

**Connection to AI tools:** Compatible with all four tools. Spec Kit's task files can include test scenarios.

---

### BDD — Behavior-Driven Development (Practice)

**Full name:** Behavior-Driven Development

**The idea:** An extension of TDD where tests are written in plain English using **Given-When-Then**, making them readable by both developers and non-technical stakeholders.

```
Given: a user is logged in
When: they click "Delete Account"
Then: their account is removed and they receive a confirmation email
```

**Analogy:** TDD asks "does the code work?" BDD asks "does the code do what the user actually needs?"

**Common tool:** Gherkin (the language), used with Cucumber or Behave.

**When to use it:** When you want specs and tests to be the same document — readable by both business and engineering.

**Famous examples:**
- **GOV.UK** — Non-technical policy teams can read and validate test scenarios
- **Cucumber** — Built specifically to enable BDD; used by Typeform, Badoo, and thousands of others
- **Salesforce** — Uses BDD for platform acceptance testing

**Connection to AI tools:** BDD's "spec as plain English" idea is the philosophical ancestor of Spec Kit's spec-first approach.

---

### Lean Software Development (Philosophy applied as practice)

**Full name:** Lean Software Development (adapted from Toyota Production System)

**The idea:** Seven principles borrowed from Toyota's manufacturing process, applied to software:

1. **Eliminate waste** — don't build features nobody needs
2. **Amplify learning** — get feedback early and often
3. **Decide as late as possible** — defer irreversible decisions
4. **Deliver as fast as possible** — speed reduces risk
5. **Empower the team** — decisions by those closest to the work
6. **Build integrity in** — quality is built in, not tested in at the end
7. **See the whole** — optimize the whole system, not just parts

**Analogy:** Toyota's biggest waste wasn't slow workers — it was waiting, inventory, and defects. Same in software: most time is wasted waiting for approvals, building unused features, or fixing preventable bugs.

**When to use it:** Its principles are universal. Most Agile methodologies (Scrum, Kanban, XP) have Lean at their core. Also covered in depth in the Philosophies section above.

**Famous examples:**
- **Toyota** — The origin; became the world's most efficient car manufacturer
- **Spotify** — Small autonomous squads, eliminate handoffs, continuous deployment
- **Netflix** — "Highly aligned, loosely coupled"; minimize process, maximize flow

**Connection to AI tools:** GSD is the most Lean-influenced — its design eliminates context rot (waste) and delivers in small, clean increments.

---

### DDD — Domain-Driven Design (Design Approach)

**Full name:** Domain-Driven Design (Eric Evans, 2003)

**The idea:** The most important thing in a complex system is understanding the *domain* — the real-world problem space (banking, healthcare, e-commerce). Your code should reflect that domain using the same language domain experts use.

**Key concepts:**
- **Ubiquitous Language** — developers and business experts use the *exact same words*. No translation layer.
- **Bounded Context** — a boundary where a specific model applies. "Order" means something different in Shipping vs. Billing.
- **Entities and Value Objects** — ways of modeling real-world things in code
- **Aggregates** — clusters of objects treated as a single unit

**Analogy:** A doctor and a developer working on a hospital system should both call it "Patient Admission" — not the developer calling it `UserCheckIn`.

**When to use it:** Complex business domains. Overkill for simple apps.

**Famous examples:**
- **Uber** — Bounded contexts: Rides, Payments, Driver Management, Notifications
- **SoundCloud** — Migrated monolith to microservices using DDD bounded contexts as service boundaries
- **LinkedIn** — Separate domain models for social graph, job matching, and feed ranking

**Connection to AI tools:** Agent OS is DDD-influenced — agents must first understand the standards and patterns of your codebase (your domain) before writing good code.

---

## How These Relate to the Four AI Tools

The four tools in this project don't invent new methodologies — they *apply* existing ones to AI-assisted development:

| AI Tool | Inspired by | Why |
|---|---|---|
| **GSD** | Lean + XP | Eliminate waste (context rot), small clean increments, fast execution |
| **BMAD-METHOD** | Scrum + SAFe | Specialist agent roles mirror Scrum team roles; scale-adaptive like SAFe |
| **Spec Kit** | Waterfall spec discipline + BDD | Write the full spec before coding; specs are human-readable like BDD scenarios |
| **Agent OS** | DDD | Agents must know your domain (standards, patterns) before they can write good code |

The key insight: **methodology matured over decades of human teams learning painful lessons**. AI tools are now encoding those lessons into automated workflows so you get the benefits without needing a large team or a formal process certification.

---

## Glossary

| Term | Full form | Plain meaning |
|---|---|---|
| BDD | Behavior-Driven Development | Write tests as plain English user stories |
| CI | Continuous Integration | Merge and test code many times per day |
| DDD | Domain-Driven Design | Model your code around the real-world business domain |
| PI | Program Increment | A ~10-week synchronized cycle across multiple Scrum teams (SAFe) |
| PM | Product Manager / Product Owner | The person who decides what gets built |
| PRD | Product Requirements Document | A document describing what the product should do |
| RUP | Rational Unified Process | IBM's structured iterative development process |
| SAFe | Scaled Agile Framework | Agile practices scaled up for large organizations |
| SDD | Spec-Driven Development | Write the specification before writing any code |
| SM | Scrum Master | The person who keeps the Scrum process running |
| TDD | Test-Driven Development | Write tests before writing code |
| WIP | Work In Progress | Tasks currently being worked on (Kanban limits this number) |
| XP | Extreme Programming | Agile methodology focused on rigorous coding practices |
