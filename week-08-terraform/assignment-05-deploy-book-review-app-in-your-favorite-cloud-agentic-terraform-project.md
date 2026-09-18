# Capstone Assignment — Deploy the Book Review App Using Terraform and Claude Code Agentic AI

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Student Details

**Full Name:** Solomon Anichebe 
**Cloud Platform:** Azure
**GitHub Repository URL:** https://github.com/nomolos98
**Public Application URL / Load-Balancer DNS:** http://4.253.165.48/

---

## Purpose

Deploy the Book Review App using Terraform on AWS or Azure in a secure, highly available, production-style three-tier architecture. Use Claude Code, specialized subagents, Terraform MCP, and validation hooks to support the engineering workflow while keeping all infrastructure-changing operations under human control.

---

# Task 0 — Prepare the Project and Agentic AI Environment

## Goal

Prepare the Book Review App project and configure the provided Claude Code Agentic AI starter kit with project context, specialized subagents, Terraform MCP, validation hooks, and safety guardrails.

## Evidence

### Screenshot 1 — Project `CLAUDE.md`

Add a screenshot of the project `CLAUDE.md` showing the three-tier architecture, security boundaries, Terraform requirements, and human-approval rules.

![Assignment 5 screenshot](screenshots/week08-ass05-claude-requirement.png)
![Assignment 5 screenshot](screenshots/week08-ass05-claude-requirement2.png)

---

### Screenshot 2 — Terraform Engineer Subagent

Add a screenshot showing the Terraform Engineer subagent configuration.

![Assignment 5 screenshot](screenshots/week08-ass05-terraform-engineer-subagent-config.png)

---

### Screenshot 3 — Architecture and Security Reviewer Subagent

Add a screenshot showing the Architecture and Security Reviewer subagent configuration.

![Assignment 5 screenshot](screenshots/week08-ass05-arch-security-reviewer-subagent-config.png)

---

### Screenshot 4 — Terraform MCP Connection

Add a screenshot showing Terraform MCP connected and available.

![Assignment 5 screenshot](screenshots/week08-ass05-terraform-mcp-connected.png)

---

### Screenshot 5 — Validation Hooks

Add a screenshot showing the configured Claude Code validation hooks.

The hook is registered for PostToolUse event. It occurs after the tool runs, not before. And triggers only on file edit/write actions — so reads, bash commands, etc. don't trigger it.

![Assignment 5 screenshot](screenshots/week08-ass05-claude-code-validation-hooks.png)
![Assignment 5 screenshot](screenshots/week08-ass05-claude-code-validation-hooks2.png)

---

# Task 1 — Design the Three-Tier Architecture

## Goal

Design the required secure, highly available three-tier architecture and create an architecture diagram before building the infrastructure.

The diagram must show:

- VPC or VNet
- Availability Zones or equivalent availability locations
- Six subnets
- Internet connectivity
- NAT or outbound design
- Public load balancer
- Web Tier
- Internal load balancer
- Application Tier
- Managed MySQL
- Read replica
- Main traffic flow

## Architecture Diagram

![Assignment 5 screenshot](screenshots/week08-ass05-three-tier-architecture-design.png)

---

# Task 2 — Build the Terraform Networking and Security Layers

## Goal

Create the modular Terraform project and implement the network and security layers across the required public and private subnets.

## Evidence

### Screenshot 6 — Modular Terraform Project Structure

Add a screenshot showing the modular Terraform project structure.

![Assignment 5 screenshot](screenshots/week08-ass05-modular-terraform-structure.png)

---

### Screenshot 7 — Six-Subnet Architecture

Add a screenshot showing the six-subnet architecture across two availability locations.

![Assignment 5 screenshot](screenshots/week08-ass05-six-subnet-architecture.png)

---

### Screenshot 8 — Public and Private Tier Separation

Add a screenshot showing the public and private tier separation, including routing and security boundaries.

nsg-web attached to Web subnets: Allow inbound 80/443 from Internet service tag

![Assignment 5 screenshot](screenshots/week08-ass05-nsg-web-attached-web-subnets.png)

nsg-app attached to App subnets: Allow inbound app port (e.g. 3001/tcp) only from Web subnet CIDRs (10.0.1.0/24, 10.0.2.0/24).

![Assignment 5 screenshot](screenshots/week08-ass05-nsg-app-attached-app-subnets.png)

nsg-db attached to DB subnets: Allow inbound DB port (e.g., 3306/tcp) only from App subnet CIDRs (10.0.11.0/24, 10.0.12.0/24).

![Assignment 5 screenshot](screenshots/week08-ass05-nsg-db-attached-db-subnets.png)

---

# Task 3 — Build the Load-Balancing and Compute Layers

## Goal

Deploy the public and internal load balancers and the Web and Application compute resources required by the Book Review App.

## Evidence

### Screenshot 9 — Web and Application Compute

Add a screenshot showing the Web and Application compute resources in their required subnets.

![Assignment 5 screenshot](screenshots/week08-ass05-web-application-resources.png)

![Assignment 5 screenshot](screenshots/week08-ass05-web-application-subnet.png)

---

### Screenshot 10 — Public Load Balancer

Add a screenshot showing the internet-facing public load balancer.

![Assignment 5 screenshot](screenshots/week08-ass05-internet-facing-public-load-balancer.png)

---

### Screenshot 11 — Internal Load Balancer

Add a screenshot showing the private internal load balancer.

![Assignment 5 screenshot](screenshots/week08-ass05-private-internal-load-balancer.png)

---

### Screenshot 12 — Healthy Targets

Add a screenshot showing healthy target groups or backend pools.

![Assignment 5 screenshot](screenshots/week08-ass05-healthy-backend-pools.png)

---

# Task 4 — Build the Managed MySQL Database Layer

## Goal

Deploy a private, highly available managed MySQL database with a read replica and restrict database connectivity to the Application Tier.

## Evidence

### Screenshot 13 — Managed MySQL Database

Add a screenshot showing the managed MySQL database deployment.

![Assignment 5 screenshot](screenshots/week08-ass05-managed-mysql-database.png)

---

### Screenshot 14 — High Availability

Add a screenshot showing the Multi-AZ or high-availability configuration.

![Assignment 5 screenshot](screenshots/week08-ass05-high-availability.png)
![Assignment 5 screenshot](screenshots/week08-ass05-high-availability2.png)

---

### Screenshot 15 — Read Replica

Add a screenshot showing the read replica configuration.

![Assignment 5 screenshot](screenshots/week08-ass05-read-replica.png)

---

### Screenshot 16 — Private Database Access

Add a screenshot showing that the database is private and accepts MySQL traffic only from the Application Tier.

![Assignment 5 screenshot](screenshots/week08-ass05-database-private-traffic4rm-applicationtier.png)

---

# Task 5 — Validate, Review, and Apply the Terraform Configuration

## Goal

Validate the Terraform configuration, review the execution plan using both Agentic AI and human judgment, and apply the infrastructure changes only after all required checks pass.

## Evidence

### Screenshot 17 — Terraform Validation

Add a screenshot showing successful `terraform validate` output.

![Assignment 5 screenshot](screenshots/week08-ass05-terraform-validate.png)

---

### Screenshot 18 — Terraform Plan

Add a screenshot showing the Terraform plan output.

![Assignment 5 screenshot](screenshots/week08-ass05-terraform-plan.png)

---

### Screenshot 19 — Terraform Apply

Add a screenshot showing successful `terraform apply` completion.

![Assignment 5 screenshot](screenshots/week08-ass05-terraform-apply.png)

---

# Task 6 — Deploy and Configure the Book Review Application

## Goal

Deploy and configure the Book Review App across the Web, Application, and Database tiers and verify the complete application functionality.

## Evidence

### Screenshot 20 — Homepage

Add a screenshot showing the Book Review App homepage through the public endpoint.

![Assignment 5 screenshot]

---

### Screenshot 21 — Login or Authentication

Add a screenshot showing successful login or authentication.

![Assignment 5 screenshot]

---

### Screenshot 22 — Book Data

Add a screenshot showing the book listing or book details.

![Assignment 5 screenshot]

---

### Screenshot 23 — Review Functionality

Add a screenshot showing the review functionality working successfully.

![Assignment 5 screenshot]

---

### Screenshot 24 — Backend or API Evidence

Add a screenshot showing that the backend or API is working successfully.

![Assignment 5 screenshot]

---

### Screenshot 25 — Database Reads and Writes

Add a screenshot showing successful database reads and writes.

![Assignment 5 screenshot]

## Public Application URL

**Public Application URL / DNS:** Add the working public application URL or load-balancer DNS here

---

# Task 7 — Demonstrate the Agentic AI Workflow

## Goal

Demonstrate how Claude Code assisted with Terraform generation, architecture and security review, and evidence-based troubleshooting while infrastructure-changing decisions remained under human control.

You do not need to submit your complete Claude Code conversation history. Include only focused evidence.

## Evidence

### Screenshot 26 — AI-Assisted Terraform Generation

Add a screenshot showing one useful example of AI-assisted Terraform generation or improvement.

![Assignment 5 screenshot](screenshots/week08-ass05-quest-answer-ai-assited.png)
![Assignment 5 screenshot](screenshots/week08-ass05-quest-answer-ai-assited2.png)

---

### Screenshot 27 — Architecture or Security Review

Add a screenshot showing one structured architecture or security review result.

![Assignment 5 screenshot](screenshots/week08-ass05-structured-security-review.png)
![Assignment 5 screenshot](screenshots/week08-ass05-structured-security-review2.png)

---

### Screenshot 28 — AI-Assisted Troubleshooting

Add a screenshot showing one AI-assisted troubleshooting interaction based on collected evidence.

![Assignment 5 screenshot](screenshots/week08-ass05-ai-assisted-troubleshooting-interaction.png)
![Assignment 5 screenshot](screenshots/week08-ass05-ai-assisted-troubleshooting-interaction2.png)
![Assignment 5 screenshot](screenshots/week08-ass05-ai-assisted-troubleshooting-interaction3.png)

---

# Task 8 — Complete the Final Architecture Review

## Goal

Review the completed infrastructure against the original capstone requirements and resolve significant architecture, security, reliability, and cost issues.

Confirm that the final review covers:

- Tier separation
- Availability
- Public exposure
- Routing
- Security rules
- Load balancing
- Database privacy
- Secrets
- Terraform quality
- Module structure
- Reliability
- Obvious cost risks

Use Screenshot 27 as the focused evidence for the structured architecture or security review.

---

# Task 9 — Answer the Reflection Questions

## Goal

Reflect on the architecture, Terraform implementation, and Agentic AI workflow. Answer each question briefly in your own words.

## Architecture

### 1. Why did you separate the Web, Application, and Database tiers?

I separated the application into three tiers so that each layer has a clear responsibility and security boundary:

Web Tier: handles user-facing traffic through the public Load Balancer and Nginx.
Application Tier: runs the backend/API and is accessed through the internal Load Balancer.
Database Tier: stores application data in private MySQL database

This separation improves security, maintainability, scalability, and troubleshooting because each tier can be managed independently.

### 2. Why is the Application Tier private?

The Application tier holds the backend's business logic and, more importantly, holds the database credentials and the code that queries MySQL directly. If it had a public IP or was reachable from the internet, an attacker could bypass the Web tier entirely, hit the API directly, or attempt to exploit the backend process itself. Keeping the backend private reduces its direct exposure to internet traffic and the only way in is through the internal load balancer, which only the Web tier can reach.

### 3. Why is MySQL private?

The database is the highest-value target in the whole architecture — it holds every user's data. It has no legitimate reason to ever be reached from the public internet; only the Application tier needs to talk to it. In this build, public_network_access = "Disabled" is set explicitly on the MySQL Flexible Server, and the DB NSG only allows inbound 3306 from the App tier subnet CIDRs (10.0.11.0/24, 10.0.12.0/24) — nothing else, not even the Web tier.

### 4. Why are multiple Availability Zones used?

I used multiple Availability Zones to improve availability and resilience. The Web and Application tiers are distributed across two zones. If one zone experiences a failure, the other zone can continue serving traffic, subject to the health of the remaining resources.
This also prevents the application from depending on a single physical location within the Azure region.

### 5. What is the difference between Multi-AZ/high availability and a read replica?

High availability is a synchronous standby copy of the same database, kept in a different zone, that exists purely for automatic failover, you don't connect to it directly, and under normal operation it's invisible. If one VM or zone fails, the other can continue serving traffic.

A read replica is primarily about database read scalability and providing another copy of database data.
So:
Multi-AZ/HA: focuses on availability/resilience.
Read replica: provides another database copy, mainly for read workloads and related database use cases.

## Terraform

### 6. How did you divide your Terraform into modules?

divided the configuration into logical modules based on infrastructure responsibility, each owning one concern: network (VNet, subnets, NAT Gateways), security (NSGs and subnet associations), load-balancer (public and internal LBs), database (MySQL Flexible Server, replica, private DNS zone), bootstrap: Generates user‑data scripts for Web and App tiers (install Node, Nginx, PM2, clone repo, configure app) and compute Reusable VM module used for Web and App tiers (NIC, VM, identity).

### 7. How do the modules communicate through variables and outputs?

The modules communicate using inputs (variables) and outputs. For example, the network module creates subnets and exposes their IDs through outputs. The compute module can then receive those subnet IDs as variables.
This pattern ensures clear contracts, modules don’t hard‑code resource IDs from other modules; they receive them as inputs.

### 8. What did you specifically check in `terraform plan`?

Beyond the basics (add/change/destroy counts), specific things this build's plans were checked for unexpected public IPs or 0.0.0.0/0 rules, whether zones was being set correctly depending on whether a resource referenced a subnet or a public IP, whether a proposed change would force a resource replacement rather than an in-place update, whether NSG rule access types were valid for the service tags they used, and whether outputs exposed anything sensitive. The recurring subnet delegation actions diff was also something worth specifically watching for, since it kept reappearing across multiple plans even after a successful apply.

## Agentic AI

### 9. What was the purpose of `CLAUDE.md`?

It was used to document the architecture goals.Capture constraints and decisions (region, SKUs, NSG rules, bootstrap approach). An instruction set every Claude Code session and subagent reads before doing anything, what patterns to follow, and what to avoid. The architecture spec (CIDR, six subnets, tier boundaries), the security rules (ports 3001 and 3306 never public), the Terraform engineering rules (modularity, no hardcoded secrets), and the safety rules (never auto-approve apply/destroy). 
Serve as a single source of truth so AI assistance stays aligned with the intended design instead of making ad‑hoc assumptions.


### 10. What work did the Terraform Engineer subagent perform?

It designed and implemented every module phase by phase — networking, security, load balancing, database, bootstrap, and compute researching current Azure provider documentation via Terraform MCP before writing resources rather than relying purely on memory. Include tasks such as: reviewing the Terraform structure, generating/improving Terraform code, working with modules, checking variables and outputs, identifying configuration problems, helping implement the Azure infrastructure, validating Terraform changes against the project requirements

### 11. What did the Architecture and Security Reviewer identify?

The Architecture and Security Reviewer was used to examine the infrastructure from a design and security perspective, rather than simply generating code.
It reviewed areas such as: separation of Web, App and Database tiers, private placement of the App and Database tiers, Load Balancer traffic flow, NSG/security boundaries, Availability Zone distribution, database networking, managed identity usage, Terraform architecture

The review helped identify areas that needed attention before considering the infrastructure complete.

### 12. Why did you use Terraform MCP instead of relying only on Claude's existing Terraform knowledge?

Terraform MCP provided Claude with access to current, project-relevant Terraform/Azure information and tooling rather than relying entirely on the model's pre-existing knowledge.

This was useful because Terraform providers and Azure resources can change over time. The clearest example in this build: before committing to zone-pinned NAT Gateways, the agent checked whether the chosen region (southafricanorth) actually supported Availability Zones by fetching Microsoft's live documentation rather than assuming — and it turned out to be correct, but a wrong assumption here would only have been caught after a failed apply

### 13. What was the purpose of your validation hooks?

The validation hooks were designed to catch problems before infrastructure was deployed. They provided automated checks around things such as: Terraform formatting > Terraform validation > Configuration checks > Plan/review > Apply

### 14. Describe one real issue Claude helped you troubleshoot.

The first terraform apply failed with four independent errors in a single run: MySQL's HA mode being incompatible with the Burstable SKU tier in Azure, VM creation failed with: SkuNotAvailable: Standard_B2s is currently not available in location 'SouthAfricaNorth'.

Ran this to check available SKUs:
az vm list-skus --location southafricanorth --resource-type virtualMachines \
  --query "[?name=='Standard_B2s' || name=='Standard_B2s_v2' || name=='Standard_D2s_v5']" -o table

Also, an NSG rule using the AzurePlatformDNS service tag with an Allow access type that Azure's API rejects outright, and a transient "connection reset" error creating the second NAT Gateway. Each was diagnosed from the raw Azure API error text rather than guessed at — for the NSG rule specifically, the root cause was confirmed by checking Microsoft's own documentation, which states that platform service tags like AzurePlatformDNS can only be used in Deny rules, since that traffic is already implicitly permitted and can't be additionally "allowed." Each fix was made and validated one at a time before retrying, rather than changing everything at once and hoping.


### 15. Describe one recommendation you reviewed, modified, or rejected instead of accepting blindly.

One important example was the recommendation to change either the VM size or region after Azure reported:

SkuNotAvailable, Standard_B2s, SouthAfricaNorth

Instead of blindly changing the VM size, I treated the recommendation as something to verify first.
The next step was to check Azure's available VM SKUs:

az vm list-skus \
  --location southafricanorth \
  --resource-type virtualMachines

This is important because changing from Standard_B2s to another size affects cost, performance, and potentially Availability Zone availability. So the AI recommendation was reviewed against actual Azure capacity information before modifying Terraform.

---

# Task 10 — Publish the Mandatory LinkedIn Post

## Goal

Publish a LinkedIn post describing the capstone, the technical work completed, the Agentic AI workflow, and the lessons learned.

Write the post in your own words, include at least one project image or other proof, and ensure that it can be viewed by the submission reviewer.

## LinkedIn Post URL

**LinkedIn Post URL:** https://www.linkedin.com/posts/solomonanichebe_devops-azure-terraform-activity-7506344512047464449-siVB?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAXBpdEBaUln31DVzGUPS7Q7mpZjlUYg8QY

---

# Submission Instructions

- Complete Tasks 0–10 in sequence.
- Include all Screenshots 1–28 exactly as specified.
- Ensure that your full name is visible in the required screenshots.
- Include the selected cloud platform.
- Include the completed architecture diagram.
- Include the modular Terraform project structure.
- Include the working public application URL or public load-balancer DNS.
- Include all required Agentic AI workflow evidence.
- Answer all 15 reflection questions briefly in your own words.
- Include the published LinkedIn post URL.
- Do not expose cloud credentials, database passwords, SSH private keys, JWT secrets, access tokens, account IDs, Terraform state containing sensitive values, or other confidential information.
- Review all screenshots and project files carefully before submitting through GitHub.

---

# Completion Checklist

- [ ] Selected AWS or Azure
- [ ] Added and reviewed the Agentic AI starter files
- [ ] Configured `CLAUDE.md`
- [ ] Configured the Terraform Engineer subagent
- [ ] Configured the Architecture and Security Reviewer subagent
- [ ] Connected Terraform MCP
- [ ] Configured validation hooks and safety guardrails
- [ ] Created the architecture diagram
- [ ] Created the six-subnet design
- [ ] Configured public Web Tier routing
- [ ] Kept the Application Tier private
- [ ] Kept the Database Tier private
- [ ] Configured tier-specific Security Groups or NSGs
- [ ] Restricted backend port `3001`
- [ ] Restricted MySQL port `3306` to the Application Tier
- [ ] Created the public load balancer
- [ ] Created the internal load balancer
- [ ] Configured listeners and health checks
- [ ] Deployed the Web Tier compute resources
- [ ] Deployed the private Application Tier compute resources
- [ ] Provisioned private managed MySQL
- [ ] Configured Multi-AZ or high availability
- [ ] Configured a read replica
- [ ] Created the modular Terraform project
- [ ] Used variables, outputs, and module dependencies
- [ ] Used current Terraform documentation through MCP
- [ ] Used hooks for deterministic validation
- [ ] Completed `terraform fmt`
- [ ] Completed `terraform validate`
- [ ] Reviewed `terraform plan`
- [ ] Completed the Terraform Engineer review
- [ ] Completed the Architecture and Security review
- [ ] Applied the infrastructure only after human approval
- [ ] Deployed and configured the backend
- [ ] Deployed and configured the frontend
- [ ] Configured Nginx where required
- [ ] Configured the internal backend endpoint
- [ ] Configured the public frontend endpoint
- [ ] Verified the homepage
- [ ] Verified login or authentication
- [ ] Verified book data
- [ ] Verified review functionality
- [ ] Verified the backend API
- [ ] Verified database reads and writes
- [ ] Verified healthy load-balancer targets
- [ ] Included AI-assisted Terraform generation evidence
- [ ] Included one architecture or security review
- [ ] Included one AI-assisted troubleshooting example
- [ ] Completed the final architecture review
- [ ] Answered all 15 reflection questions
- [ ] Published the mandatory LinkedIn post
- [ ] Added the LinkedIn post URL
- [ ] Captured all 28 required screenshots
- [ ] Confirmed that my full name is visible in the required screenshots
- [ ] Checked that no secrets or sensitive information are exposed

---

## About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory), focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations through hands-on experience.

---

## Resources

- Book Review App Repository: [https://github.com/pravinmishraaws/book-review-app](https://github.com/pravinmishraaws/book-review-app)
- DMI Official Website: [https://dmi.pravinmishra.com](https://dmi.pravinmishra.com)
- University: [https://university.pravinmishra.com](https://university.pravinmishra.com)
- Discord Community: [https://discord.pravinmishra.com](https://discord.pravinmishra.com)
- Blog: [https://dmi.pravinmishra.com/blog](https://dmi.pravinmishra.com/blog)
- YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
- Pravin Mishra on LinkedIn: [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
- CloudAdvisory on LinkedIn: [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

---

*This submission is part of the DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
