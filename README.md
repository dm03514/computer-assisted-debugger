# computer-assisted-debugging
Heuristic based debug engine.  A happy medium between structured anomaly detection and unstructured/playbook based debugging


## Commands

### Generating Heuristic/Playbook Sequence Graph

```
$ python bin/generate_graph.py examples.provider_strategy:build_for_display
```

### Generating Heuristic/Playbook Table States

```
$ python bin/generate_graph.py examples.provider_strategy:build_for_display --type=md_table
```

# Playbook Examples

## Deploy

### Playbook
![cad heuristics deploy](https://user-images.githubusercontent.com/321963/54880914-bab73680-4e20-11e9-84a8-0ab20dbd8783.png)
### State Transitions
| Node Name | Evaluator | Query Source | Yes Threshold |
| ------- | --------- | -------- | ----------- |
|LastDeploy < X hours|SingleValueThresholdEvaluator|StubQuery|LastDeploy < X hours|

---

## Provider Outage
### Playbook
![examples provider_strategy](https://user-images.githubusercontent.com/321963/54880855-0d442300-4e20-11e9-95a5-b17a477d42a5.png)

### State Transitions
| Node Name | Evaluator | Query Source | Yes Threshold |
| ------- | --------- | -------- | ----------- |
|Strategy Error Rate > 50%|OneOfManyValuesThresholdEvaluator|StubQuery|Strategy Error Rate > 50%|
|Region Strategy Error Rate > 50%|ManyValuesThresholdEvaluator|StubQuery|Region Strategy Error Rate > 50%|
|Many Customers Error Rate > 50%|ManyValuesThresholdEvaluator|StubQuery|Many Customers Error Rate > 50%|
