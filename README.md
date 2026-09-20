# pico_bayblade_speedomeeter
# High-Precision Tachometer (RP2040 PIO & Pico SDK)

A bare-metal firmware project designed to calculate high-velocity rotational metrics (such as toy blade/motor spin velocities) using sub-microsecond hardware capture loops. 

Instead of relying on CPU-bound GPIO interrupts which introduce latency jitter, this system offloads signal edge timing directly onto an RP2040 **Programmable I/O (PIO) state machine**.

## 🛠️ System Architecture & Specs
*   **Core Controller:** Raspberry Pi Pico (RP2040, Dual ARM Cortex-M0+ @ 133MHz)
*   **Firmware Layer:** Bare-metal **Pico SDK (C/C++)**
*   **Hardware Interface:** Liquid Crystal Display (LCD) framework for real-time telemetry output
*   **Signal Input:** Custom PIO hardware state machine monitoring pulse feedback lines

## ⚡ Engineering & Firmware Implementation Highlights

### 1. Jitter-Free Edge Capture via PIO State Machines (`pulse_timer.pio`)
At extreme rotational speeds, standard microcontroller interrupts degrade accuracy due to execution overhead and latency. This project implements a custom PIO assembly script that:
*   Safely executes independently of the main CPU cores.
*   Samples the sensor input line natively on hardware clock cycles.
*   Pushes deterministic counter arrays back into the RX FIFO buffer for latency-free parsing.

### 2. Non-Blocking Display Driver Interfacing
The display logic is decoupled from signal sampling loops to prevent display driver delays (`lcd/` subroutines) from interrupting physical sensor tracking.

### 3. Native CMake Build Environment
Configured for robust toolchain deployments without absolute path dependencies, leveraging modular layout separations.

```bash
cmake -S . -B build-make -DPICO_NO_PICOTOOL=ON; cmake --build build-make --target pico_bayblade_speedomeeter -j 4; & 'C:\Program Files\Raspberry Pi\Pico SDK v1.5.1\pico-sdk-tools\elf2uf2.exe' build-make\pico_bayblade_speedomeeter.elf build-make\pico_bayblade_speedomeeter.uf2;
```
