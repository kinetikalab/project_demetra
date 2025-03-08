# Project Demetra

## Background
Project Demetra is a spin-off of an open-source plasma purification [project Aetheris](https://github.com/kinetikalab/project_aetheris).

Initially, **NO2-/NO3-** were considered unnecessary and harmful byproducts of the water purification process, and it was suggested to remove nitrogen from the air to eliminate **NO2-/NO3-** from the treated water.

However, the synthesis of green "liquid nitrogen" is an important process itself, and there are significant differences compared to water purification in terms of obtaining **NO2-/NO3-** ions in water. For this reason, all work related to green fertilizer has been moved to a separate repository.

## Nitrogen Capture in Gas Discharge: Fundamentals

### Historical Sketch
Attempts to use gas discharge to synthesize nitrogen fertilizers were made more than 100 years ago. The Birkeland-Eyde process used arc discharge to produce NO, which was then converted into nitric acid. 
However, the Birkeland-Eyde process lost competition to the Haber-Bosch process, as it consumed 60-80 kWh/kg N.

In recent years, interest in plasma-based nitrogen capture has been growing. While theoretical advancements have been made, the practical implementation of plasma-based methods remains close to the Birkeland-Eyde process in terms of energy efficiency and scalability.

The importance of more efficient, affordable, and sustainable nitrogen fertilizers cannot be overstated. The use of synthetic nitrogen fertilizers is directly responsible for sustaining nearly half of the world's population.

However, the Haber-Bosch process accounts for about 1-2% of global energy consumption and is responsible for 1-2% of greenhouse gas emissions from ammonia production and distribution alone. Moreover, the centralization of the nitrogen fertilizer market—primarily concentrated near natural gas extraction sites—reduces the resilience of food supply chains in developing countries, where both access to fertilizers and their efficient use remain major challenges.

This document describes a method to create a highly efficient plasma generator capable of synthesizing **NO3-** in water with energy efficiency comparable to the Haber-Bosch process.


### Step-by-Step process
Nitrogen is the primary component of air, comprising approximately 78% of its mass. However, the main challenge is that N₂ is an extremely strong and stable molecule due to its triple bond, which is difficult to break.

The triple bond is not only strong, but the cross-section of direct electron impact dissociation is negligible (due to certain quantum mechanical restrictions). That is why, for example, one can't find the N₂ dissociation cross-section in the LXCAT database.

Let's start at the end. We need the NO₃⁻ ion in liquid, which is obtained by oxidizing NO₂⁻, given a high concentration of O₃ and O₂.
NO₂⁻ is the product of HNO₂ dissociation in water. HNO₂ has medium solubility, but under certain conditions (described below), it can dissolve quite quickly:
```
HNO₂ → H⁺ + NO₂⁻
```
The fastest way to generate HNO₂ is:
```
NO + OH + M → HNO₂ + M, k = 2.16E-17, for N = 2.7E25 (a very fast reaction!)
```
So we need NO and OH.

Let's focus on NO. NO is the Holy Grail of nitrogen capture; all plasma-based nitrogen capture technologies somehow focus on NO production.

We are not considering the thermal reaction:
```
N₂ + O₂ → 2NO
```
due to the huge energy losses required for heating. 

However, at an acceptable temperature, the fastest way to synthesize NO is via the Zeldovich mechanism:
```
N₂* + O → NO + N
```
with an additional bonus:
```
N + OH → NO + H
```
Thus, if we have excited N₂*, atomic oxygen, and OH, we can efficiently obtain two NO molecules.

Surprisingly, N₂* is not a problem in gas discharge, as about 50–70% of discharge energy is utilized for N₂ excitation. For an efficient Zeldovich reaction, vibrational levels of metastable A³ (and higher) states at 3–4+ are sufficient.

But the real challenge is oxygen. Atomic oxygen is obtained through the reaction:
```
O₂ + e⁻ → O(¹D) + O(³P), Eₑ > 8.4 eV
```
The second, more efficient reaction:
```
O₂ + e⁻ → O(³P) + O(³P), Eₑ > 6.2 eV
```
unfortunately has a significantly lower cross-section.

Taking into account that air consists of ~22% O₂ and 78% N₂, and that the N₂ excitation reaction consumes 2–3 times less energy than O₂ dissociation, we always face an oxygen deficit.

For every 5–6 N₂* molecules, we have only one O atom.

**Oxygen deficit is the main problem of plasma-based nitrogen capture.**

This statement is not entirely novel but is often overlooked in the literature.

To solve the oxygen deficit problem, we need a way to transfer energy from N₂* to O₂. Fortunately, we have one:
```
N₂(A³) + O₂ → O + O + N₂, k = 5E-18 × exp(-210/T)
```
This reaction is even more probable than the Zeldovich process, considering that O₂ concentration is much higher than O concentration. Approximately 70% of N₂(A³) reacts with O₂, generating atomic oxygen (while the remaining 30% produces O₂(a¹)).

The next question is: how can we direct more energy into N₂(A³) excitation rather than into N₂(v=1..5)?
BOLSIG+ provides a clear answer—increase the mean electron energy to 4–5 eV. For example, when the mean Eₑ = 2 eV, only 16% of the total discharge energy goes into N₂(A³) excitation, compared to 53% when Eₑ = 5 eV.

However, Eₑ > 5 eV is not typical in gas discharges at atmospheric pressure, because the self-consistent electric field directly limits electron energy.

**The final challenge – how to overcome the self-consistent electric field limitation?**
Surprisingly, the solution is quite simple: add water vapor to the discharge zone, making up ~30–40% of the total molecular concentration. The result is humid, warm air at ~60–70°C.

1. Water molecules have a high electron attachment cross-section at energies >5 eV, so the mean electron energy shifts to the right to compensate for attachment losses and rebalance the Townsend equilibrium.
2. Rotational excitations significantly reduce electron mobility, thereby slowing electron density growth and therefore higher self-consistent electric field to sustain discharge.

**TBD – Demonstrate a 2D Plasma Drift-Diffusion model to support this claim.**

**Final Bonus**
In the presence of H₂O, O(¹D) predominantly generates OH radicals:
```
O(¹D) + H₂O → OH + OH
```
These OH molecules are crucial for the second NO capture step and HNO₂ synthesis.


## Energy Balance: Back-of-the-Napkin Estimate

Let's consider a discharge with a mean electron energy of **5 eV** in an **N₂/O₂/H₂O (50%/13%/37%)** mixture.  

According to the **BOLSIG+** solution:  
- **~16–19%** of the energy is spent on **O and O(¹D) generation**  
- **~16%** is spent on **N₂(v=2..5) excitation**  
- **~53%** is spent on **N₂(A³) excitation**  

On a weighted average:  
- **One N₂*** excitation costs **~2.6 eV**  
- **Atomic oxygen (O) costs ~3.2 eV** (close to the dissociation energy due to efficient energy transfer from **N₂*** to **O₂**)  
- **Two OH radicals cost ~3.8 eV** (calculated as **8.2/2 × 0.9**)  

Additional **OH** can be obtained through the **attachment process**:  

```
O₂ + e⁻ → O⁻ + O  
O⁻ + H₂O → OH⁻ + OH  
OH⁻ + e⁻ → OH + 2e⁻  
OH⁻ + O₂⁺/N₂⁺ → OH + O₂/N₂  
```

## Key Lessons Learned
For efficient NO2-/NO3- capture from the air, the following conditions must be met:
1. Discharge in Hot Wet Air
2. Efficient mixing to saturate the water with oxigen and ensure rapid dissolution of HNO2
3. Discharge Chamber design that from one hand avoid hot arc and from another hand has not dielectric barrier to avoid discharge initialtion losses

## Design Principles
Returning to [project Aetheris](https://github.com/kinetikalab/project_aetheris) and plasma ignition in highly humidified air:

1. **High OH Radical Concentration**: A high concentration of OH radicals is achieved easily (refer to the [project Aetheris](https://github.com/kinetikalab/project_aetheris) repository for a detailed explanation).

2. **Increased Electron Energy in Discharge**: The presence of high water vapor concentrations increases electron energy in the discharge. This phenomenon is not immediately obvious and requires further explanation.
   - The self-consistent electric field in plasma is a fundamental issue. Increasing the external electromagnetic field strength alone does not necessarily increase mean electron energy, as electron density screens the external field.
   - Consequently, the equilibrium mean energy is governed by the ionization-attachment balance rather than the external field strength.
   - Water vapor shifts the mean electron energy upward due to the high attachment rates of water molecules at Ee > 5 eV (TBD: show plasma model).

3. **Stable Thermal Discharge for Energy Efficiency**: To ensure energy efficiency, a stable non-thermal and non-DBD discharge must be used, such as a gliding arc or streamer discharge.

4. **Minimization of Byproduct Losses**: Once the N2 molecule is dissociated, byproducts such as NO2, N2O5, NO3, and N2O must be recirculated into the discharge to regenerate NO (refer to the Secondary Reactions section).

Ultimately, the design remains similar to [project Aetheris](https://github.com/kinetikalab/project_aetheris) but employs a different [discharge_chambers](./discharge_chambers/). The selected configuration is a **spiral gliding arc** (refer to the `discharge_chamber` folder for details).

## Latest Experimental Results
**Date:** March 5, 2024

- **Power Consumption:** 90 W (pump) + 60 W (discharge)
- **Treatment Time:** 3 minutes
- **Volume:** 6 L

**Measured Concentrations:**  
- **NO2-:** 10-20 ppm (approximate, pending verification with ion-selective electrode [ISE])  
- **NO3-:** ~150-200 ppm (approximate, pending verification)  

These results appear promising but require further verification.
