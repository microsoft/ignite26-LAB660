# LAB660 attendee instructions

In this 75-minute lab, you will configure an AI spending policy, observe how
the policy affects the user experience, and respond to approval and monitoring
signals in a preconfigured scenario.

## Before you begin

The Skillable environment for this lab must provide:

- An administrator account that can create and assign spending policies,
  configure model-family access, inspect spending and delivered-value signals,
  manage alerts, and change limits.
- A user account in a known test group that can experience policy-controlled
  model availability, review Copilot Credit usage, and submit a credit request.
- A clean starting state for policy creation.
- A separate preconfigured policy scenario with custom credit-request routing,
  seeded usage and spending data, delivered-value signals, and at least one
  actionable alert or limit condition.
- A reliable reset point for each lab instance.

Policy changes must take effect within the exercise window. If propagation is
not predictable, the environment must include pre-staged before-and-after
states.

## Lab flow

| Section | Time | Goal |
|---------|------|------|
| Orientation | 5 minutes | Review the environment, personas, and starting state |
| Exercise 1 | 15 minutes | Create a group-scoped spending and model-access policy |
| Exercise 2 | 15 minutes | Validate model choice and spend visibility in Cowork |
| Exercise 3 | 20 minutes | Route and process a credit request |
| Exercise 4 | 15 minutes | Connect cost to value and take corrective action |
| Recap | 5 minutes | Review the policy lifecycle and key takeaways |

## Orientation

Review the Skillable environment, the available admin and user personas, and
the starting policy configuration.

## Exercise 1: Configure an AI spending policy

In **Microsoft 365 admin center**, use **Copilot > Cost Management** to create
a policy for a test group. Configure the supported agents and services,
model-family access, policy and user spending limits, alerts, and the
appropriate billing method.

## Exercise 2: Validate model choice and spend visibility

Switch to the user persona in **Microsoft Copilot Cowork**. Examine how the
policy affects model choice, then review credit usage, remaining credits,
usage history, and threshold notifications.

## Exercise 3: Route and process a credit request

Use the preconfigured policy scenario to submit a credit request. Follow the
request through the custom URL into the existing automation and approval flow,
then observe the result from both the user and administrator perspectives.

## Exercise 4: Connect cost to value and course correct

Use Agent 365 cost management and the Insights consumption dashboard to review
spending, consumption, and delivered-value signals. Investigate an alert or
limit condition, identify the policy or usage pattern driving it, and adjust
the appropriate control.

## Recap

Review how policy configuration, user experience, approvals, monitoring, and
corrective actions work together across the AI spending lifecycle.
