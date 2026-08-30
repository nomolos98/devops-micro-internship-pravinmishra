# Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

![Assignment 4 screenshot](screenshots/ass04-gotto-job-Jira-project-overview.png)

---

### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

SOLO MODE

PO: I prioritized the website improvements that would make the job platform clearer, easier to use, and more trustworthy for users.

SM: I ensured the team followed the sprint process by confirming the requirements, tracking tasks, and preventing unnecessary scope changes.

Dev Lead: I reviewed the Gotto Job code and made a small front-end improvement without changing the backend.

DevOps Lead: I committed the update to Git, deployed it to the live environment, and tested the result in the browser.

---

# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

![Assignment 4 screenshot](screenshots/ass04-gotto-job-Jira-project-overview.png)
![Assignment 4 screenshot](screenshots/ass04-gotto-job-Jira-project-detail.png)

---

# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

![Assignment 4 screenshot](screenshots/ass04-gotto-job-backlog-epic-panel.png)

---

# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

![Assignment 4 screenshot](screenshots/ass04-gotto-job-backlog-six-stories.png)

---

#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

![Assignment 4 screenshot](screenshots/ass04-gotto-story-points-filled.png)

---

# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

![Assignment 4 screenshot](screenshots/ass04-gotto-job-backlog-showing-story-points-visible.png)

---

### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

## Story Point Estimates and Debate Notes

| Story | Final Estimate | Reason |
|---|---:|---|
| **Story 1: Hero tagline clarity** | **1** | Estimated as 1 because it mainly requires updating the hero text and checking its mobile wrapping. I briefly considered a higher estimate for responsive testing, but the implementation remains simple and low-risk. |
| **Story 2: Primary CTA color** | **1** | Estimated as 1 because it is primarily a CSS change involving the button background, hover state, and text readability. The review confirmed that it was straightforward and did not require major code changes. |
| **Story 4: Footer trust links** | **1** | Estimated as 1 because adding the About and Contact links is a small navigation and markup change. I considered the need to verify keyboard focus and routing, but the overall effort was still minimal. |
| **Story 5: Job card typography** | **2** | Estimated as 2 because it requires adjusting the job title styles and checking spacing, visual hierarchy, and responsive behavior. The discussion considered 1 point, but the additional layout verification made 2 more appropriate. |
| **Story 6: Remote badge** | **2** | Estimated as 2 because the work involves identifying remote listings, adding the `REMOTE` badge, and styling it without disrupting the card layout. In Solo Mode, I debated between 1 and 2, but the conditional display and testing justified 2 points. |
| **Story 7: Posted on date text** | **1** | Estimated as 1 because a static human-readable date can be added to each card with minimal markup and formatting work. I considered the need to check all cards, but it was not complex enough to require 2 points. |
| **Story 8: Advanced search labels** | **2** | Estimated as 2 because it involves updating multiple form labels or placeholders and verifying alignment, readability, and mobile responsiveness. I considered 1 point, but the changes across several search fields supported a 2-point estimate. |

## Reflection
The stories in this backlog are intentionally limited to UI only improvements. They do not involve backend development, database changes, authentication, complex API integration, or major infrastructure work. Therefore, estimates of 1 and 2 accurately reflect the expected effort.
The 1-point stories involve simple changes such as updating text, adding links, changing colors, or adding a button. 
The 2-point stories require changes across a component or page, together with responsive, visual, and accessibility testing
A 3-point story would normally involve large, complex logic, extensive testing, or greater deployment risk. A 3-point estimate could have been appropriate if the Remote Badge story required backend logic to identify remote jobs dynamically, or if the Advanced Search story required new search functionality connected to a database. Since those requirements are outside the current scope, no story was estimated at 3 points.

---

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

![Assignment 4 screenshot](screenshots/ass04-gotto-job-sprint1-selected-stories.png)

---

#### Screenshot 8 — One Story showing the Sub-tasks created

![Assignment 4 screenshot](screenshots/ass04-gotto-job-one-story-showing-subttasks.png)

---

# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

![Assignment 4 screenshot](screenshots/ass04-gotto-job-burndown-chart-page.png)

---

# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

![Assignment 4 screenshot](screenshots/ass04-gotto-story-done.png)

---

#### Screenshot 11 — Git commit output

![Assignment 4 screenshot](screenshots/ass04-gotto-story-commit.png)

---

#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

![Assignment 4 screenshot](screenshots/ass04-liive-url-browser.png)

---

# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

![Assignment 4 screenshot](screenshots/ass04-gotto-story-retro-notes.png)

---

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://lnkd.in/p/edimJuuR`

---

#### Screenshot 14 — Published LinkedIn post

![Assignment 4 screenshot](screenshots/ass04-linkedln-post.png)

---

# Submission Instructions

- Add all 14 required screenshots
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Team Mode or Solo Mode selected and all four roles documented (Screenshot 1 & Notes)
- [ ] Task 2: Team-managed Scrum project created with the required name (Screenshot 2)
- [ ] Task 3: UI improvement Epic created (Screenshot 3)
- [ ] Task 4: 6–8 Stories added under the Epic and ranked by value (Screenshots 4 & 5)
- [ ] Task 5: Story Points set (1, 2, or 3) with reasoning recorded (Screenshot 6 & Notes)
- [ ] Task 6: Sprint 1 created with Sprint Goal, 3–4 Stories, and Sub-tasks (Screenshots 7 & 8)
- [ ] Task 7: Burndown Chart opened (Screenshot 9)
- [ ] Task 8: One UI-only increment implemented, committed, deployed, and verified (Screenshots 10–12)
- [ ] Task 9: Retro comment with one Scrum pillar and one Scrum value (Screenshot 13)
- [ ] Task 10: Mandatory LinkedIn post published with the live URL, backlog refinement, Sprint planning, one shipped increment, proof, and Screenshot 14
- [ ] Full Name visible in required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
