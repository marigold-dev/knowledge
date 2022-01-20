---
description: Those properties are defined on a consensus level.
---

# Liveness & Safety properties

## &#x20;Definitions

{% hint style="info" %}
**Decision**&#x20;

The action by which a process makes a value relevant/true.
{% endhint %}

{% hint style="info" %}
**Action**

A consensus defines its own set of actions available to its processes. For instance endorsement, commit, message, votes, etc
{% endhint %}

## Specifications

### Tolerance spec

Ability to carry on  standard operations in the presence of byzantine nodes, up to a specific threshold of byzantine nodes.

### Non-repudiation spec (safety)

Actions are associated with a single individual (account or node or valid key) and it is not possible to successfully dispute authorship of a statement.

### Progress spec

There is no sequence of actions such that no new action is possible.

### Agreement spec (safety)

All processes that decide (correct or not) must decide the same value.

**or** No two processes decide differently

### Integrity spec (safety)

At most one decision per process

### Validity spec (safety)

The value decided by a process must have been proposed

### Termination spec (liveness)

All correct processes must eventually decide a value

