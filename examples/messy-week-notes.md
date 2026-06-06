# Messy Week Notes

This is an example input for the **Weekly Review Lite** workflow.

## Team context

I’m a first-time tech lead for a product engineering team of six engineers.

The team owns the billing and subscriptions area of a B2B SaaS product. We work with a product manager, a designer, and a customer success lead. We are two weeks into a four-week push to improve plan-change flows before a larger pricing update.

I still contribute code, but I’m also expected to help with delivery planning, code review, technical decisions, and unblocking the team.

## Current goals

* Finish the new plan-change flow by the end of next sprint.
* Reduce billing-related support tickets before the pricing update.
* Avoid introducing regressions in invoice generation.
* Keep the scope small enough that we can release incrementally.

## What happened this week

We made decent progress on the UI work, but the backend work is more tangled than expected.

The current subscription model has several old assumptions baked in. It handles simple upgrades and cancellations, but not mid-cycle downgrades very cleanly. There are several special cases around annual plans, credits, and grandfathered pricing.

One engineer started refactoring the subscription calculation logic because they said the existing code was too hard to safely change. The PR is already large and still growing.

The PM asked whether we are still on track for the release date. I said “probably,” but I don’t feel confident.

Customer Success shared three recent support tickets where customers were confused by invoice adjustments after changing plans. These seem related to the same area of the system we are changing.

The designer has finalised the main happy path, but there are still unanswered questions about edge cases and error states.

## PR/code review concerns

* The main backend PR is over 1,200 lines.
* It changes calculation logic and some API response shapes.
* The test coverage is improving, but mostly around the new intended behaviour.
* I’m not sure we have enough regression coverage for existing billing cases.
* I left some review comments asking whether we can split the PR, but the engineer pushed back and said splitting it would take longer.
* Another engineer approved the PR because they wanted to unblock the work, but I don’t think they reviewed the risk areas deeply.

## Delivery concerns

* We may be underestimating billing edge cases.
* The PM is still thinking of this as a mostly UX-led flow improvement, but the backend complexity is now the main risk.
* We do not have a clear decision on whether mid-cycle downgrades are in scope for the first release.
* QA will probably get squeezed if we keep the current deadline.
* I’m worried we will merge a risky backend change too late in the sprint.

## People concerns

* The engineer working on the backend PR is capable but defensive when asked to reduce scope or split work.
* A junior engineer has been quiet in standups and may be stuck on the UI validation work.
* I have been doing too much async review late at night instead of pairing or clarifying earlier.
* I’m worried I’m becoming the bottleneck, but I also don’t trust the current level of review.

## Stakeholder concerns

* PM wants a confidence update before roadmap planning next week.
* Customer Success wants to know whether the confusing invoice adjustment cases will be fixed in this release.
* Engineering Manager asked me whether the team needs help, and I said we were okay. I’m not sure that was the right answer.

## Decisions made

* We agreed not to redesign the whole billing settings page.
* We agreed to release the plan-change flow behind a feature flag.
* We agreed to add more automated tests around new plan-change scenarios.

## Decisions still open

* Are mid-cycle downgrades in scope?
* Do we support all grandfathered pricing cases in the first release?
* Do we split the backend PR before merging?
* Do we need a regression test matrix before release?
* Do we move the date or reduce scope?

## Things I am avoiding

* Telling the PM that the date may be at risk.
* Having a direct conversation with the backend engineer about the PR size and reviewability.
* Asking my manager for help because I don’t want to look like I can’t handle the role.
* Admitting that I don’t fully understand every billing edge case myself.

## Anything else

I feel like I’m still acting like a senior engineer who reviews hard PRs, rather than a tech lead who makes risk visible earlier.

I want to keep the team moving, but I also don’t want to let a risky billing change slip through because everyone is tired of talking about scope.
