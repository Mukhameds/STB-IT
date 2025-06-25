
---

# VII. Code Examples and Templates

## 7.1 Simple Block Reacting to a Numeric Signal

```go
Block{
  BlockID: "B_compareValue",
  PhaseSet: ["Φ_numeric"],
  FormShape: "{sensor, value>100}",
  Threshold: 0.8,
  ReactionFn: func(signal Signal) []Signal {
    if signal.Payload > 100 {
      return []Signal{{Type: "alert", Payload: "value too high", Phase: "Φ_warning"}}
    }
    return nil
  },
  State: {}
}
````

## 7.2 Cascade Activation Scenario

```go
SignalQueue ← [Signal{Type: "temp", Payload: "T=90°C", Phase: "Φ_heat"}]

Block B1 (heatSensor): PhaseSet = [Φ_heat] → logs alert  
Block B2 (memory): PhaseSet = [Φ_heat] → stores the value  
Block B3 (fanActivator): PhaseSet = [Φ_alert] → triggers cooling
```

## 7.3 Phantom Definition Example

```go
Fantom{
  ID: "F_overheatRisk",
  TriggerPhases: ["Φ_heat", "Φ_warning"],
  MassThreshold: 2.0,
  Reaction: func() Signal {
    return Signal{Type: "predict", Payload: "risk of failure", Phase: "Φ_predict"}
  },
  Lifetime: 5000ms
}
```

## 7.4 Main Engine Loop Template

```go
func RunEngine(queue []Signal, blocks []Block) {
  for {
    sig := Dequeue(queue)
    for _, b := range blocks {
      if Match(sig, b) {
        reactions := b.React(sig)
        Enqueue(queue, reactions...)
      }
    }
    UpdateFantomField(sig)
    DecayBlocks()
  }
}
```

```

---

