# LAB660: Configuring, monitoring, and managing AI spend with Agent 365

Ignite 2026 hands-on lab: scenario and build specification, **time-optimised version**

- **Prepared by:** Akhil Ravindran, Finbarr Duggan, AI FinOps
- **Audience:** Lab build team, speakers and proctors
- **Status:** Draft v0.11 (time-optimised proposal, based on v0.10)
- **Scope:** The lab goes through Copilot Cowork only. The same controls apply to the other AI services in Copilot > Cost Management, but they aren't covered hands-on.

---

## What changed from v0.10, and why

v0.10 estimates at **~121 minutes** of hands-on work for a novice, against 65 minutes available, and asks students to switch users **11 times** (~33 minutes of sign-in alone, and the most error-prone part of the lab). This version keeps every promise in the abstract but changes **who does what**:

| Change | Effect |
|---|---|
| **Students stay signed in as the admin for the whole core path.** Zero user switches. | Removes ~33 min of sign-in time and the main source of proctor calls. |
| **User-side experiences move to the room screen** (intro "before" montage, looping clips during the lab, wrap-up "after" montage) and to screenshots in the student guide. | Students still see every user state: no access, `/cost`, personal limit, shared limit, request, redirect, restored access, PAYG overflow. |
| **All three credit requests are pre-staged** (U02, U08, U10), not just U08. | S5 becomes a "watch" step; S6 starts with three requests waiting. |
| **Confirmation steps that depend on propagation** (U02/U10 access after approval, U04 after the billing change) are shown on the room screen from an instructor tenant where the changes were applied hours earlier. | No more students waiting on asynchronous enforcement, or failing a checkpoint that's not their fault. |
| **Instructor-only content** (PPAC allocation lever, P3 talk track, external request redirect) moves to the wrap-up and guide sidebars. | Frees ~5 min of hands-on time. |
| **Reading is pre-digested**: the guide shows the four pre-staged policies as a table, so students confirm rather than discover. All names, values and URLs use the lab platform's type-text feature. | Cuts orientation and data-entry time for novices. |
| Low-value-per-minute steps (admin mailbox, Groups view, report exports, U06 recipient on the new policy) become **stretch exercises**. | Fast finishers still get them. |

**Result: ~56 minutes for a novice** (9 minutes of buffer inside the 65-minute hands-on block), ~36 minutes for a confident attendee, who then has time for the stretch exercises.

---

## 1. Session

| Item | Detail |
|---|---|
| Session | LAB660: Configuring, monitoring, and managing AI spend with Agent 365 |
| Format | 75-minute hands-on lab at Microsoft Ignite 2026 (17 to 20 November, San Francisco): 5 min intro, 65 min hands-on, 5 min wrap-up |
| Abstract | Get hands-on with AI spend management in Agent 365 and learn how to confidently deploy and scale AI across your organisation. After this 75-minute lab, you will understand how to configure the policies that control model and agent availability and spending limits as well as how to monitor spending and course correct by understanding delivered value. |
| Lab owner | Finbarr Duggan |
| Speakers | Finbarr Duggan, Reshma Kapoor |
| Proctors | Akhil Ravindran, Madeline Nelson, Shawn Leonard, Shilpi Agarwal |
| Lab environment | Hosted by Skillable. Issues are tracked in the microsoft/ignite26-LAB660 GitHub repository. Labs go through QA, then security review, then team testing. |
| Room screen | Driven by the speaker from an instructor tenant (or pre-recorded clips, with the live tenant as backup). See section 5. |

### How the lab covers the abstract

| Abstract promise | Hands-on (student) | Room screen and guide (watch) |
|---|---|---|
| Configure the policies that control agent availability | S1, S2 (Agents and services, Auto-apply new services) | Intro: U10 has no access because no Cowork policy includes them |
| Configure the policies that control model availability | S2 (model profile; tenant model settings) | — |
| Configure spending limits | S2, S3, S6 (policy and per-user limits) | S4: what users see at a personal limit and a shared limit |
| Monitor spending | S3 (Top actions), S8 (Overview and Consumption) | Guide: the admin alert email |
| Course correct by understanding delivered value | S8 (Cowork Usage and Value tabs, one change) | — |
| Deploy and scale AI with confidence | S6 (approvals, request policy), S7 (billing methods) | S5: requests from the user side. Wrap-up: restored access, redirect message, PAYG overflow, PPAC lever, P3 |

---

## 2. Lab at a glance

| Item | Detail |
|---|---|
| Per student | One dedicated tenant: 1 admin and 10 users (U01 to U10) |
| Service used | Copilot Cowork only |
| Starting state | Usage-based billing already activated. Four spending policies pre-staged. Month-to-date Cowork consumption pre-seeded. One capacity pack whose credits available to MAC are already used up. **Three pending credit requests (U02, U08, U10).** |
| What students build | One new spending policy and model profile; limit and alert edits; three request approvals; a custom request policy; a billing-method change; one value-based course-correction |
| Sign-in pattern | **Admin only, in a normal browser window, for the whole core path.** User credentials are provided for stretch exercises only. |
| User experience | Shown on the room screen and as screenshots in the student guide |

### Key concepts the lab teaches

Unchanged from v0.10: spending policy; Agents and services and Auto-apply new services; model profile; tenant model settings; policy monthly limit; per-user monthly limit; admin alerts and user notifications; billing method; credit requests; delivered value. Draw-down order when several funding sources apply: prepaid capacity packs, then Copilot Credit Pre-Purchase Plan (P3), then pay-as-you-go.

---

## 3. Tenant build specification (per student tenant)

Sections 3.1 to 3.5 are unchanged from v0.10. Section 3.6 lists what this version adds or removes. In the "Used in" column of 3.4, S4 and S5 are now room-screen segments rather than student sign-ins.

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
| U02 Allan | Standard user, at limit | SG-AI-Standard | Standard (PAYG) |
| U03 Diego | Standard user, light usage | SG-AI-Standard | Standard (PAYG) |
| U04 Isaiah | Finance analyst | SG-AI-Finance | Finance (Capacity pack only) |
| U05 Joni | Finance analyst | SG-AI-Finance | Finance (Capacity pack only) |
| U06 Lynne | Finance lead (AI Reader, optional) | SG-AI-Finance | Finance (Capacity pack only) |
| U07 Megan | Marketing manager | SG-AI-Marketing | Marketing (Shared pool, PAYG) |
| U08 Nestor | Marketing specialist | SG-AI-Marketing | Marketing (Shared pool, PAYG) |
| U09 Patti | Pilot power user who automates work with scheduled tasks | SG-AI-Pilot | Pilot (Capacity pack + PAYG) |
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
### 3.6 Build changes for the time-optimised version

| Change | Detail | Owner to validate |
|---|---|---|
| Pre-stage U02's request | Credit request from U02 (Standard, at 100%), with the business justification text from the guide | Build team: confirm requests can be created by script or API across ~600 tenants (same mechanism as U08) |
| Pre-stage U10's request | First-time access request from U10 (not in a policy). Turn on the request-access setting if needed. | Build team |
| Student credentials | Core path needs the admin only. Keep U01 to U10 credentials in the guide's appendix for stretch exercises. | Skillable |
| Type-text | Every name, value, URL and message students enter is a type-text item in the Skillable guide | Content |
| Instructor "before" tenant | Matches the student starting state (section 3.4), with U01's standard Cowork task ready to run | Speakers |
| Instructor "after" tenant | All student changes applied **at least a few hours before the session**, plus the request policy, so restored access and the redirect message show reliably | Speakers |
| Room-screen clips | Recorded clips A to G (section 5) with large on-screen labels, played in a loop during the hands-on block. Also embedded as screenshots in the guide. | Content |
| Mailboxes | Admin mailbox still needed (stretch). User mailboxes are needed only if the seeded user notifications are kept for the screen demo. | Build team |

Validation items from v0.10 that are **no longer on the student path** (still worth validating for the screen demos): request entry points in Cowork, enforcement latency after a limit is crossed, group-membership propagation time, and pack-only blocking messages.

---

## 4. Scenario walkthroughs

Scenario IDs are kept from v0.10 so build notes and the seeding tables still line up. ⏱ marks the estimated time for a novice. 📺 marks content shown on the room screen and in the guide instead of done hands-on.

### S0. Get started (⏱ ~3 min)

1. Launch the lab, sign in to the VM, open the browser and sign in to MAC as the admin with type-text credentials. ⏱ ~3 min

### S1. Orientation: who can use Cowork, and why (⏱ ~5 min; v0.10 ~11 min)

**Sign in:** Admin.

1. In MAC, go to Copilot > Cost Management. Note the Overview, Consumption and Configuration tabs. ⏱ ~1.5 min
2. Open Configuration. Confirm the four pre-staged policies match the table in the guide (scope, Agents and services, limits, billing method). ⏱ ~1.5 min
3. Open "Standard (PAYG)" and walk through its sections: scope, agents and services, limits and alerts, model profile and billing method. ⏱ ~2 min
4. 📺 Recap from the intro: U10 is in no group that a Cowork policy targets, so U10 has no access (Clip A).

**Checkpoint:** The student can say which users have Cowork access, and why.

*Removed:* the Cowork tabs tour (S8 covers it) and the U10 sign-in.

### S2. Configure a policy: agent availability, model availability and spending limits (⏱ ~13 min; v0.10 ~14 min)

**Sign in:** Admin.

1. Configuration > + Add spending policy. ⏱ ~0.5 min
2. Name it "Extended limit (approved requests)". Switch from All users to Specific groups and select SG-AI-Extended. ⏱ ~1.5 min
3. In Select agents and services, select Cowork. Turn Auto-apply new services off. ⏱ ~1 min
4. In Set limits and alerts: limited monthly budget 10,000 credits; monthly budget limit for users 5,000; policy alert at 80% to the admin; user notifications on at 80%. ⏱ ~2.5 min
5. In Model profiles, choose Customize model selection > Create new model profile. Name it "Cost-aware models", select two models, and allow Microsoft to select the most comparable model. ⏱ ~2.5 min
6. Select billing method: Change > Azure subscription "Lab-PAYG". ⏱ ~2 min
7. Review, then Create spending policy. Confirm it appears in Configuration. ⏱ ~2 min
8. Open Copilot > Cowork > Settings and find the model and AI provider settings (tenant-wide model availability). ⏱ ~1 min

**Checkpoint:** The new policy is listed, scoped to SG-AI-Extended (0 members), with Cowork, a model profile and PAYG billing. The student can explain the model profile vs tenant model settings.

*Changed:* the alert goes to the admin only (the people picker for U06 is practised once, in S3).

### S3. Limits and alerts on a live policy (⏱ ~4 min; v0.10 ~6 min)

**Sign in:** Admin.

1. 📺 In the guide: screenshot of the Standard policy alert email (70% or more), with a note that it repeats daily. ⏱ ~0.5 min
2. In Cost Management > Overview, review Top actions: Standard (70.8%) and Marketing (100%) are flagged, as are U01 and U02. ⏱ ~1.5 min
3. Edit "Standard (PAYG)": add U06 as a second alert recipient, confirm user notifications at 80%, then Save changes. ⏱ ~2 min

**Checkpoint:** The student can explain policy limit vs per-user limit, and admin alerts vs user notifications.

*Moved to stretch:* opening the admin mailbox.

### S4 + S5. See it from the user side (📺 ⏱ ~2 min; v0.10 ~28 min with 5 user switches)

**Sign in:** None. Students read one guide page while the room screen loops the clips.

| Clip | User | What it shows | Teaching point |
|---|---|---|---|
| B | U01 (97.5%) | `/cost` before and after the standard lab task; the task completes even though it crosses the limit | Approximate task cost and remaining credits; enforcement isn't mid-task |
| C | U02 (100%) | Blocked message and the request option; request submitted | Personal limit |
| D | U08 (30% personal, Marketing at 100%) | Blocked despite personal headroom | Shared policy limit |
| E | U10 | First-time access request | Requests for access, not just more credits |

**Checkpoint:** The student can explain the difference between a personal limit and a shared policy limit. The three requests they'll approve in S6 are the ones in the clips.

### S6. Admin reviews and approves requests (⏱ ~13 min; v0.10 ~27 min)

**Sign in:** Admin.

1. Overview > Top actions > View requests. Three pending requests: U02, U08 and U10 (all pre-staged). ⏱ ~1 min
2. Open U10's request ("Not in a policy"). Approve it, and add U10 to SG-AI-Standard. ⏱ ~3 min
3. Open U02's request (Standard). Approve it, and move U02 from SG-AI-Standard to SG-AI-Extended. U02's 2,000 credits carry forward, leaving 3,000 under the new 5,000 limit. ⏱ ~3.5 min
4. Open U08's request (Marketing). Approve it, and raise the Marketing monthly limit from 4,000 to 6,000. U07 and U08 both regain headroom (66.7% used). ⏱ ~2.5 min
5. Create a custom request policy: Credit requests > Request policies > Add request policy. All products and services, the redirect URL and user message (type-text). Save. ⏱ ~3 min
6. 📺 Wrap-up (Clip F): U01 requests more credits and sees the redirect message; the request shows in MAC as "Handled externally". U02 and U10 now have access.

**Checkpoint:** Three requests resolved, each with a different fix; a request policy that routes future requests to an external process.

*Moved to wrap-up:* the U01 redirect and the U02/U10 confirmations. *Moved to stretch:* exporting the requests list.

### S7. Capacity packs vs PAYG vs both (⏱ ~6.5 min; v0.10 ~19 min)

**Narrative:** "Finance says Cowork stopped working, but their policy is only at 15%."

**Sign in:** Admin.

1. Consumption > Policies view: Finance shows 15% utilisation, billing method "Prepaid capacity packs". ⏱ ~1 min
2. Overview: open the Prepaid Capacity pack credits usage card. 1,500 of 1,500 MAC credits used, because 23,500 are allocated to a PPAC environment. ⏱ ~2 min
3. Compare the three funding set-ups using the table in the guide: Finance (pack only) blocked; Pilot (pack plus PAYG) overflows to PAYG (📺 Clip G: U09 runs a task); Standard and Marketing (PAYG only) unaffected by the pack. ⏱ ~1 min
4. Course-correct: edit the Finance policy's billing method and add "Lab-PAYG". Save. Scope, limits, alerts and services are kept. ⏱ ~2 min
5. Guide sidebar: the other two levers, reduce the PPAC allocation, or buy more packs or P3 (P3 purchases are final). Shown live at wrap-up. ⏱ ~0.5 min

**Checkpoint:** The student can explain, for each billing method, what happens when prepaid credits run out.

*Moved to wrap-up:* U09 and U04 sign-ins, the PPAC demo and the P3 talk track.

### S8. Monitor spending and course-correct on delivered value (⏱ ~9.5 min; v0.10 ~13 min)

**Sign in:** Admin.

1. Cost Management > Overview: Total Copilot Credits used, Prepaid Capacity pack card, Pay-as-you-go card, Active users, spending trend chart. ⏱ ~1.5 min
2. Consumption > Policies, then the Users view: select U02 to see daily usage, spending policy history (Standard then Extended) and credits by policy. ⏱ ~2.5 min
3. Copilot > Cowork > Usage: active users, total tasks, tasks by type (user-initiated or scheduled). ⏱ ~1 min
4. Copilot > Cowork > Value: assisted hours, then Assisted hours by task category. ⏱ ~2 min
5. Make one course-correction based on value (Marketing limit, move U01 to Extended, or keep Pilot for U09's scheduled tasks). ⏱ ~2.5 min

**Checkpoint:** The student names one change, the spend evidence and the value evidence behind it.

*Moved to stretch:* the Groups view and exporting a report.

### Stretch exercises (for fast finishers)

Original stretches A to F are kept. New ones, for students who want the hands-on user experience:

- **Stretch G, see it for yourself:** in an InPrivate window, sign in as U02 or U10 and confirm access after your S6 approvals (allow time for changes to apply).
- **Stretch H, external requests:** sign in as U01, request more credits and see your redirect message; then act on the "Handled externally" item in MAC.
- **Stretch I, Finance restored:** sign in as U04 and confirm Cowork works after your S7 billing change.
- **Stretch J, alerts in the inbox:** open the admin mailbox and find the Standard policy alert.
- **Stretch K, reports:** Consumption > Groups view (SG-AI-Marketing), and export the requests list and a usage report.

---

## 5. Room screen run of show

| When | Segment | Content | Source |
|---|---|---|---|
| 0:00 to 0:05 | Intro | 2 min: Contoso story and lab goals. 3 min: "before" montage of Clips A to E (U10 no access, U01 `/cost` and task, U02 blocked and requests, U08 blocked by shared pool, U10 requests access) | Recorded clips, voiced live; "before" tenant as backup |
| 0:05 to 1:10 | Hands-on | Clips A to G loop silently with large labels ("Clip C: U02 personal limit"), so students can look up when the guide points them there | Recorded loop |
| 1:10 to 1:15 | Wrap-up | 3 min: "after" montage: U02 and U10 now have access (Clip F), U01's redirect message, U04 working after the billing change, U09 PAYG overflow on the Consumption page, PPAC allocation lever and P3 in 30 seconds. 2 min: recap and close | "After" tenant, live, with recorded fallback |

| Clip | Content |
|---|---|
| A | U10 opens Cowork: no access |
| B | U01 `/cost`, runs the standard task, `/cost` again |
| C | U02 blocked by personal limit, submits a request |
| D | U08 blocked by the shared Marketing limit |
| E | U10 requests first-time access |
| F | After approvals: U02 and U10 have access; U01 sees the redirect message |
| G | U09 runs a task on PAYG overflow; U04 works after the Finance billing change |

> **Speaker note:** the intro and wrap-up are tight at 5 minutes each. If the montage runs long, drop the live voice-over and let the loop carry Clips A to E during the first minutes of hands-on, while students do S0 and S1.

---

## 6. Timing summary

| Scenario | v0.10 novice estimate (min) | v0.11 novice estimate (min) | User switches v0.10 → v0.11 |
|---|---|---|---|
| S0 Get started | 3 | 3 | 0 → 0 |
| S1 Orientation | 11 | 5 | 1 → 0 |
| S2 Configure a policy | 14 | 13 | 0 → 0 |
| S3 Limits and alerts | 6 | 4 | 0 → 0 |
| S4 How users hit a limit | 19 | 2 (S4 + S5, watch) | 3 → 0 |
| S5 Users request credits | 9 | (included above) | 2 → 0 |
| S6 Approve requests | 27 | 13 | 3 → 0 |
| S7 Capacity packs vs PAYG | 19 | 6.5 | 2 → 0 |
| S8 Monitor and course-correct | 13 | 9.5 | 0 → 0 |
| **Total** | **121** | **56** | **11 → 0** |

Against 65 minutes of hands-on time, that leaves ~9 minutes of buffer for a novice. A confident attendee (~65% of novice time, ~36 min) has ~28 minutes for stretch exercises.

### Trim levers if pilot testing runs long

| Lever | Saves | Trade-off |
|---|---|---|
| Pre-create the "Cost-aware models" profile; students just select it in S2 | ~1.5 min | Students don't build a model profile |
| Replace the Cowork Settings check (S2 step 8) with a guide screenshot | ~1 min | Tenant model settings become watch-only |
| Move the custom request policy (S6 step 5) to stretch | ~3 min | Request routing becomes watch-only |
| Drop the Standard alert edit (S3 step 3) | ~2 min | No hands-on alert edit on a live policy |
