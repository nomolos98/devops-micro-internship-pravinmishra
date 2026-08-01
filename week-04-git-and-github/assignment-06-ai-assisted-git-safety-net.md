# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

![Assignment 6 screenshot](screenshots/ass06-git-remote-new-branch.png)

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

creating a separate branch keeps your changes away from the main project so you can work safely without breaking anything. Also it makes the Pull Request cleaner because it only shows the changes for that specific task.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

![Assignment 6 screenshot](screenshots/ass06-git-status-staged-feature-ai-pr-ready.png)

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

A fake key is used so it doesn't expose any sensitive information and lead to security breaches. It also lets learners focus on the process of using keys without worrying about access permissions, expiration, or security problems.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![Assignment 6 screenshot](screenshots/ass06-hooks-pre-commit-vscode.png)

---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![Assignment 6 screenshot](screenshots/ass06-git-config-core-hookspath.png)

---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

hooks/pre-commit is tracked in the repo so everyone on the team gets the same rule set, while .git/hooks/ is local to one clone and is not versioned or shared with other contributors. That makes the checked-in hook portable, reviewable, and consistent across contributors, whereas a file only in .git/hooks/ would exist only on one developer’s machine

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

They intercept different layers of activity, but they serve the same safety goal.

**What each intercepts**
- `hooks/pre-commit` intercepts a Git commit right before the commit is finalized. It inspects staged files and blocks the commit if it finds something risky, like a secret pattern or an oversized file.

- `PreToolUse` intercepts a tool action before the tool runs. In your earlier setup, it acted as a checkpoint before potentially dangerous operations, such as write actions during planning or destructive infrastructure commands like terraform destroy.

**What they have in common**
- Both are preventive guardrails and enforce policy

- Both can stop risky actions and block automation when the action violates a rule, then force a review

- Both are meant to keep workflows predictable and safer, especially where mistakes could leak secrets or change infrastructure unexpectedly.

- In summary, hooks/pre-commit protects the Git repository and its history. While PreToolUse protects the tooling workflow and runtime actions.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

![Assignment 6 screenshot](screenshots/ass06-git-commit-rejected-blocked.png)

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line that matches is the one inside the grep -qE: AKIA[0-9A-Z]{16}

It matched because the fake key AKIAABCDEFGHIJKLMNOP has the exact AWS access key shape that regex looks for: it starts with AKIA, followed by 16 characters, each of which is an uppercase letter or digit, which is the typical AWS access key ID format the hook is trying to catch

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

Yes, a hook like this could miss a secret if it is stored in a variable name that does not look like a known secret pattern, because this rule only searches for specific text signatures such as AKIA... or private-key headers.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

![Assignment 6 screenshot](screenshots/ass06-skill-frontmatter.png)

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

![Assignment 6 screenshot](screenshots/ass06-pr-ready-output-risky-file.png)

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready has Bash and Read because its job is to inspect staged changes, not modify them. The skill’s own description says it should review git diff --cached and git status, report risks, and draft a PR title/description; it explicitly says never to commit, push, open a PR, or edit files, so write capability is unnecessary.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

They did not flag the exact same things.

The hooks/pre-commit hook blocked the commit as it caught the credential-shaped string itself: the pattern in scripts/notify.sh, because its job was to scan staged content for secret-like text and oversized files. The /pr-ready check also noticed that same secret-shaped string, but it additionally flagged the DEBUG: echo as a risky debug print and framed the change as a PR-quality review item rather than a hard commit blocker.

**What one caught that the other didn't**
/pr-ready caught the debug print risk.

hooks/pre-commit did not explicitly report the debug echo in the output you showed; it only blocked on the secret pattern.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

![Assignment 6 screenshot](screenshots/ass06-git-commit-no-blocked-message.png)

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

![Assignment 6 screenshot](screenshots/ass06-pr-ready-clean-risk-report.png)

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the credential line that contains the secret from scripts/notify.sh and replaced it with a normal script message. There is no secret check to match and no debug-style output that prints a token or credential-like value.

This task demonstrates the Human Act, Verify stage of the Agentic Loop. The automated tools did not fix the problems only identified them.


---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

![Assignment 6 screenshot](screenshots/ass06-pull-request-show-my-base-repo.png)
![Assignment 6 screenshot](screenshots/ass06-github-pull-request-show.png)


---

#### PR Link

`https://github.com/nomolos98/devops-micro-internship-interviews/pull/1`

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I would have changed any part of the draft that did not exactly match the staged files, especially the PR title, the description of what changed, and any risk notes. The reason is that AI drafts can be close but still overstate, understate, or generalize the change, and the final PR text should reflect the real diff you are about to submit

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

If copied blindly, the PR could describe the wrong files, the wrong intent, or the wrong risk level. That can confuse reviewers, make the change look broader than it is, or even miss a security concern that should be mentioned explicitly.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

The PR needs to target your own fork because the work is happening in your repository copy and your branch namespace. The shared upstream repository usually should not receive direct pushes from every contributor; instead, your fork is where you stage your branch, and then you propose the change back to upstream through a PR.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Gather: checking the staged diff, running the status check, and reviewing the hook output. These steps collect the raw facts about what is actually changing.
---

**2. Which step(s) represent Analyze?**

Analyze: the AI review step that reads the staged changes and drafts the PR title, description, and risk report. This is where the information is interpreted and turned into a recommendation.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Human Act: you run git commit, git push, and open the PR. A human must do this because those actions are the final authorization points, and they represent an intentional decision to publish changes rather than just inspect them.

---

**4. Which step is Verify?**

Verify: re-running the review after the script was cleaned up and confirming that the staged files are now clean. This checks whether the earlier problem was actually fixed before publication.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

You need both because they solve different problems. The fixed-rule hook is fast and deterministic for obvious policy violations like secret-shaped strings, while the AI skill is better at contextual review, catching mixed concerns, debug text, and whether the PR story matches the actual diff.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

`https://www.linkedin.com/posts/solomonanichebe_dmibypravinmishra-devops-git-share-7486361979255685121-09xr/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAXBpdEBaUln31DVzGUPS7Q7mpZjlUYg8QY`

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

- AI is a strong assistant, but it should not replace the developer.

- The best workflow combines automation, AI support, and human decision-making.

- Fixed rules are excellent for catching obvious problems quickly.

- Human judgment is still required to review results, correct issues, commit changes, push branches, and open Pull Requests responsibly.

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`https://github.com/nomolos98/devops-micro-internship-interviews.git`

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

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
