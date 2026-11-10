# @lab.Title

## Lab overview

You're the Microsoft 365 admin at **Contoso**. Contoso has used Microsoft 365 Copilot for months, and now teams want Cowork and agents, which are billed by usage in Copilot Credits. In this lab, you'll set up the controls for that spend, then use them to act on two weeks of usage.

You'll work in two tenants:

| Part | Where Contoso is | Exercises |
|---|---|---|
| Part 1: Set up  | November 1. Usage-based billing isn't turned on yet, and there are no spending policies. | 1, 2 and 3 |
| Part 2: Operate | November 16, two weeks later. The Sales policies from Part 1 are in place, plus one for Finance, with two weeks of usage data. | 4 and 5 |

| Exercise | Time | What you'll do |
|---|---|---|
| 1 | 8 minutes | Turn on usage-based billing with a default policy for everyone |
| 2 | 9 minutes | Open Cowork to the Sales team as a pilot, with guardrails |
| 3 | 8 minutes | Put a budget on the Sales team's agents |
| 4 | 8 minutes | Navigate to the link, then find the policies and people that need action |
| 5 | 12 minutes | Unblock Finance's power user without raising everyone's limits |

### How this lab works

- Text formatted like +++this example+++ is type text. Click in the box you want to fill, then select the text, and it's typed for you.
- Select the check box next to each step when you finish it.
- In Part 2, you'll open new link in another window, so you stay signed in with the same user.
- About 25 minutes into the hands-on time, the presenter will ask everyone to move to Part 2, even if you haven't finished.
- Need help? Raise your hand and a proctor will come to you.

===

### Sign in to Tenant

1. [] Sign in to Windows. If you see the lock screen, select @lab.CtrlAltDelete first. Select each value to type it:
    - Username: +++@lab.VirtualMachine(Win11-Pro-Base).Username+++
    - Password: +++@lab.VirtualMachine(Win11-Pro-Base).Password+++
2. [] On the desktop, double-click **Microsoft Edge**. If Edge shows a welcome or setup screen, close it.
3. [] Click in the Edge address bar, select +++https://admin.cloud.microsoft+++, then press **Enter**.
4. [] Click in the email box, select +++admin@@lab.CloudCredential(WWLM365E7).TenantName+++, then select **Next**.
5. [] Click in the password box, select +++@lab.CloudCredential(WWLM365E7).Password+++, then select **Sign in**.
6. [] If you're asked **Stay signed in?**, select **Yes**.
7. [] Check that the **Microsoft 365 admin center** home page opens. Keep this Edge window open.

> [!Help] Type text goes wherever your cursor is, so click in the right box before you select it. If sign-in still fails, raise your hand.

===

## Exercise 1: Turn on usage-based billing with a default policy for everyone

⏱ About 8 minutes ·

**Scenario:** It's November 1. Contoso uses Microsoft 365 Copilot, but Cowork and other usage-based experiences stay off until you turn on usage-based billing. The CIO and CFO agree to let everyone try them under a safe ceiling: $20 a person a month, any model, paid from the Azure subscription **Lab-PAYG**, with a warning at 80%.

**Goal:** Turn on usage-based billing with a default spending policy for all users: 2,000 credits ($20) a person, 20,000 credits for the organization, and alerts at 80%.

1. [] In the admin center's left navigation, select **Copilot** > **Cost Management**. If you don't see **Copilot**, select **Show all** first.
2. [] Select **Get started**. You should see the panel **Activate the default spending policy for your organization**.
3. [] In the **Billing method** section, open the subscription list and select **Lab-PAYG**. Don't select **Create new**.
4. [] Select **Advanced billing settings** to expand it. Keep the region that's selected as default.
5. [] In **Set the monthly spending limit for this policy**, select **Limit monthly spending**, then enter +++20000+++.
6. [] Turn on the monthly spending limit for users, then enter +++2000+++.
7. [] In **Define alerts**, set the threshold to +++80+++ percent. Your admin address is already filled in as the recipient.
8. [] Select **Customize setup configuration** and review what the policy covers: **All users**, all supported services and the default models. Don't change anything.
9. [] Check that **Auto-apply new services** is on, and leave it on.
10. [] Select **Activate**. When setup is complete, select **Manage Configuration**.
11. [] On the **Configuration** tab, check that **Default spending policy** is listed as **Enabled**.

===

## Exercise 2: Open Cowork to Sales as a pilot, with guardrails

⏱ About 9 minutes · 

**Scenario:** The Sales VP's team wants to use Cowork for proposals, account research and pipeline analysis, and $20 a month won't last them. You agree to a pilot with guardrails: Cowork only, $2,000 a person and $10,000 for the team, a warning before anyone is cut off, and a short list of approved models.

**Goal:** Create the policy **Sales Cowork pilot** for Contoso Sales, with the model profile **Sales no frontier models**: 1,000,000 credits for the team, 200,000 a person, and alerts at 80%.

### Choose who the policy covers

1. [] On the **Configuration** tab, select **+ Add spending policy**.
2. [] In the name box, enter +++Sales Cowork pilot+++.
3. [] For the scope, select **Identity**.
4. [] Switch from **All users** to **Specific groups**. Search for +++Contoso Sales+++, select **Contoso Sales**, then select **Next**.

### Choose the service

5. [] In **Select agents and services**, select **Cowork** only. You can find this checkbox under **Microsoft Copilot**
6. [] Turn off **Auto-apply new services**, then select **Next**.

### Set limits and alerts

7. [] Select **Limited monthly budget** and enter +++1000000+++.
8. [] Turn on the monthly budget limit for users and enter +++200000+++.
9. [] Set the policy alert threshold to +++80+++ percent. Your admin address is already a recipient.
10. [] Turn on user notifications at +++80+++ percent, then select **Next**.

### Choose the models

11. [] In **Model profiles**, select **Customize model selection** > **Create new model profile**.
12. [] Name the profile +++Sales no frontier models+++.
13. [] Select **[STANDARD MODEL 1]** and **[STANDARD MODEL 2]**. Leave every other model cleared, including the frontier models.
14. [] Select **Microsoft can select the most comparable model to maintain availability**.
15. [] Select **Save**, then select **Next**.

### Choose billing and create the policy

16. [] In **Select billing method**, keep **Lab-PAYG**, then select **Next**.
17. [] Review each section, select **Create spending policy**, then select **Done**.
18. [] Check that the **Configuration** tab lists two policies: **Default spending policy** and **Sales Cowork pilot**.

===

## Exercise 3: Put a budget on Sales agents

⏱ About 8 minutes · 

**Scenario:** The Sales team builds its agents in one Copilot Studio environment, **Contoso Sales Projects**. It holds the **Sales Agent**, which goes live to the team this week, and **Proposal Helper**. Every conversation uses credits. Pete Pipeline owns both agents. Finance wants a monthly cap, and you and Pete should both hear when spend gets close.

**Goal:** Create one resource-based policy.

In the policy steps, select **Next** to move on to each new step.

1. On the **Configuration** tab, select **+ Add spending policy**.
2. Name the policy +++Sales Agent+++, then select **Resources** as the scope.
3. Select **Resource collection**. Search for +++Sales Agent Test Environment+++, then select **Sales Agent Test Environment**. It's listed with its environment, Contoso Sales Projects.
4. Set the monthly spending limit to +++300000+++.
5. Set the alert threshold to +++80+++ percent. Your admin address is already a recipient. Search for +++Pete Pipeline+++ and add him.
6. Keep **Lab-PAYG** as the billing method.
7. Review the settings, then select **Create spending policy**.

### Check your work

1. [] On the **Configuration** tab, check that your new policy is listed with a **Resources** scope.

===

Part 2 starts here: the same Contoso two weeks later, on Monday, November 16. The **Sales Cowork pilot** and **Sales environment agents** policies are live. IT also added **Finance Cowork** on November 1, when Finance asked for room for its month-end close.

1. [] In Edge, open an InPrivate window: press **Ctrl+N**, or select **Settings and more** (**...**) > **New window**.
2. [] Click in the address bar, select +++https://admin.cloud.microsoft/?pkgver=Rolling_261110.33_V2&hvc=bigmac:pkgver=PR_261110.242_V2&vnext=true#/copilot/costmanagement/overview+++, then press **Enter**.
3. [] Select **Copilot** > **Cost Management**. You should see the **Overview** tab with two weeks of data.

===

## Exercise 4: Find the policies and people that need action

⏱ About 8 minutes

### Find what needs action

**Scenario:** There are 15 days left in the month. The CFO wants a two-line update: how much has Contoso spent so far, and what needs action?

1. [] On the **Overview** tab, review the tiles at the top. You should see:
    - **Total Copilot Credits used**: 1,330,000
    - **Prepaid capacity pack credits used**: 0
    - **Pay-as-you-go credits used**: 1,330,000
    - **Active users of Copilot Credits**: 8
2. [] Review the cards that flag what needs action. You should see:
    - **Policies approaching or at limit**: **Finance Cowork**, at 750,000 of 1,200,000 credits (62.5%). It's marked **Needs action** because it's past its 60% alert threshold.
    - **Users at ≥90% of spending limit**: **Sally Sales**, at 190,000 of 200,000 credits (95%), and **Fiona Forecast**, at 450,000 of 500,000 credits (90%)
3. [] Scroll down to the spending cards. You should see:
    - **Spending**: $13,300.00 estimated spend this month. The second week (November 9 to 15) is 50% higher than the first, with weekday peaks of 140,160 credits ($1,401.60).
    - **Agents and services spending the most credits (month to date)**: **Cowork**, 1,150,000 credits, and **Copilot Studio**, 180,000 credits
    - **Top users by cost**: Fiona Forecast $4,500.00, Sally Sales $1,900.00, Polly Procurement $1,500.00, Bill Budget $1,500.00 and Pete Pipeline $800.00
4. [] Select the **Consumption** tab. The **Policies** view is sorted by **Credits used**.

5. [] Switch to the **Users & groups** view, and set **Group by** to **All users**. The list is sorted by **Total credits used**. 

6. [] Select **Fiona Forecast** to open her details. You should see her daily usage under **Finance Cowork**: 31,296 credits each weekday from November 2 to 6, rising to 46,944 each weekday from November 9 to 13.

===

## Exercise 5: Unblock Finance's power user

⏱ About 12 minutes

**Scenario:** Fiona Forecast, FP&A Analyst, has used 450,000 of her 500,000 credits with 15 days left, in the middle of the monthly forecast refresh. Bill Budget, the Finance Director, asks you to keep her working without letting Finance's budget run away.

**Goal:** Create the security group **Copilot Power Users**, add Fiona, and give the group its own policy: 1,000,000 credits a person, 2,000,000 for the group, Cowork only, and alerts at 80%.

### Weigh the options

| Option | The change | What happens | Verdict |
|---|---|---|---|
| A: Raise the team limit | Raise Finance Cowork's 1,200,000 team limit | Fiona is still capped by her 500,000 personal limit, with only 50,000 credits left. | Doesn't help Fiona |
| B: Raise everyone's personal limit | Per-user limit from 500,000 to 1,000,000 for all of Finance | Polly and Bill, at 30% of their limits, get room they don't need. All three still share a team limit that's already at 62.5%. | Raises the ceiling for everyone to fix one person |
| C: A power user group | A new group, Copilot Power Users, with its own policy at 1,000,000 a person. Fiona joins it. | Fiona's 450,000 credits carry forward: 45% of her new limit, with 550,000 left. Nobody else's limits change. | Fixes it |

You'll build option C.

1. [] Select the **Configuration** tab, then select **Finance Cowork**. Find the two levers: the policy limit (1,200,000) is option A, and the per-user limit (500,000) is option B. Close the panel without saving.

### Create the power user group

2. [] In the left navigation, select **Teams & groups** > **Active teams & groups**, then select the **Security groups** tab. If you don't see **Teams & groups**, select **Show all** first.
3. [] Select **Add a security group**.
4. [] On **Set up the basics**, enter the name +++Copilot Power Users+++ and the description +++Approved Copilot power users with higher limits+++, then select **Next**.
5. [] On **Edit settings**, don't change anything, then select **Next**.
6. [] Review your selections, select **Create group**, then select **Close**.
7. [] In the **Security groups** list, select **Copilot Power Users**. If it isn't listed yet, refresh the page.
8. [] Select the **Members** tab, then select **View all and manage members**. Search for +++Fiona+++, select **Fiona Forecast**, then select **Add**. Close the panel. Fiona stays in Contoso Finance too.

===

## Exercise 5: Unblock Finance's power user (continued)

### Give the group its own policy

9. [] Select **Copilot** > **Cost Management** > **Configuration**, then select **+ Add spending policy**.
10. [] Name the policy +++Copilot Power Users+++, then select **Identity** as the scope.
11. [] Switch from **All users** to **Specific groups**. Search for +++Copilot Power Users+++, select it, then select **Next**. If the group isn't listed yet, wait a minute and search again.
12. [] In **Select agents and services**, select **Cowork**. Turn off **Auto-apply new services**, then select **Next**.
13. [] Select **Limited monthly budget** and enter +++2000000+++.
14. [] Turn on the monthly budget limit for users and enter +++1000000+++.
15. [] Set the policy alert threshold to +++80+++ percent. Turn on user notifications at +++80+++ percent, then select **Next**.
16. [] In **Model profiles**, keep the default models (don't customize the model selection), then select **Next**. These are the same models Fiona had in Finance.
17. [] In **Select billing method**, keep **Lab-PAYG**, then select **Next**.
18. [] Review the settings, select **Create spending policy**, then select **Done**. Check that the **Configuration** tab now lists four policies, including **Copilot Power Users**.

### Check the result

19. [] Select the **Overview** tab and refresh the page. Once the change applies, **Fiona Forecast** is no longer in **Users at ≥90% of spending limit**. **Sally Sales** is still there at 95%, because you changed Fiona's limit only.
20. [] Select the **Consumption** tab, then the **Users & groups** view. Fiona's 450,000 credits carry forward against her new 1,000,000 limit: 45% used, with 550,000 left. **Finance Cowork** keeps the 750,000 credits used before the move, and **Copilot Power Users** shows no credits yet.

> [!Note] Group membership and dashboard updates can take a few minutes. If you don't see the change yet, check again later.

**If you have time:** so Finance's owners don't get a daily alert for the rest of the month, select **Finance Cowork**, change its policy alert threshold from 60 to +++95+++ percent, then select **Save changes**.

You've finished the hands-on part of the lab. Look up at the room screen for the closing.
