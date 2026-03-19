```markdown
# Trust Conflict Resolver

## Overview
The Trust Conflict Resolver is a smart contract designed to deterministically resolve conflicting trust signals. It processes positive and negative inputs, applies integrity weighting, and produces a consistent trust score while tracking conflict frequency over time.

This contract is useful in systems where multiple trust signals may conflict and a fair, transparent resolution mechanism is required.

---

## Features
- Deterministic trust resolution logic
- Conflict detection and penalty mechanism
- Integrity-based score adjustment
- Time-based resolution control
- Per-user trust and conflict tracking
- Read-only access to trust data

---

## Error Codes
| Code | Description |
|------|-------------|
| u600 | Invalid signals provided |
| u601 | Resolution attempted too soon |

---

## Configuration Constants
- **MIN_RESOLUTION_GAP**  
  Minimum block interval required between consecutive resolutions for a user

- **CONFLICT_THRESHOLD**  
  Threshold used to determine if signals are in conflict

- **CONFLICT_PENALTY**  
  Amount deducted from trust score when a conflict is detected

- **RESOLUTION_REWARD**  
  Bonus added when signals align with high integrity

---

## Data Storage

### `resolved-trust`
Stores the current resolved trust score for each user.

### `last-resolution-block`
Tracks the last block height when a user’s trust was updated.

### `conflict-count`
Counts how many times a user has triggered a conflict condition.

---

## Read-Only Functions

### `get-resolved-trust`
Returns the current trust score of a user.

### `get-conflict-count`
Returns the number of conflicts recorded for a user.

---

## Core Function

### `resolve-trust`

#### Parameters
- **positive-signal**: Positive trust input value  
- **negative-signal**: Negative trust input value  
- **integrity-flag**:
  - `0` = low integrity  
  - `1` = neutral  
  - `2` = high integrity  

#### Behavior
1. Ensures sufficient block gap since last resolution  
2. Validates integrity input  
3. Compares positive and negative signals  
4. Detects conflicts based on threshold  
5. Applies:
   - Penalty if conflict detected  
   - Reward if signals align and integrity is high  
6. Updates user trust score and metadata  

---

## Resolution Logic

### Conflict Case
- Triggered when signal difference exceeds threshold  
- Increments conflict counter  
- Applies penalty to trust score  

### Normal Resolution
- Computes difference between positive and negative signals  
- Adds reward if integrity is high  
- Updates trust score accordingly  

---

## Security Considerations
- Prevents rapid repeated updates using block-based delay  
- Validates integrity flag inputs  
- Ensures deterministic and transparent calculations  

---

## Use Cases
- Reputation systems  
- Decentralized identity scoring  
- Fraud and trust analysis platforms  
- Governance and voting weight systems  

---

## Future Improvements
- Event emission for tracking resolutions  
- Adjustable configuration via admin controls  
- Integration with external trust or oracle systems  
- Historical trust tracking for analytics  

---

## License
This project is open-source and available for modification and distribution.
```
