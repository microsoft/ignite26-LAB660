# LAB660: Configuring, monitoring, and managing AI spend with Agent 365

Ignite 2026 hands-on lab: scenario and build specification

- **Prepared by:** Akhil Ravindran, Finbarr Duggan, AI FinOps
- **Audience:** Lab build team, speakers and proctors
- **Status:** Draft v0.10
- **Scope:** The lab goes through Copilot Cowork only. The same controls apply to the other AI services in Copilot > Cost Management, but they aren't covered hands-on.

---

## 1. Session

| Item | Detail |
|---|---|
| Session | LAB660: Configuring, monitoring, and managing AI spend with Agent 365 |
| Format | 75-minute hands-on lab at Microsoft Ignite 2026 (17 to 20 November, San Francisco) |
| Abstract | Get hands-on with AI spend management in Agent 365 and learn how to confidently deploy and scale AI across your organisation. After this 75-minute lab, you will understand how to configure the policies that control model and agent availability and spending limits as well as how to monitor spending and course correct by understanding delivered value. |
| Lab owner | Finbarr Duggan |
| Speakers | Finbarr Duggan, Reshma Kapoor |
| Proctors | Akhil Ravindran, Madeline Nelson, Shawn Leonard, Shilpi Agarwal |
| Lab environment | Hosted by Skillable. Issues are tracked in the microsoft/ignite26-LAB660 GitHub repository. Labs go through QA, then security review, then team testing. |

### How the lab covers the abstract

| Abstract promise | Where it's covered |
|---|---|
| Configure the policies that control agent availability | S1 (a spending policy grants access to Cowork), S2 (Agents and services, Auto-apply new services) |
| Configure the policies that control model availability | S2 (model profile in the policy; tenant-level model provider settings) |
| Configure spending limits | S2, S3 and S4 (policy and per-user limits, and what users experience when they're reached) |
| Monitor spending | S3 (alerts and notifications), S8 (Cost Management Overview and Consumption) |
| Course correct by understanding delivered value | S8 (Copilot > Cowork Usage and Value tabs) |
| Deploy and scale AI with confidence | S5 and S6 (requests and approvals), S7 (capacity packs, PAYG or both) |

---

## 2. Lab at a glance

| Item | Detail |
|---|---|
| Per student | One dedicated tenant: 1 admin and 10 users (U01 to U10) |
| Service used | Copilot Cowork only |
| Starting state | Usage-based billing already activated. Four spending policies pre-staged. Month-to-date Cowork consumption pre-seeded. One capacity pack whose credits available to MAC are already used up. One pending credit request. |
| What students build | One new spending policy and model profile; limit and alert edits; request approvals; a custom request policy; a billing-method change; one value-based course-correction |
| Sign-in pattern | Admin in a normal browser window. Users in a separate InPrivate window or browser profile, switching users as directed. |

### Key concepts the lab teaches

| Concept | What it does | Where in MAC |
|---|---|---|
| Spending policy | Grants access to Cowork for a scope of users or groups, and sets limits, alerts, model profile and billing method | Copilot > Cost Management > Configuration |
| Agents and services, and Auto-apply new services | Chooses what the policy unlocks (Cowork in this lab). Auto-apply (on by default) adds newly supported services and agents automatically, and with them, access. | Spending policy > Select agents and services |
| Model profile | Reusable set of at least two models a policy can use (Cowork only) | Spending policy > Model profiles, or Configuration > Model profiles |
| Tenant model settings | Control which model providers are available at all. They decide which models users see, not whether they can use Cowork. | Copilot > Settings, or Copilot > Cowork > Settings |
| Policy monthly limit | Caps the credits the whole policy can spend each month. When it's reached, users in the policy lose access until credits reset on the 1st. | Spending policy > Set limits and alerts |
| Per-user monthly limit | Caps what any one user in the policy can spend | Spending policy > Set limits and alerts |
| Admin alerts and user notifications | Emails stakeholders when policy usage reaches a threshold (credits or %), and emails users at a % of their own limit | Spending policy > Set limits and alerts |
| Billing method | How the policy is funded: prepaid capacity packs, an Azure subscription (PAYG, with P3 if attached), or both | Spending policy > Select billing method |
| Credit requests | User requests for first-time access or more credits, reviewed by admins or routed to an external process | Overview > Top actions > View requests |
| Delivered value | Cowork usage, assisted hours and credits spent by task category | Copilot > Cowork > Usage and Value |

Draw-down order when several funding sources apply: prepaid capacity packs, then Copilot Credit Pre-Purchase Plan (P3), then pay-as-you-go.

---

## 3. Tenant build specification (per student tenant)

### 3.1 Licences, subscriptions and roles

| Component | Requirement | Notes |
|---|---|---|
| Microsoft 365 base licence with Exchange Online | Admin and U01 to U10 | Needed for admin alert emails and user threshold notifications |
| Microsoft 365 Copilot licence | U01 to U10 (admin optional) | Cowork requires a Copilot licence; usage-based experiences require a user subscription licence |
| Azure subscription in the same tenant, linked to the MAC billing account | One subscription, for example "Lab-PAYG" | Used as the PAYG billing method. Make the admin Owner or Contributor so Advanced billing settings (billing region, resource group) appear. List it in the scrapes (3.5). |
| Copilot Studio capacity pack | 1 pack (25,000 Copilot Credits per month) | Tenant licence bought through MAC Marketplace by a Global or Billing admin |
| Power Platform admin center (PPAC) allocation | Allocate 23,500 of the pack's credits to a separate environment, for example "Lab - Copilot Studio" | Leaves 1,500 credits available to MAC services, so the lab can show an exhausted pack without burning 25,000 credits. |
| Student admin role | Global Administrator (or Billing Administrator plus AI Administrator) | Creating spending policies (S2) and setting billing methods (S7) need Global or Billing admin. AI Administrator alone can edit policies, limits and alerts but can't create policies. |
| U06 role | AI Reader (optional stretch) | Shows read-only access to Cost Management dashboards |
| P3 | Not purchased in student tenants | P3 purchases are final and can't be cancelled; cover as an instructor talk track only |

### 3.2 Personas and security groups

| User | Persona | Security group | Policy at lab start |
|---|---|---|---|
| Admin | Contoso IT and FinOps admin (the student) | None | None |
| U01 Alex | Standard user, heavy month | SG-AI-Standard | Standard (PAYG) |
| U02 Blake | Standard user, at limit | SG-AI-Standard | Standard (PAYG) |
| U03 Casey | Standard user, light usage | SG-AI-Standard | Standard (PAYG) |
| U04 Dana | Finance analyst | SG-AI-Finance | Finance (Capacity pack only) |
| U05 Eli | Finance analyst | SG-AI-Finance | Finance (Capacity pack only) |
| U06 Frankie | Finance lead (AI Reader, optional) | SG-AI-Finance | Finance (Capacity pack only) |
| U07 Gray | Marketing manager | SG-AI-Marketing | Marketing (Shared pool, PAYG) |
| U08 Harper | Marketing specialist | SG-AI-Marketing | Marketing (Shared pool, PAYG) |
| U09 Indy | Pilot power user who automates work with scheduled tasks | SG-AI-Pilot | Pilot (Capacity pack + PAYG) |
| U10 Jordan | New joiner, Sales | None | None (no Cowork access) |

Also pre-create an empty group, SG-AI-Extended. The student's new policy targets it.

> **Build note:** Spending policies can target specific users only through security groups, so every persona is placed by group membership.

### 3.3 Pre-staged spending policies

| Policy | Scope | Agents and services | Auto-apply new services | Monthly policy limit | Per-user limit | Admin alert | User notification | Model profile | Billing method |
|---|---|---|---|---|---|---|---|---|---|
| Standard (PAYG), the default policy | SG-AI-Standard | Cowork | On | 6,000 | 2,000 | 70%, to admin | 80% | Default | Azure subscription (PAYG) |
| Finance (Capacity pack only) | SG-AI-Finance | Cowork | Off | 6,000 | 2,000 | 80%, to admin and U06 | 80% | Default | Prepaid capacity packs only |
| Marketing (Shared pool, PAYG) | SG-AI-Marketing | Cowork | On | 4,000 | 4,000 | 90%, to admin | 80% | Default | Azure subscription (PAYG) |
| Pilot (Capacity pack + PAYG) | SG-AI-Pilot | Cowork | On | 10,000 | 5,000 | 80%, to admin | 80% | "Pilot - Approved models" | Prepaid capacity packs plus Azure subscription (PAYG overflow) |

### 3.4 Seeded consumption: target month-to-date state at lab start

| User | Policy | Per-user limit | Seeded credits | % of own limit | Funded by | Expected state at lab start | Used in |
|---|---|---|---|---|---|---|---|
| U01 | Standard | 2,000 | 1,950 | 97.5% | PAYG | Active, near limit; user threshold email (80%) received | S4, S6 |
| U02 | Standard | 2,000 | 2,000 | 100% | PAYG | Blocked by personal limit | S4, S5, S6 |
| U03 | Standard | 2,000 | 300 | 15% | PAYG | Active | Stretch A |
| U04 | Finance | 2,000 | 400 | 20% | Capacity pack | Blocked: pack credits exhausted | S7 |
| U05 | Finance | 2,000 | 300 | 15% | Capacity pack | Blocked: pack credits exhausted | S7 |
| U06 | Finance | 2,000 | 200 | 10% | Capacity pack | Blocked: pack credits exhausted | S7, Stretch C |
| U07 | Marketing | 4,000 | 2,800 | 70% | PAYG | Blocked: shared policy limit reached | S4 |
| U08 | Marketing | 4,000 | 1,200 | 30% | PAYG | Blocked: shared policy limit reached; pending credit request | S4, S6 |
| U09 | Pilot | 5,000 | 1,600 | 32% | 600 capacity pack, then 1,000 PAYG | Active, now running on PAYG overflow | S7 |
| U10 | None | None | 0 | None | None | No Cowork access | S5, S6 |

Policy roll-up at lab start:

| Policy | Credits used | Policy limit | Utilisation | Alert state |
|---|---|---|---|---|
| Standard (PAYG) | 4,250 | 6,000 | 70.8% | Admin alert (70%) firing daily |
| Finance (Capacity pack only) | 900 | 6,000 | 15.0% | Below threshold, but users blocked because pack credits are exhausted |
| Marketing (Shared pool, PAYG) | 4,000 | 4,000 | 100% | Limit reached; admin alert (90%) firing daily |
| Pilot (Capacity pack + PAYG) | 1,600 | 10,000 | 16.0% | Below threshold |

Funding roll-up at lab start:

- Capacity pack credits available to MAC: 1,500 (25,000 purchased minus 23,500 allocated in PPAC). Used: 1,500, or 100% (Finance 900 plus Pilot 600).
- PAYG credits used: 9,250 (Standard 4,250, Marketing 4,000, Pilot 1,000).
- Total: 10,750 credits; 9 active users.

### 3.5 Skillable environment and security review

- **Lab profile role:** the student admin needs Global Administrator (or Billing Administrator plus AI Administrator). If the Skillable lab profile can only grant AI Administrator, pre-create the Extended policy and turn S2 into editing it, and make S7's billing-method change an instructor demo.
- **Scrapes:** Skillable needs a document listing every Azure resource the lab uses, for the security review. Any later change to the Azure environment needs new scrapes and a new review. Include:
  - The Azure subscription used as the PAYG billing method ("Lab-PAYG").
  - The resource group where billing policies are deployed. Pre-create it, so it's known at review time.
  - The billing policy resources created for the PAYG-billed policies: Standard, Marketing and Pilot at build time, plus Extended (S2) and Finance (S7) created during the lab.
- **Validate** exactly which Azure resources a PAYG-billed spending policy creates, and whether resources created by students during the lab are acceptable to the security review. If not, have students select the pre-created resource group, or pre-stage those policies.
- **Tenant licensing:** confirm the Skillable tenants include Copilot licences for U01 to U10, the capacity pack, an Azure subscription linked to the MAC billing account, and Exchange mailboxes.

---

## 4. Scenario walkthroughs

Each scenario lists the goal, who signs in, the steps, a checkpoint and build notes.

### S1. Orientation: who can use Cowork, and why (Module 1, 7 min)

**Goal:** Understand the Cost Management layout and how access to Cowork is decided.

**Sign in:** Admin, then U10.

**Steps:**

1. In MAC, go to Copilot > Cost Management. Note the Overview, Consumption and Configuration tabs.
2. Open Configuration and review the four pre-staged policies: scope, Agents and services, limits and billing method.
3. Open one policy and walk through its sections: scope, agents and services, limits and alerts, model profile and billing method.
4. Go to Copilot > Cowork and note the Overview, Usage, Value and Settings tabs; S8 comes back here.
5. Sign in as U10 and open Cowork in the Copilot app. U10 has no access because no policy that selects Cowork includes them.

**Checkpoint:** The student can say which users have Cowork access, and why.

### S2. Configure a policy: agent availability, model availability and spending limits (Module 2, part 1)

**Goal:** Build one policy that controls which agents are available (Cowork), which models are available, and how much can be spent. The student will later use it to approve limit upgrades.

**Sign in:** Admin.

**Steps:**

1. Configuration > + Add spending policy.
2. Define the policy scope: name it "Extended limit (approved requests)". Switch from All users to Specific groups and select SG-AI-Extended.
3. Agent availability. In Select agents and services, select Cowork. Turn Auto-apply new services off, so future services and agents don't inherit this higher limit.
4. Spending limits. In Set limits and alerts:
   - Limited monthly budget: 10,000 credits.
   - Monthly budget limit for users: 5,000 credits.
   - Policy alert at 80% (or 8,000 credits), recipients: admin and U06.
   - User notifications on, at 80%.
5. Model availability. In Model profiles (shown because Cowork is selected), choose Customize model selection > Create new model profile. Name it "Cost-aware models", select two models, and allow Microsoft to select the most comparable model to maintain availability.
6. Select billing method: Change > Azure subscription "Lab-PAYG" (pay-as-you-go).
7. Review, then select Create spending policy. Confirm it appears in Configuration.
8. Open Copilot > Cowork > Settings and find the model and AI provider settings, which control model availability for the whole tenant.

**Checkpoint:** The new policy is listed, scoped to SG-AI-Extended (0 members), with Cowork, a model profile and PAYG billing. The student can explain the difference between the model profile and the tenant model settings.

> **Build note:** **Validate** the exact field labels, whether a policy alert accepts one threshold or several, and the model and provider settings shown on the Cowork Settings tab.

### S3. Configure limits and alerts on a live policy (Module 2, part 2)

**Goal:** Understand the two limit layers and the two kinds of notification.

**Sign in:** Admin (and admin mailbox).

**Steps:**

1. Open the admin mailbox and find the Standard policy alert (70% or more). Note that it repeats daily.
2. In Cost Management > Overview, review Top actions: Standard (70.8%) and Marketing (100%) are flagged, as are U01 and U02.
3. Edit "Standard (PAYG)": add U06 as a second alert recipient, confirm user notifications at 80%, then select Save changes.

**Checkpoint:** The student can explain the difference between the policy limit and the per-user limit, and between admin alerts and user notifications.

### S4. How users hit a limit (Module 3, 9 min)

**Goal:** Experience the "run out" states as a user, and use `/cost`.

**Sign in:** U01, U02 and U08.

**Steps:**

1. U01 (97.5% used): open Cowork and type `/cost` to see the approximate credits for the task, the credits used this month and the credits remaining (about 50). Start the standard lab task (for example: "Analyse Contoso Q3 AI spend.xlsx, identify the top three cost drivers and create a two-page Word summary with a chart"). The task can complete even if it crosses the limit. Type `/cost` again.
2. U02 (100% used): open Cowork and try to start a task. It's blocked. Note the message and the request option, but don't submit yet.
3. U08 (30% personal, Marketing policy at 100%): open Cowork. U08 still has personal headroom, but the shared Marketing limit is used up, so U08 is blocked.

**Checkpoint:** The student can explain the difference between a personal limit and a shared policy limit.

> **Build notes:** Provide a standard task prompt and sample file that reliably uses more than 50 credits. Capture the exact blocked messages and screens for the student guide. **Validate** how long enforcement takes after a limit is crossed.

### S5. Users request more credits or access (Module 4, part 1)

**Goal:** See the request experience from the user's side.

**Sign in:** U02, then U10.

**Steps:**

1. U02: from the blocked state, submit a request for more credits, using the business justification text provided in the student guide.
2. U10: in Cowork, request access (first-time use).

**Checkpoint:** Each user sees a confirmation that the request was sent.

> **Build note:** **Validate** the request entry point in Cowork for both cases, and whether U10 needs the request-access setting turned on.

### S6. Admin reviews and approves requests (Module 4, part 2)

**Goal:** Resolve requests with the right fix, and route future requests to an external process.

**Sign in:** Admin (and U01 for step 6).

**Steps:**

1. Overview > Top actions > View requests. The Credit requests page lists pending and approved requests: U08 (pre-staged), plus U02 and U10 (live).
2. Open U10's request. Note the requested service, licence status and current policy ("Not in a policy"). Approve it, and grant access by adding U10 to SG-AI-Standard.
3. Open U02's request (current policy: Standard). Approve it, and move U02 from SG-AI-Standard to SG-AI-Extended. U02's 2,000 credits carry forward, leaving 3,000 under the new 5,000 limit.
4. Open U08's request (current policy: Marketing). Approve it, and edit the Marketing policy to raise the monthly limit from 4,000 to 6,000. U07 and U08 both regain headroom (the pool is now 66.7% used).
5. Create a custom request policy: Credit requests > Request policies > Add request policy. Choose All products and services. Enter the redirect URL (a lab-owned IT portal page) and the message users will see. Optionally add a Learn more link and name the external service (for example, ServiceNow). Save.
6. Sign in as U01 (now over the limit after S4) and request more credits. U01 sees the redirect message. Back in MAC, the request appears in All requests, labelled "Handled externally". Approve, reject or mark it as already processed.
7. Optional: export the requests list.
8. At the end of the lab, sign in as U02 and U10 to confirm access (allow time for changes to apply).

**Checkpoint:** Three requests resolved, each with a different fix; one request handled externally.

> **Build notes:** **Validate** what Approve does in the UI (status change only, or a prompt to change scope or limits). **Validate** how long group membership changes take to apply. **Validate** whether adding a user to a second group (without removing them from the first) re-evaluates their policy. Provide a lab-owned redirect page. If U01 isn't blocked yet because of asynchronous enforcement, the proctor demonstrates step 6 in the instructor tenant.

### S7. Capacity packs vs PAYG vs both (Module 5, 13 min)

**Narrative:** "Finance says Cowork stopped working, but their policy is only at 15%."

**Goal:** Understand how billing methods map to policies, and what happens when prepaid credits run out.

**Sign in:** Admin, then U09 and U04.

**Steps:**

1. Consumption > Policies view: Finance shows 15% utilisation, with billing method "Prepaid capacity packs".
2. Overview: select the Prepaid Capacity pack credits usage card. The flyout shows consumption by service across MAC and Power Platform, with the assigned capacity. The pack credits available to MAC are used up (1,500 of 1,500), because 23,500 credits are allocated to a PPAC environment.
3. Compare the three funding set-ups in the tenant:
   - Finance (pack only): blocked until the pack replenishes or an admin acts.
   - Pilot (pack plus PAYG): sign in as U09 and run a short task. It works, and the overflow is billed as PAYG.
   - Standard and Marketing (PAYG only): unaffected by the pack. Only their policy limits cap spend.
4. Course-correct, option 1 (hands-on): edit the Finance policy's billing method and add Azure subscription "Lab-PAYG", so pack credits are used first and then PAYG. Save. The policy's scope, limits, alerts and services are kept.
5. Sign in as U04 and confirm Cowork works (allow time for the change to apply).
6. Option 2 (instructor demo): in PPAC (Licensing > Copilot Studio > Manage capacity), reduce the environment allocation to release pack credits back to MAC services.
7. Option 3 (talk track): buy more capacity packs, or buy P3 from Cost Management > Configuration > Buy Pre-purchase Credits. P3 purchases are final.

**Checkpoint:** The student can explain, for each billing method, what happens when prepaid credits run out.

> **Build notes:** **Validate** pack-only blocking behaviour and the user message. **Validate** the PPAC allocation lever. **Validate** billing-method editing (an external walkthrough from July 2026 said the billing method was locked after creation; current Learn guidance says it can be changed). Confirm the capacity pack's replenishment date against the 1st-of-month policy reset.

### S8. Monitor spending and course-correct on delivered value (Module 6, 11 min)

**Goal:** Read the spending dashboards, compare spend with the value delivered, and make one evidence-based change.

**Sign in:** Admin.

**Steps:**

1. Cost Management > Overview: review Total Copilot Credits used, the Prepaid Capacity pack card, the Pay-as-you-go card (which includes P3), Active users and the spending trend chart (prepaid, PAYG and cumulative).
2. Consumption > Policies (the default view): policy status, scope, active users, credit usage, current spending limit, limit utilisation and billing method. Then the Users view (select U02 to see total credits, daily usage, spending policy history and credits by policy) and the Groups view (select SG-AI-Marketing).
3. Copilot > Cowork > Usage: active users, total tasks, average tasks per user and retained users, plus tasks by type (user-initiated or scheduled).
4. Copilot > Cowork > Value: Cowork assisted hours, then the Assisted hours by task category table (users, assisted hours and credits spent for each category).
5. Make one course-correction based on value, for example:
   - Marketing's pool ran out on content creation. If that work shows strong assisted hours, keep the higher limit from S6; if not, put it back to 4,000 and coach the team.
   - U01's heavy month is mostly analysis and research with strong assisted hours: move U01 to the Extended policy.
   - U09's scheduled tasks automate repeatable work: keep the Pilot policy and consider widening its scope.
6. Export a report.

**Checkpoint:** The student names one change, the spend evidence and the value evidence behind it.

> **Build note:** **Validate** that the Value tab shows task categories and assisted hours for the seeded usage.

### Stretch exercises (for fast finishers)

- Stretch A, precedence: add U03 to SG-AI-Pilot. U03 is now in Standard (2,000 per user) and Pilot (5,000 per user). The highest per-user limit wins, so Pilot applies, and U03's 300 credits carry forward (6% of the new limit).
- Stretch B, access vs budget (discussion): why a 1-credit "All users" policy that selects Cowork gives everyone access. The fix is to remove Cowork from that policy, or keep users out of its scope.
- Stretch C, read-only finance view: sign in as U06 (AI Reader). Dashboards are visible, but policies, limits, alerts, request policies and billing methods can't be changed.
- Stretch D, deleting a policy (discussion): deleting a policy doesn't reset or reallocate credits. Past usage stays in reports, and users carry on under any other policy that applies to them.
- Stretch E, Cowork-specific requests: add a second request policy for Cowork only, with a different redirect URL. Cowork requests now follow it, because a service-specific request policy takes precedence over the all-services one.
- Stretch F, new services (discussion): a new service launches next month. Which policies grant access to it automatically? Standard, Marketing and Pilot, because Auto-apply new services is on; Finance and Extended don't.
