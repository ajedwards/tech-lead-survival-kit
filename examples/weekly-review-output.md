# Weekly Review Output

This is an example output from the **Weekly Review Lite** workflow.

## Summary

This was not a bad week, but the shape of the work changed.

The plan-change flow is no longer mainly a UX delivery task. The main risk is now backend billing complexity, especially around mid-cycle changes, grandfathered pricing, invoice adjustments, and regression coverage.

The highest-leverage tech lead move is to make that risk visible early, reduce ambiguity, and stop the large backend PR from becoming the only place where the real decision-making happens.

## 1. Delivery risks

### Risk 1: The release date may be based on an outdated understanding of the work

**Why it matters:**
The PM still appears to understand this as a mostly UX-led flow improvement, but the work has exposed deeper subscription and invoice-calculation complexity. If that mismatch continues, the team may appear on track until QA or production reveals otherwise.

**Action to take:**
Send a clear update that separates UI progress from backend billing risk. Avoid saying “probably on track” unless the unresolved scope questions are answered.

**Who needs to be involved:**
Tech lead, PM, Engineering Manager, backend engineer, QA if available.

**Classification:**
Urgent.

---

### Risk 2: QA and regression testing may get squeezed

**Why it matters:**
Billing changes have high trust impact. The current test effort appears focused on new intended behaviour, but the larger risk is breaking existing invoice and subscription scenarios.

**Action to take:**
Create a lightweight regression matrix before approving the backend change. Include annual plans, monthly plans, upgrades, downgrades, cancellations, credits, grandfathered pricing, and invoice adjustments.

**Who needs to be involved:**
Tech lead, backend engineer, QA, PM.

**Classification:**
Important.

---

### Risk 3: Scope is still ambiguous

**Why it matters:**
The team has not decided whether mid-cycle downgrades, grandfathered pricing, and all invoice-adjustment scenarios are in scope for the first release. That ambiguity is likely driving PR growth and review difficulty.

**Action to take:**
Force a scope decision. Use three options:

1. Release happy-path upgrades only.
2. Support upgrades and selected downgrade scenarios.
3. Support the full set of billing edge cases.

Make the trade-off explicit: date, quality, support-ticket impact, and engineering risk.

**Who needs to be involved:**
PM, tech lead, Engineering Manager, Customer Success input.

**Classification:**
Urgent.

## 2. Technical risks

### Risk 1: The backend PR is too large to review safely

**Why it matters:**
A 1,200-line PR that changes calculation logic and API response shapes is difficult to review deeply. The risk is not only code correctness; it is that architectural and product decisions are being smuggled into implementation.

**Action to take:**
Do not treat this as a normal PR review problem. Schedule a short pairing or design-review session with the backend engineer. Aim to split the work by risk boundary, not necessarily by file.

Possible splits:

* regression test scaffolding
* internal calculation refactor without behaviour change
* new plan-change behaviour
* API response-shape changes
* feature-flagged integration

**Who needs to be involved:**
Tech lead, backend engineer, possibly one second reviewer.

**Classification:**
Urgent.

---

### Risk 2: Regression coverage is probably weaker than new-feature coverage

**Why it matters:**
The most damaging failure mode is not that the new plan-change flow fails obviously. It is that existing billing behaviours silently change.

**Action to take:**
Before merge, require explicit regression coverage for existing behaviours. The standard should not be “more tests were added”; it should be “the known billing behaviours we rely on are protected.”

**Who needs to be involved:**
Backend engineer, tech lead, QA.

**Classification:**
Important.

## 3. People follow-ups

### Follow-up 1: Backend engineer is becoming defensive

**Why it matters:**
The engineer may be interpreting review comments as criticism of their technical ability, rather than concern about reviewability and delivery risk. If that dynamic continues async, it will slow the team down and increase tension.

**Action to take:**
Move out of PR comments and into a direct conversation.

Suggested opening:

> “I think the concern here is not whether the refactor is technically valid. It’s that the change is now carrying several risks at once: billing behaviour, API shape, regression coverage, and release timing. I’d like us to split the risk so the team can review and release this safely.”

**Who needs to be involved:**
Tech lead and backend engineer.

**Classification:**
Urgent.

---

### Follow-up 2: Junior engineer may be stuck

**Why it matters:**
Silence in standups can mean good focus, but in this context it may mean the junior engineer is blocked or unsure how to raise uncertainty.

**Action to take:**
Check in privately. Keep it lightweight and specific.

Suggested message:

> “I noticed you’ve been quieter than usual on the UI validation work. Are you clear on the next step, or would a quick pairing session help unblock anything?”

**Who needs to be involved:**
Tech lead and junior engineer.

**Classification:**
Watchlist, but act soon.

---

### Follow-up 3: You are using late-night async review as a substitute for leadership

**Why it matters:**
Late-night review may feel productive, but it can also hide the need for earlier alignment, pairing, or scope decisions.

**Action to take:**
Choose one high-risk topic next week to resolve synchronously before it becomes another long PR thread.

**Who needs to be involved:**
Tech lead; possibly backend engineer or PM depending on topic.

**Classification:**
Important.

## 4. Stakeholder updates needed

### PM update

The PM needs a clearer distinction between UI progress and backend/release risk.

Message should include:

* UI work is progressing.
* Backend complexity is higher than expected.
* Scope decisions are still open.
* Release confidence depends on resolving those decisions.
* You recommend a short scope/risk review.

### Engineering Manager update

The earlier “we are okay” answer should be corrected.

Message should include:

* The team is making progress.
* You are concerned about the size/risk of the backend PR.
* You are planning to address it with the engineer.
* You may need support if scope/date trade-offs escalate.

### Customer Success update

Do not promise that all confusing invoice-adjustment cases will be fixed.

Message should include:

* The team is investigating the cases.
* Some may be addressed by the new flow.
* Some may depend on unresolved scope decisions.
* You will confirm once the regression/scope matrix is clear.

## 5. Decisions made

These decisions are useful and should be written down:

1. No full redesign of the billing settings page.
2. Plan-change flow will release behind a feature flag.
3. More automated tests will be added around new plan-change scenarios.

Suggested action:

Capture these in a lightweight decision log so they do not get reopened casually.

## 6. Decisions still open

These are the decisions most likely to affect delivery:

1. Are mid-cycle downgrades in scope?
2. Are all grandfathered pricing cases in scope?
3. Does the backend PR need to be split before merge?
4. What regression test matrix is required before release?
5. Are we moving the date, reducing scope, or accepting risk?

Suggested action:

Turn these into a 30-minute decision meeting, not a long Slack thread.

Recommended meeting title:

> Plan-change release scope and billing risk review

## 7. Delegation opportunities

### Delegate regression matrix drafting

You do not need to personally define every billing case.

Ask the backend engineer to draft the first version of the regression matrix, then review it with QA/PM.

### Delegate UI validation support

Pair the junior engineer with another engineer or designer for validation questions rather than becoming the only unblocker.

### Delegate customer-ticket mapping

Ask Customer Success or PM to map the three support tickets to specific billing scenarios. This will clarify whether they are in scope.

## 8. Manager 1:1 topics

Bring these to your Engineering Manager:

1. “I may have under-signalled the billing risk last time we spoke.”
2. “The main backend PR is now large enough that I’m concerned about review quality.”
3. “I’m going to push for a scope decision around mid-cycle downgrades and grandfathered pricing.”
4. “I’d like your advice on when to hold the line on PR splitting versus accepting short-term delivery pressure.”
5. “I’m noticing that I default to late-night review rather than earlier alignment. I want to improve that.”

## 9. Next week’s top three priorities

### Priority 1: Make release risk visible

Send a stakeholder update and schedule a scope/risk review.

### Priority 2: Reduce backend PR risk

Move the PR discussion out of async comments. Agree on either a split plan or a specific review strategy with regression coverage.

### Priority 3: Clarify scope

Resolve mid-cycle downgrades, grandfathered pricing, and invoice-adjustment expectations before more implementation work accumulates.

## One uncomfortable thing you may be avoiding

You may be avoiding the fact that “probably on track” was not accurate enough.

That does not mean you failed. It means the situation changed and your communication needs to catch up. A tech lead’s job is not to maintain confidence at all costs. It is to make reality visible early enough that the team still has options.

## One thing you should not overreact to

Do not overreact to the backend engineer’s defensiveness by turning this into a performance issue.

Right now, treat it as a risk-clarity and collaboration problem. If the pattern repeats after a direct conversation and clearer expectations, then reassess.

## Draft stakeholder update

> Quick update on the plan-change work.
>
> The UI work is progressing, and we are still aiming to release incrementally behind a feature flag. However, the backend billing work has exposed more complexity than we initially expected, especially around mid-cycle changes, grandfathered pricing, credits, and invoice adjustments.
>
> I do not think this is blocked, but I do think we need a short scope/risk review before we can give a confident release call.
>
> The main decisions to close are:
>
> 1. whether mid-cycle downgrades are included in the first release,
> 2. how much grandfathered pricing support is required immediately,
> 3. what regression coverage we need before release, and
> 4. whether we reduce scope or adjust the target date.
>
> My recommendation is that we spend 30 minutes aligning on those decisions before the backend PR gets any larger. That should give us a safer path to release and avoid discovering billing edge cases too late in QA.
