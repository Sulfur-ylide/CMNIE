# CMNIE: An Information Extraction Benchmark for Chinese Military News

CMNIE is a Chinese military-news benchmark for joint information extraction. It is built from publicly accessible Chinese military-news texts and provides aligned annotations for events, event arguments, named entities, and entity relations.

The dataset is available on ModelScope: `https://www.modelscope.cn/datasets/mzzzhu/CMNIE`.

## Dataset Overview

CMNIE contains 13,000 news instances. It covers four information-extraction tasks:

- **Event extraction:** event triggers, event types, argument spans, and argument roles.
- **Named entity recognition:** entity spans and entity types.
- **Relation extraction:** typed relations between entity mentions.
- **Joint information extraction:** the four annotation layers are available in the same instance.

| Annotation item | Coverage |
|---|---:|
| Instances | 13,000 |
| Event-bearing instances | 6,997 |
| Event triggers | 6,997 |
| Event arguments | 23,087 |
| Entity mentions | 97,508 |
| Relation mentions | 40,252 |
| Event types | 7 |
| Argument roles | 10 |
| Entity types | 7 |
| Relation types | 8 |

### Event types

`Experiment`, `Manoeuvre`, `Deploy`, `Accident`, `Indemnity`, `Support`, and `Exhibit`.

### Argument roles

`Subject`, `Equipment`, `Date`, `Location`, `Content`, `Area`, `Militaryforce`, `Result`, `Object`, and `Materials`.

### Entity types

`PER`, `TIME`, `GPE`, `EQU`, `ORG`, `LOC`, and `FAC`.

### Relation types

`Belong`, `Carry`, `Subordinate`, `Equal`, `Hostility`, `Develop`, `Cooperation`, and `Fellow`.

## Data Splits

| Split | File | Instances | Event-bearing instances |
|---|---|---:|---:|
| Train | `train_1205.json` | 8,000 | 4,368 |
| Development | `dev_1205.json` | 2,000 | 1,080 |
| Test | `test_1205.json` | 3,000 | 1,549 |

All files are JSON Lines files: each physical line contains one JSON object. The `.json` filename extension is retained for compatibility with the original release.

## Data Format

```json
{
  "id": "unique-instance-id",
  "sentence": "Original Chinese news text.",
  "tokens": ["Original", "Chinese", "news", "text", "."],
  "tokens_count": 5,
  "event_mention": {
    "trigger": {"text": "...", "offset": [start, end]},
    "event_type": "Manoeuvre",
    "arguments": [
      {"role": "Subject", "text": "...", "offset": [start, end]}
    ]
  },
  "entity_mention": [
    {"entity_type": "ORG", "text": "...", "offset": [start, end]}
  ],
  "relation_mention": [
    {
      "head": {"entity_type": "ORG", "offset": [start, end]},
      "tail": {"entity_type": "GPE", "offset": [start, end]},
      "relation_type": "Subordinate"
    }
  ]
}
```

Offsets are token-level half-open intervals, `[start, end)`, rather than character offsets. For an annotated span, `"".join(tokens[start:end])` equals the corresponding `text`. An empty `event_mention` object (`{}`) indicates an instance without an event annotation.

## Evaluation Code

Evaluation code: **coming soon**.
