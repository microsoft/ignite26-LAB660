# @lab.Title

## Lab overview

You're the Microsoft 365 admin at **Contoso**. Contoso has used Microsoft 365 Copilot for months, and now teams want to use Cowork and agents, which are billed by usage in credits ($0.01 = 1 credit). In this lab, you'll set up the controls for Contoso's usage-based AI services, setup spending policies for Cowork and Agent environment, and modify spend limits after analyzing the value from two weeks of the company's Cowork consumption.

The lab includes two parts:

| Part | Where Contoso is on their AI journey | Exercises |
|---|---|---|
| Part 1: Activate AI consumption and initial policies  | November 1. Usage-based billing isn't turned on yet, and there are no spending policies configured yet. | 1, 2 and 3 |
| Part 2: Adjust policies | November 16, two weeks later. The Sales policies from Part 1 are in place, plus one for Finance, with two weeks of usage data. | 4 and 5 |

| Exercise | Time | What you'll do |
|---|---|---|
| 1 | 8 minutes | Turn on usage-based billing with a default spend policy for all users |
| 2 | 9 minutes | Setup a Cowork pilot for the Sales team, with model and spend guardrails |
| 3 | 8 minutes | Set a limit on the Sales team's agents (using a specific environment) |
| 4 | 8 minutes | Understand the users and their spend policies that require action |
| 5 | 12 minutes | Unblock Finance's power user without raising everyone's limits |

### How this lab works

- Text formatted like +++this example+++ is type text. Click in the box you want to fill, then select the text, and it's typed for you.
- Select the check box next to each step when you finish it.
- In Part 2, you'll open a new link in another window, so you stay signed in with the same user.
- About 25 minutes into the hands-on time, the presenter will ask everyone to move to Part 2, even if you haven't finished.
- Need help? Raise your hand and a proctor will come to you.

===

### Sign in to Tenant

1. [] Click the Sign in button and you should be promted for a Microsoft email sign in (skip to Step 4) otherwise
2. [] If your virtual machine has not opened up and your Edge browser hasnt loaded then raise your hand or try to sign in to Windows. If you see the lock screen, select Sign in. Use the following credentials if asked for:
    - Username: +++@lab.VirtualMachine(Ignite26LAB660).Username+++
    - Password: +++@lab.VirtualMachine(Ignite26LAB660).Password+++
    - If sign in doesnt work select @lab.CtrlAltDelete first
3. [] **Microsoft Edge** session must be open. If not then on the desktop, double-click **Microsoft Edge**. If Edge shows a welcome or setup screen, close it.
4. [] Click in the Edge address bar, select +++https://admin.cloud.microsoft+++, then press **Enter**.
5. [] Click in the email box, select +++@lab.CloudCredential(PoolB).Sign-inName+++, then select **Next**.  Check the Resources tab if the signin information is not available here.
6. [] You should be asked to 'Enter Temporary Access Pass' - Click into the password box, select +++@lab.CloudCredential(PoolB).Sign-inCode+++, then select **Sign in**.
7. [] If you're asked **Stay signed in?**, select **Yes**.
8. [] Check that the **Microsoft 365 admin center** home page opens. Keep this Edge window open.

> [!Help] Type text goes wherever your cursor is, so click in the right box before you select it. If sign-in still fails, check the resources tab for the email and password. If that still fails, raise your hand.

===

## Exercise 1: Turn on usage-based billing with a default policy for everyone

⏱ About 8 minutes ·

**Scenario:** It's November 1. Contoso uses Microsoft 365 Copilot, but Cowork and other usage-based experiences stay off until you turn on usage-based billing. The CIO and CFO agree to let everyone try them under a safe ceiling: $20 a person a month, any model, paid from the Azure subscription, with a warning at 80%.

**Goal:** Turn on usage-based billing with a default spending policy for all users: 2,000 credits ($20) a person, 15,000 credits ($150) for the organization, and alerts at 80%.

**Note:** You may encounter fields that ask for credits in some places and $ in others. Remember 1 credit = $0.01 or $1.00 = 100 credits. This is to be expected as the product teams are still rolling out a more standard way to set limits based on local currency.

1. [] In the admin center's left navigation, select **Copilot** > **Cost Management**. If you don't see **Copilot**, select **Show all** first.
2. [] Select **Get started**. You should see the panel **Activate the default spending policy for your organization**.
3. [] In the **Billing method** section, Uncheck **Use Capacity Packs**.
4. [] Select **Use pay-as-you-go subscription**. Select the available subscription.
5. [] In **Set the monthly spending limit for this policy**, select **Limit monthly spending**, then enter either +++15000+++ credits or +++150+++ USD.
6. [] In **Select monthly budget limits for users**, select **limit monthly spending per user**, then enter +++2000+++ credits or +++20+++ USD.
7. [] Toggle on **Define alerts**. Your admin address is already filled in as the recipient. Set the threshold to +++80+++ percent.
8. [] Select **Customize setup** and review what the policy covers: **All users**, and all supported services. Don't change anything.
9. [] Click the **Agents and services** section and verify that the top toggle **Allow new Agents and services as they become available** is enabled.
10. [] Click **Save changes** and then Select **Activate**. Be patient - this step could take 60-90 seconds.
11. [] When setup is complete, select **Manage Configuration** and you'll be taken to the **Copilot > Cost Management** tab where we'll focus our attention.  
12. [] On the **Configuration** sub-tab, check that the default **All Users Policy** is listed as **Enabled**.

===

## Exercise 2: Setup a Cowork pilot for the Sales team, with model and spend guardrails

⏱ About 9 minutes · 

**Scenario:** The Sales team wants to pilot an increase in their team's Cowork credits to support sales proposals, account research and pipeline analysis. They anticipate needing more than the current default of $20 based on recent usage patterns.  a month won't last them. You all agree to a scaled up pilot with guardrails: Cowork only, $2,000 a person and $10,000 for the team, a warning before anyone is cut off, and a scoped list of approved models.

**Goal:** Create the policy **Sales Cowork pilot** for Contoso Sales, with the model profile **Sales no frontier models**: 1,000,000 credits (or $10,000) for the team, 200,000 credits (or $2,000) a person, and alerts at 80%.

### Choose who the policy covers

1. [] On the **Configuration** tab, select **+ Add spending policy**.
2. [] In the name box, enter +++Sales Cowork pilot+++.
3. [] For the scope, select **Identity**.
4. [] Switch from **All users** to **Specific groups**. Search for +++Contoso Sales+++, select **Contoso Sales**, then select **Next**.

### Choose the service

5. [] **Turn off** Allow new Agents and services as they become available.
6. [] Under **Microsoft Copilot**, select **Cowork** only. Uncheck all other services then select **Next**.

Continue to the next page to complete Exercise 2.

===

## Exercise 2 (continued): Setup a Cowork pilot for the Sales team, with model and spend guardrails

### Set limits and alerts

7. [] In **Set the monthly spending limit for this policy**, select **Limit monthly spending**, then enter +++1000000+++ credits or +++10000+++ USD.
8. [] In **Select monthly budget limits for users**, select **limit monthly spending per user**, then enter +++200000+++ credits or +++2000+++ USD.
9. [] Toggle on **Define alerts**. Your admin address is already filled in as the recipient. Set the monthly spending alert threshold (the top one) to +++80+++ percent of limit.
10. [] Set the user alert threshold to +++80+++ percent, then select **Next**.
    
### Choose the models

11. [] In **Model Template**, select **Customize model selection** > **Create new model profile**.
12. [] Name the profile +++Sales no frontier models+++.
13. [] Select **Anthropic > Opus** and **OpenAI > Sol**. The models **Anthropic > Sonnet** and **OpenAI > Terra** are required. Leave every other model unchecked, including the frontier models such as **Anthropic > Fable** and **OpenAI > Astra** as you do not need to give the most expensive models to the sales team yet and want to help them stretch their spend limits.
14. [] Select **Save**, then select **Next**.

### Choose billing and create the policy

16. [] In **Billing method**, keep the default billing method and default subscription selected. Select **Next**.
17. [] Review each section, select **Create spending policy**, then select **Done**. Congrats! You added a spend policy for the Cowork AI service scoped to a specific group and limited access to the most expensive frontier models!
18. [] Check that the **Configuration** tab lists two policies: the default **All Users Policy** (from Exercise 1) and newly created **Sales Cowork pilot**.

===

## Exercise 3: Set a limit on the Sales team's agents (using a specific environment)

⏱ About 8 minutes · 

**Scenario:** The Sales team builds its agents in one Copilot Studio environment, **Sales Agent Test Environment**. In practice it will hold multiple resources such as a **Sales Leads Agent**, which goes live to the team this week, and **Proposal Helper Workflow**. Every conversation uses credits. Pete Pipeline owns both agents. Finance wants a monthly cap, and you and Pete should both know when spend gets close.

**Goal:** Create one specific **environment**-based policy.

1. [] On the **Configuration** tab, select **+ Add spending policy**, then select **Next**.
2. [] Name the policy +++Sales Agent+++,
3. [] Select **Resources** as the scope and then Select **Resource collection** (be sure you did not select **Specific resource**)
5. [] Under **Resource collection** select **Specific environments**. Search for +++Sales Agent Test Environment+++, then select **Sales Agent Test Environment**, then select **Next**.
6. [] No action needed on the **Review agents and services** pane (however, if you have Copilot Studio environments that contain agents, workflows, and apps you'd be able to set policies for those specific resources as well). You can proceed by clicking **Next**
7. [] In **Set the monthly spending limit for this policy**, select **Limit monthly spending**, then enter +++500000+++ credits or +++5000+++ USD.
8. [] In **Select monthly budget limit for agents**, select **Limit monthly spending per agent**, then enter +++250000+++ credits or +++2500+++ USD.
9. [] Toggle on **Define alerts**. Your admin address is already filled in as the recipient. Search for +++Pete Pipeline+++ and add him. You can also toggle on 'Notify agent maker' if you wish. Set the alert thresholds to +++80+++ percent, then select **Next**.
10. [] In **Billing method**, keep the default billing method and default subscription selected, then select **Next**.
11. [] Review the settings, then select **Create spending policy**.

### Check your work

1. [] On the **Configuration** tab, check that your new 'Sales Agent' policy is listed with a **Budget scope** as **1 environment**.

===

Part 2 of the Lab starts here: It's now Monday, November 16 and two weeks have passed since Contoso has started consuming their new Cowork and Sales Agent AI services. The **Sales Cowork pilot** and **Sales environment agents** policies are live. IT also added a **Finance Cowork** policy on November 1, when Finance asked for additional AI spend to support the company's month-end close processes with Cowork.

1. [] In Edge, open a new browser tab by clicking the "+" icon next to the open tab.
2. [] Click in the address bar, select +++aka.ms/lab660+++, then press **Enter**.
3. [] Select **Copilot** > **Cost Management**. You should see the **Overview** tab with two weeks of spend data.

===

## Exercise 4: Find the policies and people that need action

⏱ About 8 minutes

### Find what needs action

**Scenario:** There are 15 days left in the month. The CFO wants a two-line update: how much has Contoso spent so far, and what needs action?

1. [] On the **Overview** tab, review the tiles at the top. You should see:
    - **Total Copilot Credits used**: 1.3 Million
    - **Active users of Copilot Credits**: 8
    - **Cost this month**: $13K
    - **Value**: $51K
2. [] Review the cards that flag what needs action. You should see:
    - **Policies approaching or at limit**: **Finance Cowork**, at $7,500 of $12,000 (63%). It's marked **Needs action** because it's past its 60% alert threshold.
    - **Users at ≥90% of spending limit**: **Sally Sales**, at $1,900 of $2,000 (95%), and **Fiona Forecast**, at $4,500 of $5,000 (90%)
3. [] Scroll down to review the **Agent cost & value** insights on each card. You'll see:
    - **Cost**: $13,300.00 estimated spend month to date and a forecasted spend of $26,600 by month-end.
    - **Top agents and services by cost**: **Cowork**, $11,500, and **Sales Agent**, $1,800 spent.
    - **Top users by cost**: Fiona Forecast $4,500.00, Sally Sales $1,900.00, Polly Procurement $1,500.00, Bill Budget $1,500.00 and Pete Pipeline $800.00.
    - **Value vs. cost** shows a large bubble representing **Cowork** and a smaller bubble representing **Sales agent**. The services are plotted based on the average economic value generated per session vs. average AI cost per session. **Cowork** has many more sessions (across many use cases) but in aggregate seems to be generating good value relative to cost. **Sales agent** may have room for improvement as the session costs seem high relative to the value (potential room to optimize).
    - **Top use cases by cost** shows at a glance the business activities connected to the AI spend - we will take a closer look at this later.
4. [] Select the **Consumption** sub-tab to see the active **Policies** sorted by **Cost**.

5. [] Switch to the **Users & groups** view. The list is set to **Group by** **All users**. The list is sorted by **Total credits used**. 

6. [] Select **Fiona Forecast** to open her details. You should see her daily usage under **Finance Cowork**. Additionally, her cost should be $4,500 for the first two weeks of November. The **Value** module shows her AI spend generated an estimated $21.6k of value across use cases such as Budget and forecast as well as financial statement preparations which the CFO agrees is AI usage worth scaling. **Note** user-specific visibility into spend, use cases must be enabled by the organization.

7. 5. [] Switch to the **Use cases** view to drill down and explore the spend and value mapped to Domain > Category > Sub-Category to help you understand where the AI spend went and align with the CFO and other business leaders how best to manage the spend. Toggle between **Hierarchy** and **Table** views.
===

## Exercise 5: Unblock Finance's power user

⏱ About 12 minutes

**Scenario:** Fiona Forecast, FP&A Analyst, has used 450,000 of her 500,000 credits with 15 days left, in the middle of the monthly forecast refresh.

**Goal:** Bill Budget, the Finance Director, asks you to help unblock her work without letting Finance's total budget run away.

### Weigh the options

| Option | The change | How to | What happens | Verdict |
|---|---|---|---|---|
| A: Raise the team limit | Raise Finance Cowork's 1,200,000 team limit | Select the **Configuration** tab, then select **Finance Cowork**. Increase the policy limit (1,200,000). For this exercise, close the panel without saving. | Fiona is still capped by her 500,000 personal limit, with only 50,000 credits left. | Doesn't help Fiona |
| B: Raise everyone's personal limit | Per-user limit from 500,000 to 1,000,000 for all of Finance | Select the **Configuration** tab, then select **Finance Cowork**. Increase the per-user limit (500,000). For this exercise, close the panel without saving. | Polly and Bill, at 30% of their limits, get room they don't need. All three still share a team limit that's already at 62.5%. | Raises the ceiling for everyone to fix one person's problem. |
| C: Define a Cowork power user group | A new group, Copilot Power Users, with its own policy at 1,000,000 a person. Fiona joins it. | Exercise 5 below |  Fiona's 450,000 credits carry forward: 45% of her new limit, with 550,000 left. Nobody else's limits change. | Unblocks Fiona (and lays groundwork to unblock power users from other functions) |

**We will build option C.**
===

### Option C: Create the Cowork power user group

2. [] In the left navigation, select **Teams & groups** > **Active teams & groups**
3. [] Be sure to select the **Security groups** sub-tab. 
4. [] Select **Add a security group**.
5. [] On **Set up the basics**, enter the name +++Cowork Power Users+++ and the description +++Approved Cowork power users with higher user limits+++, then select **Next**.
6. [] On **Edit settings**, don't change anything, then select **Next**.
7. [] Review your selections, select **Create group**, then select **Close**.
8. [] In the **Security groups** list, select **Cowork Power Users**. If it isn't listed yet, refresh the page.
9. [] Select the **Members** tab, then select **View all and manage members**. Select **Add members** and search for +++Fiona+++, select **Fiona Forecast**, then select **Add**. Close the panel. Fiona is now part of the Cowork Power Users group as well as her original group Contoso Finance.

===

## Exercise 5: Unblock Finance's power user (continued)

### Give the group its own policy

10. [] Select **Copilot** > **Cost Management** > **Configuration**, then select **+ Add spending policy**.
11. [] Name the policy +++Copilot Power Users+++, then select **Identity** as the scope.
12. [] Switch from **All users** to **Specific groups**. Search for +++Cowork Power Users+++, select it, then select **Next**. If the group isn't listed yet, wait a minute and search again.
13. [] In **Review agents and services**, **turn off** the toggle next to 'Include all agents and services the users have access to'. Next, under **Microsoft Copilot**, select **Cowork** only. Uncheck all other services then select **Next**.
14. [] In **Set the monthly spending limit for this policy**, select **Limit monthly spending**, then enter $ +++20000+++ USD. **Note** we are inputting $ now instead of credits.
15. [] In **Select monthly budget limits for users**, select **limit monthly spending per user**, then enter $ +++10000+++ USD.**Note** we are inputting $ now instead of credits.
16. [] Toggle on **Define alerts**. Set the policy alert threshold to +++80+++ percent. Turn on user notifications at +++80+++ percent, then select **Next**.
17. [] In **Model template**, keep the default selection 'Apply model selection automatically' (don't customize the model selection), then select **Next**. These are the same models Fiona had in Finance.
18. [] In **Billing method**, keep the default billing method and default subscription selected then select **Next**.
19. [] Review the settings, select **Create spending policy**, then select **Done**. Check that the **Configuration** tab now lists four policies, including **Copilot Power Users**.

### Check the result

20. [] Select the **Consumption** tab, then the **Users & groups** view. Fiona's $4,500 spend will continue to carry forward against her new $10,0000 limit: 45% used, with $5,500 left as her new power user policy is more permissive. Other users still governed by the **Finance Cowork** policy, such as Polly Procurement and Bill Budget still have a $5,000 limit. On the **Policies** tab you can see **Cowork Power Users** policy with its $20,000 limit.

> [!Note] Group membership and dashboard updates can take a few minutes. If you don't see the change yet, check again later.

**If you have time:** so Finance's owners don't get a daily alert for the rest of the month, select **Finance Cowork**, change its policy alert threshold from 60 to +++95+++ percent, then select **Save changes**.

You've finished the hands-on part of the lab. Look up at the room screen for the closing.
