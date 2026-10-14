# Line-Following Robot

A line-following robot (LFR) built for **ENMT221 Mechatronics Design 1** at the University of Canterbury (Semester 2, 2026). The course runs a robot design project where every student designs a section of a line-follower individually, the team combines the best concepts into one PCB and mechanical design, and then the robots race against each other.

**Our team placed second.**

## What I did

My individual component was the **microcontroller section of the LFR PCB**:

- **ATmega4808-A** (AVR) with the datasheet-mandated support circuitry — voltage regulator, decoupling, clock
- External connectors for the sensor array, motor drivers, battery, and programming headers, so the board could integrate cleanly into the team PCB
- Full PCB layout in KiCad with Gerber/drill files for fabrication

From there the team merged the individual sections into one board, built the robot, programmed it (line sensing → PWM drive commands per the classic two-sensor control loop), tested and refined it, then raced. The PCB in this folder is my submission.

## Files

- [`LFR.kicad_pcb`](LFR.kicad_pcb) — the microcontroller PCB, laid out in KiCad 10 (2-layer, 1.6 mm)
