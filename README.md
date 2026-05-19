# Fault-Tolerant Digital Traffic Light Control System

A gate-level, hardware-controlled digital traffic light system designed without using any microcontrollers. This project features dynamic cycle acceleration via asynchronous pedestrian requests and hardware-enforced fail-safe mechanisms such as interlocking and conflict resolution.

## 📸 Project Visuals
| Proteus Schematic | Physical Implementation |
|---|---|
| ![Schematic](Images/schematic.png) | ![Physical Circuit](Images/physical_circuit.jpg) |

## 🚀 Key Features & Hardware Architecture
* **No Microcontrollers:** Fully implemented at the gate level using 74-series logic components and basic semiconductors.
* **Synchronous State Machine:** Built using an NE555 Timer in astable mode, dual 74HC74 D-Type Flip-Flops, and a 74HC86 XOR gate to generate a 2-bit synchronous counter.
* **Dynamic Timing Control:** Integrated BC237 NPN transistors and potentiometers to dynamically scale the operating frequency ($0.133\text{ Hz} - 0.699\text{ Hz}$) by altering the RC time constant.
* **Asynchronous Pedestrian Intervention:** A debounced hardware switch prompts an accelerated cycle towards the pedestrian phase safely through combinational state progression without compromising cross-traffic safety.

## 🛡️ Hardware-Enforced Fail-Safe Mechanisms
Unlike software-defined solutions, safety metrics in this system are **hardware-impossible** to bypass:
1. **Dual Green Protection (Conflict Resolution):** A 74HC00 NAND gate instantly detects if both main and side roads are assigned a GREEN status simultaneously. It immediately triggers an asynchronous reset to a safe initial state (State 0: Main Green, Side Red).
2. **Dead State Protection (Dark Intersection):** A supervisory network utilizing 74HC32 OR gates continuously monitors all lighting channels. If an illegal state occurs where all lights are turned OFF (all outputs LOW) during power-up or operation, the system automatically auto-resets back into the safe initial cycle.

## 📋 System State Sequence
| State (Phase) | Main Road Lights | Side Road Lights | Pedestrian Lights | Description |
|---|---|---|---|---|
| **State 0** | GREEN | RED | RED | Traffic flows on the main road. |
| **State 1** | YELLOW | RED | RED | Main road prepares to stop. |
| **State 2** | RED | GREEN | RED | Right of way is given to the side road. |
| **State 3** | RED + YELLOW | RED | GREEN | Safe crossing duration for pedestrians. |

## 📦 Bill of Materials (BOM)
* **ICs (Logic & Timing):** NE555, 74HC74, 74HC86, 2x 74HC32, 2x 74HC08, 74HC00, 74HC04
* **Semiconductors:** 2x BC237 NPN Transistors, 4x 1N4148 Fast Switching Diodes
* **Display Elements:** 3x Green LEDs, 3x Red LEDs, 1x Yellow LED
* **Passives:** 100kΩ / 50kΩ Potentiometers, 47kΩ, 6x 10kΩ, 7x 330Ω Resistors, 44µF Electrolytic & 3x 100nF Ceramic Capacitors

## 📂 Repository Contents
* `/Simulation`: Contains the Proteus Design Suite schematic file.
* `/Documents`: Contains the comprehensive academic project report.
