---
title: "What Zero False Alarms Taught Me About Physics-Informed ML"
description: "Eighteen months of production at Peel Region, 13 storms, and one overflow caught 7 hours early."
date: 2025-04-15
icon: "∿"
---

In April 2025, a combined sewer in Peel Region, Ontario overflowed. We caught it 7 hours and 40 minutes before it happened.

That number — 7h40m — is the kind of thing you spend years working toward and then, when it finally appears in a log, you stare at it for longer than you should.

## The Problem With Pure ML on Physical Systems

Water utility telemetry is hostile data. Sensors fail mid-storm. There are calibration drifts that accumulate silently over weeks. Flow meters get partially blocked and start reading at 60% accuracy. And the thing you're trying to predict — a combined sewer overflow — is rare enough that your positive class is desperately underrepresented in any training set.

Standard time-series classification handles none of this gracefully.

What we built instead was [Lark](https://github.com/carldata), a Go library that bakes the underlying hydraulic physics directly into its prediction architecture. Rather than letting a gradient-boosted tree discover that *water flows downhill* from 40 million data points, we encode it explicitly: antecedent moisture conditions, decay functions for dry-weather baseflow, gate positions, upstream contributing area.

The model learns *residuals from physics*, not raw patterns.

## The Antecedent Moisture Problem

The single most important predictor of overflow isn't current rainfall — it's what happened before it rained.

A 20mm storm on saturated ground behaves nothing like a 20mm storm after two weeks of dry weather. The soil can't absorb the initial pulse; the combined sewer surcharges faster; the overflow window opens earlier.

We encode this as an exponential decay over a 2016-step window (roughly a week of 5-minute readings) using the drainage district's own `dwf.API()` call with a decay coefficient of 0.85. This single formula — borrowed directly from the hydraulic engineering literature — does more predictive work than any learned feature we've experimented with.

```go
// Antecedent Moisture Condition via exponential decay
func ComputeAMC(flow []float64, decay float64) float64 {
    var amc float64
    for i := len(flow) - 1; i >= 0; i-- {
        amc = amc*decay + flow[i]
    }
    return amc
}
```

## Thirteen Storms, Zero False Alarms

This is the stat that matters most operationally. False alarms are expensive — they require dispatch, they erode trust with the utility client, and they're how you lose a contract.

Across 13 validated storm events at Cavendish Creek (site 24111) and Clarkson GO Weir (site 25524), Lark produced zero false positive alerts. The April 3rd real overflow was the first true positive in that validation window.

Seven hours and forty minutes of lead time means an operations team can mobilize, pre-position equipment, notify downstream stakeholders, and in some cases, route flow away from the overflow structure entirely.

That's not just a metric. That's avoided sewage in a creek.

## What This Means for MLOps in the Infrastructure Space

The lesson I keep returning to is about the relationship between domain knowledge and model complexity. In domains with well-understood physics — hydrology, power systems, structural monitoring — the most leverage comes not from larger models or more data, but from *encoding what you already know*.

A random forest that has to learn from scratch that wet ground absorbs rain more slowly needs millions of examples to get there. A model that starts from the physics gets there with 400 storm events from a single catchment.

This is what I mean when I say physics-informed ML isn't a technique. It's a philosophy about where you put your engineering effort.

---

*Lark is in production for Peel Region, Ontario. If you work in water utilities or infrastructure ML, I'd genuinely like to hear from you.*
