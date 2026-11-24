<img width="705" height="444" alt="Reworking Skripsi PCB1" src="https://github.com/user-attachments/assets/17c1e8c2-9ff6-400f-b8a0-a99cd1df30a5" />


# Transmiter-Subsystem-Visible-Light-Communication

Hardware design repository (KiCad schematic and PCB layout) for a high-speed **Visible Light Communication (VLC) Transmitter Subsystem**. The circuit integrates a DC bias-tee conditioning network, a high-speed non-inverting amplifier stage based on dual **LM7171BIN** op-amps, and an **IRF510PBF** N-channel power MOSFET driver stage to modulate an LED light source with high-frequency data signals.

---

#### Circuit Architecture & Functional Blocks
<img width="923" height="451" alt="Reworkin skripsi Schematic1" src="https://github.com/user-attachments/assets/45f2595c-73aa-46d4-8833-876de12cb727" />




1. **Power Supply Decoupling & DC Bias Reference (`C3`, `JP1`, `RV1`, `C2`, `U1`)**
   - **`C3` (2.2 µF):** Bulk decoupling capacitor connected between `VCC` and `GNDREF` to filter low-frequency supply ripple.
   - **`RV1` (Trim Potentiometer) & `C2` (100 nF):** Forms an adjustable voltage divider (enabled via solder jumper `JP1`) with high-frequency noise filtering (`C2`) to set the precise DC offset voltage required to keep the transmitter LED operating in its linear region.
   - **`U1` (LM7171BIN — Voltage Follower / Buffer):** Configured as a unity-gain buffer (`OUT` tied directly to `-IN`) to provide a low-impedance, stable DC bias reference without loading the potentiometer network.

2. **Passive Bias-Tee & Signal Combining Network (`J1`, `R2`, `R3`, `C4`)**
   - **`J1` (Coaxial / RF Input Connector `10-473-A3`):** Accepts the incoming high-speed modulating data signal.
   - **`R2` (510 Ω) & `R3` (1 kΩ):** Resistive summing network that combines the buffered DC bias voltage from `U1` with the AC data signal from `J1` before feeding into the amplification stage.
   - **`C4` (10 pF):** Shunt capacitor to `GNDREF` for high-frequency stability and parasitic ringing suppression.

3. **High-Speed Gain Stage (`U2`, `R4`, `R5`)**
   - **`U2` (LM7171BIN — Non-Inverting Amplifier):** A very high-speed, high-slew-rate voltage-feedback operational amplifier configured in a non-inverting topology to amplify the combined DC + AC signal.
   - **`R4` (510 Ω) & `R5` (510 Ω):** Feedback resistor network setting a closed-loop voltage gain off, preserving fast signal transitions.

4. **LED Driver & Output Modulation Stage (`R6`, `C1`, `Q1`, `JP2`)**
   - **`R6` (47 Ω) & `C1` (20 pF):** Gate resistor and shunt capacitance placed between `U2` output and the MOSFET gate to damp high-frequency oscillations and control switching edge rates.
   - **`Q1` (IRF510PBF — N-Channel Power MOSFET):** Acts as the current-modulating driver stage (Drain connected to `VCC` / LED load path, Source routed through jumper `JP2` to `GNDREF`) capable of handling higher LED drive currents at high switching speeds.
   - **`JP1` & `JP2` (Bridged Jumpers):** Hardware test/isolation jumpers allowing easy current measurement or circuit debugging during PCB bring-up.
  
<img width="555" height="345" alt="Reworking skripsi PCB2_Top" src="https://github.com/user-attachments/assets/c21559cf-49af-4e89-bb98-9b0829f1088e" />

<img width="557" height="347" alt="Reworking Skripsi PCB3_Bottom" src="https://github.com/user-attachments/assets/efabda3a-35b6-4af3-864c-74d8b77a299d" />


---
