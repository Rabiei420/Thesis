## Macroscale Asphalt Pavement Models

This directory contains the macroscale models for both **dry** and **saturated** pavement conditions. The files are located within the `ABAQUS Model and ODB files` directory.

### ⚠️ Software Compatibility
* Both models are built within the `Asphalt pavement model` (`.cae` extension) file.
* **Important:** The models were created using **ABAQUS version 2024**. They can only be opened with ABAQUS 2024 or newer. Backward compatibility with older versions is not supported.

---

## Model Descriptions & Material Properties

Within the ABAQUS project file, you will find two primary models:
1. `Macroscale Model-Dry`: Simulates the pavement under dry conditions.
2. `Macroscale Model-saturated`: Simulates the pavement under saturated conditions.

Detailed justifications for the material parameters can be found in the accompanying thesis. The properties are derived from the following sources and guidelines:

### 1. Geometric Dimensions
* **Reference:** German Guideline **RStO 12** (*FGSV 499*), Page 19, Plate 1 (2.1).

### 2. Mechanical & Viscoelastic Properties
* **Reference:** German Guideline **RDO 09** (*FGSV 488*).
* **Layers 1 & 2 (Asphalt Surface & Binder Courses - *Asphaltdeckelschicht* & *Asphaltbinderschicht*):** Viscoelastic parameters are directly implemented from the laboratory experimental results published by **Liu et al. (2022) [1]**.
* **Layer 3 (Asphalt Base Course - *Asphalttragschicht*):** The elastic modulus is calculated using the temperature-dependent functions on page 34 of the RDO guideline (Equations A7 and A8). For Equation A8, the parameters are evaluated at **20°C** and **80 Hz**.
* **Layer 4 (Hydraulically Bound Layer - *HGT*):** The elastic modulus is selected according to Appendix 3 (page 32) of the RDO guideline.
* **Layers 5 & 6 (Frost Protection Layer & Subgrade):** The elastic moduli are retrieved from Table A7 (page 39) of the RDO guideline.

### 3. Hydraulic Properties (Saturated Condition Only)
* **Reference:** **Sui et al. (2020)**. 
* **Methodology:** Values are based on experimental measurements of dense asphalt concrete (AC-20) using a hollow Marshall specimen under varying hydraulic heads. Laboratory results indicated vertical hydraulic conductivities on the order of $10^{-4}$ m/s.
* **Implementation:** * A **Horizontal-to-Vertical (H/V) ratio of 10:1** is implemented to capture the transversely isotropic behavior of the asphalt mixture.
  * For the **top 4 layers**, the vertical hydraulic conductivity is selected within the experimental range of the reference study, and horizontal conductivities are adjusted based on the 10:1 ratio.
  * The **lower layers** are assigned a lower magnitude of vertical hydraulic conductivity.
* **Data Log:** The complete list of hydraulic conductivities can be found in **Table 4 of the thesis** and are processed in the Excel file `[Insert Excel Filename.xlsx]` under sheet `[Insert Sheet Name/Number]`.

---

## Model Results & ODB Files

The macroscale simulation results are managed under the **Jobs** section in ABAQUS.

* **File Location:** To view the outputs, the Output Database (`.odb`) files must remain in the same directory as the ABAQUS model file (`.cae`).
* **Unprocessed Variables:** All `.odb` files contain complete, unprocessed variable results.

### Key Analysis Jobs
* `NM-Dry-displacement`
* `NM-saturated-displacement`

> 💡 **Note:** These specific jobs restrict the output variables strictly to **displacement values**. These outputs are intentionally streamlined to be transferred as displacement boundary histories into subsequent **mesoscale models**.

---

### References
* **[1]** Liu et al. (2022). *[Insert full citation if needed]*
* **[2]** Sui et al. (2020). *[Insert full citation if needed]*
