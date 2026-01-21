# NE555 Analog PWM Motor Driver

A standalone, analog pulse-width modulation (PWM) speed controller for DC motors, utilizing the 555 timer architecture for robust, code-free operation.

![PCB View](PCB1.png)

## Functions
*   **Speed Control:** Adjusts motor speed via a potentiometer (VR1) altering the PWM duty cycle.
*   **Voltage Regulation:** Onboard 7812 regulator ensures stable gate drive voltage regardless of input fluctuations.
*   **Load Switching:** Low-side driving of motors, fans, or LEDs.

## Technical Highlights (Design Evaluation)

This circuit improves upon standard 555 PWM schematics with industrial protection features:

*   **Steering Diode Topology:** Unlike basic 555 circuits limited to >50% duty cycle, diodes **D3 and D4** separate the charge and discharge paths of capacitor C6. This allows the potentiometer (VR1) to adjust the duty cycle across the full **0% to ~100% range**.
*   **Gate Drive Stability:** The **LM7812** regulator isolates the NE555 from the noisy main power rail. This ensures the MOSFET gate is always driven with a clean 12V signal, preventing localized heating due to under-driving (incomplete saturation) when the main battery voltage drops.
*   **Inductive Protection:**
    *   **Schottky Flyback (SR560):** A fast-recovery Schottky diode is placed across the output to clamp high-voltage inductive spikes from the motor, protecting the MOSFET from breakdown.
    *   **Reverse Polarity (1N5408):** Protects the entire circuit from accidental reverse battery connection.

## Specifications
*   **Input Voltage:** 14V - 35V DC (Limited by 7812/Capacitors).
*   **Output Current:** 5A (Limited by Fuse F1).
*   **PWM Frequency:** Fixed (Determined by C6/VR1).
*   **Power Element:** IRFZ44N (N-Channel MOSFET).

## Pinout
| Pin | Description |
| :--- | :--- |
| **P1 (VIN)** | Power Input (+/-) |
| **P2 (MOT)** | Motor Output (+/-) |
