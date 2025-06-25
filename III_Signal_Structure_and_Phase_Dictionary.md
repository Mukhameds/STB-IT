# III. Signal Structure and Phase Dictionary

## 3.1 General Signal Model

A signal is the fundamental unit of information transmission within the system.  
It is capable of exciting blocks depending on the match between its form, phase, and type.  
Each signal has a strictly defined structure.

### Signal Fields:

* `Type` — signal type (e.g., text, audio, numeric, sensory, logical)  
* `Payload` — content (e.g., "temperature = 100°C" or "code = 0110")  
* `PhaseKey` — phase identifier corresponding to a specific letter, sound, image, or value  
* `Origin` — source of the signal (e.g., external sensor or another block)  
* `TimeStamp` — time of signal generation (optional)

## 3.2 Rejection of Float-Phase: Phase Dictionary

STB does not use float64 values for phase.  
Instead, it utilizes a signal-phase dictionary — analogous to Braille or Morse code.

### Example of Phase Dictionary:

| PhaseKey | Value   | Description               |
|----------|---------|---------------------------|
| Φ₀       | A       | Start, activation         |
| Φ₁       | B       | Intermediate phase        |
| Φ₂       | C       | Termination, inhibition   |
| Φ₃       | 0101    | Binary signal             |
| Φ₄       | T_HIGH  | High temperature          |
| Φ₅       | “if”    | Logical construct         |

The phase dictionary is extensible and context-sensitive.

## 3.3 Phase Matching Mechanism

Each block defines a list of PhaseKeys it is tuned to.  
Matching can be strict (`==`) or based on masks/group patterns.

### Types of Matching:

* Exact PhaseKey match  
* Belonging to a phase group (e.g., "all logical operators")  
* Pattern matching or regular expressions

## 3.4 Potential of Phase-Based Addressing

The phase component of a signal can serve as:

* A routing mechanism (only blocks matching Φ₄ are activated)  
* A key for logical comparison (comparing signal phases)  
* A classifier of event categories (e.g., all signals with Φ_temperature)
