# Project Demetra

## Background
Project Demetra is a spin-off of an open-source plasma purification [project Aetheris](https://github.com/kinetikalab/project_aetheris).
Initially, **NO2-/NO3-** were considered unnecessary and harmful byproducts of the water purification process. It was suggested to remove nitrogen from the air to eliminate **NO2-/NO3-** from the treated water.

However, the synthesis of green liquid nitrogen is an important process, and there are significant differences compared to water purification in terms of obtaining **NO2-/NO3-** ions in water. For this reason, all work related to green fertilizer has been moved to a separate repository.

## Nitrogen Capture in Gas Discharge: Fundamentals
Nitrogen is the primary component of air, comprising approximately 78% of its mass. However, the main challenge is that N2 is an extremely strong and stable molecule due to its triple bond, which is difficult to break.

The simplest and most straightforward reaction pathways for incorporating nitrogen into liquid form are as follows:

### Stage 1 - NO Synthesis
#### Pathway 1:
N2 + e → N + N + e (Ee > 9.8 eV)  
N + OH → NO + H  

#### Pathway 2:
N2 + e → N2(A3) + e (Ee > 6.2 eV)  
N2(A3) + O → N(2D) + NO  
N(2D) + O2 → NO + O(1D)

#### Pathway 3 (Thermal Reaction):
N2 + O → NO + N (T > 4000K)  

Energy levels of approximately 10 eV are rare in atmospheric-pressure gas discharges, making the second mechanism the most prevalent in NO synthesis. It is also important to note that in plasma, stepwise excitation occurs through intermediate vibrational N2 states.

The thermal reaction suggests that a hot discharge (e.g., gliding arc, streamer discharge) is required rather than a cold discharge (e.g., dielectric barrier discharge, DBD).

In summary, maintaining high electron energy is **essential** to ensure a high NO production rate.

### Stage 2 - HNO2/HNO3 Synthesis
HNO2 is a crucial molecule due to its high Henry constant, which allows it to dissolve easily in water. HNO2 can be synthesized via the reaction:

NO + OH + M → HNO2 + M  

### Stage 3 - NO2-/NO3- in Liquid Phase
HNO2 rapidly dissolves in water, undergoing dissociation into NO2- and H+:

HNO2 → NO2- + H+  

NO2- can be further oxidized to NO3-.

## Secondary Reactions
Further discussion is needed regarding reactions involving NO2 and NO3 in the gas phase, particularly higher nitrogen oxides and their reaction cycles.

### Key Lessons Learned
For efficient NO2-/NO3- capture from the air, the following conditions must be met:
1. High electron energy.
2. High concentrations of OH and O radicals.
3. Efficient and rapid gas-liquid mixing.

## Design Principles
Returning to [project Aetheris](https://github.com/kinetikalab/project_aetheris) and plasma ignition in highly humidified air:

1. **High OH Radical Concentration**: A high concentration of OH radicals is achieved easily (refer to the [project Aetheris](https://github.com/kinetikalab/project_aetheris) repository for a detailed explanation).

2. **Increased Electron Energy in Discharge**: The presence of high water vapor concentrations increases electron energy in the discharge. This phenomenon is not immediately obvious and requires further explanation.
   - The self-consistent electric field in plasma is a fundamental issue. Increasing the external electromagnetic field strength alone does not necessarily increase mean electron energy, as electron density screens the external field.
   - Consequently, the equilibrium mean energy is governed by the ionization-attachment balance rather than the external field strength.
   - Water vapor shifts the mean electron energy upward due to the high attachment rates of water molecules at Ee > 4 eV (TBD: add cross-section analysis from LXCAT).
   - To compensate for electron losses in the attachment process, the ionization-attachment equilibrium shifts accordingly (TBD: verify using a 2D plasma-fluid model).

3. **Stable Thermal Discharge for Energy Efficiency**: To ensure energy efficiency, a stable thermal discharge must be used, such as a gliding arc or streamer discharge.

4. **Minimization of Byproduct Losses**: Once the N2 molecule is dissociated, byproducts such as NO2, N2O5, NO3, and N2O must be recirculated into the discharge to regenerate NO (refer to the Secondary Reactions section).

Ultimately, the design remains similar to [project Aetheris](https://github.com/kinetikalab/project_aetheris) but employs a different [discharge_chambers](./discharge_chambers/). The selected configuration is a **spiral gliding arc** (refer to the `discharge_chamber` folder for details).

## Latest Experimental Results
**Date:** February 6, 2024

- **Power Consumption:** 100 W (pump) + 36 W (discharge)
- **Treatment Time:** 3 minutes
- **Volume:** 6 L

**Measured Concentrations:**  
- **NO2-:** 10-20 ppm (approximate, pending verification with ion-selective electrode [ISE])  
- **NO3-:** 100-200 ppm (approximate, pending verification with ISE)  

**Cost Analysis:**  
- **N Production Cost (Electricity at $0.05/kWh):** $1.03 - $2.06 per kg of N  

These results appear promising but require further verification.
