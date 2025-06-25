
---

# IV. Block Model and Its States

## 4.1 Block as a Unit of Reaction

A block is an autonomous element of the computational architecture.  
It can receive signals, compare them with its own phase and form configuration, and generate a response.  
Blocks are not active by default — they are only excited when an incoming signal matches their phase configuration.

## 4.2 Block Structure

Each block is described by the following parameters:

* `BlockID` — unique identifier  
* `PhaseSet` — a set of phase keys to which the block is sensitive  
* `FormShape` — internal form (feature structure)  
* `Threshold θ` — minimum form-factor value required for activation  
* `ReactionFn` — reaction function (can emit new signals or modify the incoming one)  
* `State` — internal state (memory, counter, accumulator, etc.)

## 4.3 Types of Block States

A block’s state represents its internal memory or configuration, affecting future reactions. Possible states include:

* **Constant**: configuration is static and does not change  
* **Accumulative**: the block accumulates values linked to incoming signals (e.g., frequency of activation)  
* **Reactive**: the state is updated in response to specific phases  
* **Temporal**: the state is active only within a defined time window

## 4.4 Block Activation Logic

A block is activated only when all of the following conditions are satisfied:

* Signal phase ∈ block’s `PhaseSet`  
* Form match ≥ `θ` (sensitivity threshold)  
* (Optional) The block’s internal state permits reaction (e.g., cooldown has expired)

## 4.5 Delay and Inhibition Mechanisms

A block may include internal inhibitory parameters:

* `Delay` — delay before reaction is executed after excitation  
* `InhibitWindow` — time window during which the block cannot be re-excited  
* `Decay` — spontaneous degradation of the internal accumulated state

These parameters model resilience, inertia, and habituation — essential properties of reactive systems.

## 4.6 Example Block Definition

```json
{
  "BlockID": "B_logger",
  "PhaseSet": ["Φ₄", "Φ₃"],
  "FormShape": "{sensor,temperature}",
  "Threshold": 0.7,
  "ReactionFn": "log(payload)",
  "State": {
    "entries": [],
    "lastTrigger": "2025-06-22T18:00:00Z"
  }
}
````


---


