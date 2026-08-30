# Understanding How Adjustable Power Supply Works Using LM317 IC


This project is the second stage of my power-supply project series. The first stage was -

[5V Regulated Power Supply using LM7805]()


After building a fixed 5V regulated supply, I wanted to understand how the output voltage could be made adjustable instead of being fixed to a single value.

For this, I used the **LM317A Adjustable Linear Voltage Regulator** and built the circuit first in **LTspice** and then **physically on a breadboard**.

## What I Wanted to Learn

The main goal was not simply to get a particular output voltage.

I wanted to understand -

- How LM317A controls its output voltage
- How the resistor network connected to OUT and ADJ affects the output
- How a preset can be used to adjust the output
- How rectification and filtering work before the regulator
- How closely a real circuit behaves compared with simulation
- What changes when ideal simulation components are replaced by real components.


## What all I've used

The circuit consists of -

- Step-down transformer
- Full-wave bridge rectifier 
- 1000 µF filter capacitor
- 0.33 µF input capacitor
- LM317A adjustable regulator
- R1 = 220Ω 
- R2 = 22Ω 
- R3 = 10KΩ (preset for adjustment)
- 0.33 µF output capacitor


## How LM317A works?

LM317A maintains approximately 1.25 V between its OUT and ADJ terminals.

The output voltage can be calculated using -

$$
V_{OUT}=1.25\left(1+\frac{R_2}{R_1}\right)+I_{ADJ}R_2
$$

where:
- $R_1$ = 220 Ω
- $R_2$ = variable resistance
- $I_{ADJ}$ = adjustment pin current



Therefore, changing the resistance in the adjustment network changes the regulated output voltage.

This is the main difference from the previous fixed 5V regulator project.


## Simulation vs Practical Results

| Parameter | Simulation | Practical |
|:---:|:---:|:---:|
| Regulator | LT317A | LM317A |
| R1 | 220 Ω | 218 Ω |
| Fixed resistor | 22 Ω | 23.4 Ω |
| Adjustment | 720 Ω preset | ≈ 720 Ω preset |
| Output | Stable/adjustable | ≈ 5.02 V |
| Main issue | All Ok | Getting 720Ω through 10K Preset |
| Additional | None | Heat Sink to secure the IC |

## Learning Outcome

The first power supply taught me how AC is converted into regulated DC.

This stage added another important concept -

The regulator itself can be controlled through an external feedback network.
I also learned that selecting a resistor value theoretically is only one part of building a circuit. In hardware, the actual condition of the component matters just as much.

The faulty preset was frustrating, but it actually became one of the most memorable parts of this experiment because I had to understand why the circuit was behaving differently instead of simply assuming that the simulation was wrong.

Most importantly, I became more comfortable with the idea of moving from -

***Theory → Simulation → Hardware → Unexpected Result → Troubleshooting → Understanding***

rather than expecting the hardware to behave exactly like the simulation.
