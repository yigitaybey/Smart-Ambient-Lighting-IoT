<div align="center">
  <h1>💡 Smart Ambient Lighting (IoT)</h1>
  <p><em>R&D, Engineering Diary, and System Architecture</em></p>
</div>

<br>

##  Project Status: Phase 1 (R&D & Component Selection)
This repository serves as the engineering logbook for my custom IoT Smart Lighting System. Before writing a single line of code or designing the PCB, I conducted a deep-dive feasibility study and Root Cause Analysis (RCA) to select the right components for safely switching a high-current (24V/5A) load using a 3.3V microcontroller.

##  Core Architecture & Hardware Choices

Instead of relying on basic tutorials, I analyzed datasheets to build a robust, scalable, and safe architecture:

### 1. The Brain: ESP32-S3 (Dual-Core)
*   **Why ESP32-S3?** A standard Arduino cannot handle non-blocking Wi-Fi communication and high-frequency hardware PWM simultaneously. The ESP32-S3’s dual-core (LX7) architecture allows me to isolate the MQTT network loop on Core 0 while running the PID brightness algorithm on Core 1 without stuttering.
*   **Memory:** 8MB PSRAM for handling potential embedded web servers in fallback mode.

### 2. The Sensor: VEML7700 (I2C)
*   **Why not LDR?** Analog photoresistors are prone to noise and temperature drift.
*   **Why not BH1750?** While standard, the BH1750 maxes out quickly. The VEML7700 can read up to **140,000 Lux**, meaning it won't blind or clip even in direct sunlight, providing a true digital metric for the PID controller.

### 3. The Power & Switching: IRLZ44N (N-Channel MOSFET)
*   **The 3.3V to 24V Trap:** The ESP32 outputs only 3.3V logic. Standard MOSFETs (like IRF540N) require 10V at the gate to fully open, meaning they would act as resistors and catch fire under a 5A load if driven by 3.3V. 
*   **The Solution:** The IRLZ44N is a **Logic-Level** MOSFET with an exceptionally low $R_{DS(on)}$ (0.035 $\Omega$), ensuring it reaches full saturation near 3.3V/4V, keeping thermal dissipation to an absolute minimum while switching the 24V LED strip via PWM.

### 4. Power Supply & Safety
*   **SMPS:** Mervesan 24V 10A Metal Case SMPS (providing 100% headroom for a 5A load).
*   **Step-Down:** LM2596S fixed to 5V to safely power the ESP32 logic rail from the 24V source.
*   **Fusing:** A 7.5A Blade Fuse placed immediately at the 24V output to protect against catastrophic short circuits.

##  Bill of Materials (BOM) & Specs

| Component | Role | Specification |
| :--- | :--- | :--- |
| **ESP32-S3** | Microcontroller / Wi-Fi | Dual Core LX7, 8MB PSRAM |
| **IRLZ44N** | Low-Side Switch | Logic-Level, TO-220, $R_{DS(on)}$: 0.035 $\Omega$ |
| **VEML7700** | Ambient Light Sensor | I2C Protocol, up to 140K Lux |
| **LED Strip** | Load | 24V, 5A (approx 120W total) |
| **Mervesan SMPS** | Power Supply | 24V, 10A (SCP, OTP, OVP Protected) |
| **LM2596S** | Buck Converter | 24V to 5V Step-down, 3A Max |
| **Blade Fuse** | Safety | 7.5A Automotive Type |

##  Datasheets & References
*(All component datasheets will be archived in the `/datasheets` folder of this repository for future PCB layout references in KiCad).*

## 🔮 Next Steps (Roadmap)
1.  **Hardware Validation:** Breadboard testing the PWM logic and IRLZ44N thermal performance once components arrive.
2.  **Firmware Development:** Writing the FreeRTOS C++ code and I2C sensor integration.
3.  **PCB Design:** Designing the custom board in KiCad.
4.  **Enclosure:** 3D designing a passive-cooling case in Fusion 360 (using ABS/PETG, avoiding PLA for thermal reasons).
