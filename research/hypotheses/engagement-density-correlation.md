---
template: hypothesis
template_version: 1.0.0
collection: hypotheses
slug: engagement-density-correlation
title: Engagement Density Correlates With Coordination Quality (Testable)
authors:
  - jane-doe
insights:
  - asynchronous-coordination-density
status: active
stage: draft
validation-status: pending
test-design: Cohort study across 10+ asynchronous platforms over 90 days; measure engagement-density distribution (top-quartile concentration ratio) and coordination-quality proxy (task-completion rate / decision-quality survey); correlate.
tags:
  - coordination
related_hypotheses: []
example: true
created: 2026-05-21
updated: 2026-05-21T17:53
---

# Engagement Density Correlates With Coordination Quality (Testable)

## Hypothesis

If we measure engagement density (top-quartile time-concentration of participation) on an asynchronous-coordination platform, then coordination quality (task-completion / decision-quality / participant-satisfaction proxies) will correlate positively with density — and the correlation will be stronger than with total engagement volume.

## Underlying insight(s)

Builds directly on [[research/insights/asynchronous-coordination-density|Engagement Density Predicts Coordination Quality in Asynchronous Networks]], which synthesised two observations and one library paper into the density-over-volume claim. This hypothesis makes the claim testable.

## Why this matters

If validated, this hypothesis would imply that engagement metrics across asynchronous platforms (open-source projects, collaborative document tools, online research collectives) are tracking the wrong primary indicator. The implications for platform design and operator KPIs would be substantial.

If invalidated, the underlying insight is weaker than the framing suggests — likely needs further specification (which density measure? which coordination-quality proxy?).

## Test design

90-day cohort study across 10+ asynchronous-coordination platforms (open-source projects, async-collab tools). Measure:

- **Engagement density:** top-quartile time-concentration ratio (what fraction of total engagement falls in the top-quartile of time-blocks).
- **Coordination quality:** task-completion rate per cohort + a participant-satisfaction survey.
- **Total engagement volume:** as a control variable.

Test whether density beats volume as a predictor in a multi-variate model.

## Validation history

- 2026-05-21: created as part of example dummy content. `validation-status: pending`. Not actually being tested.

## Notes

Placeholder hypothesis. Not actually being investigated by Co-Goods. Used to exercise the hypothesis template + the `validation-status` rendering.
