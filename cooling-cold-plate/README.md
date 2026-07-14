# Conjugate Heat Transfer & Fluid Flow Analysis

## Project Overview
This project simulates conjugate heat transfer to evaluate the thermal management of an Aluminum 6061 plate generating a high thermal load. The system is cooled via an internal pipe channeling a two-part gaseous mixture of Refrigerant R-134a and Air. The simulation couples both fluid dynamics (forced convection) and solid thermodynamics (conduction) within a gravity-enabled external environment to accurately predict maximum system temperatures.

### Core Engineering Specifications
* **Analysis Type:** External Flow with Gravity and Solid Conduction enabled.
* **Fluid Mixture:** Refrigerant R-134a (0.8 concentration) and Air (0.2 concentration) modeled as Real Gases.
* **Solid Material:** Aluminium 6061 (Applied globally).
* **System Units:** Metric SI (m, kg, s, K).

---

## 1. Domain Setup & Fluid Subdomains
Because this is an external analysis featuring internal cooling channels, the computational environment required specific zoning:
* **Computational Domain:** The global bounding box was optimized and resized tightly around the solid to minimize unnecessary external mesh cell calculations while capturing radiant/convective effects.
* **Fluid Subdomain:** A dedicated fluid subdomain was isolated inside the internal pipe geometry to confine the Refrigerant/Air mixture strictly to the cooling channel, preventing it from incorrectly filling the external atmospheric domain.

![Figure 1: Section view of the computational domain and isolated fluid subdomain setup.](images/image_620b00.png) *(Note: Replace with your actual section view/domain setup image)*

---

## 2. Thermal & Flow Boundary Conditions
To replicate the physical operating parameters, the following inputs were defined:

| Location | Condition Type | Value | Engineering Purpose |
| :--- | :--- | :--- | :--- |
| **Lid 1 (Inlet)** | Mass Flow Rate | $0.008\text{ kg/s}$ | Defines the cooling fluid intake normal to the face. |
| **Lid 2 (Outlet)** | Static Pressure | Ambient | Defines the exit boundary with a baseline fluid temperature of $261.15\text{ K}$. |
| **Plate (Back Face)**| Surface Heat Source | $1200\text{ W}$ | Simulates a high-power electronic or mechanical component generating constant heat. |

---

## 3. Engineering Goals for Convergence
To prevent the solver from terminating prematurely, specific thermal criteria were tracked to ensure steady-state equilibrium was mathematically reached:
* **Surface Goals (Maximums):** Tracked the maximum fluid temperature at the outlet (Lid 2) and the total solid temperature directly at the heat source plate.
* **Global Goals (Maximums):** Monitored the overall maximum fluid and solid temperatures across the entire computational domain.

---

## 4. Analysis Results & Engineering Insights

### Solver Convergence
The solver successfully reached steady-state conditions, with the Global Goal plots demonstrating flat asymptotic lines for temperature versus iterations. This confirms the heat being generated ($1200\text{ W}$) reached a stable equilibrium with the heat being dissipated by the refrigerant flow and external environment.

![Figure 2: Goal plot showing stable temperature convergence over solver iterations.](images/image_62125f.png) *(Note: Replace with your Goal Plot graph)*

### Thermal Distribution & Heat Dissipation
* **Maximum System Temperature:** The analysis identified a peak solid temperature of **$546.71\text{ K}$** located at the heat source plate. 
* **Solid Conduction:** The Surface Plot reveals how the Aluminium 6061 conducts the heat outward from the $1200\text{ W}$ generation zone, creating a clear thermal gradient as it approaches the cooling pipe.

![Figure 3: Solid temperature surface plot detailing the thermal gradient across the Aluminum plate.](images/image_6212a2.png) *(Note: Replace with your Surface Plot image)*

### Fluid Flow & Cooling Efficiency
* **Fluid Heat Absorption:** The mid-plane Cut Plot (offset by $0.02\text{ m}$) and Flow Trajectories show the cold internal refrigerant mixture entering the pipe, absorbing thermal energy from the adjacent aluminum walls, and exiting at a significantly higher temperature. 
* **Conclusion:** The forced convection provided by the $0.008\text{ kg/s}$ mass flow rate successfully extracts heat from the core system, though localized hot spots remain on the extreme edges of the plate, suggesting potential areas for design optimization (e.g., adding cooling fins or increasing mass flow).

![Figure 4: Cut plot and 3D flow trajectories showing the refrigerant fluid absorbing heat as it traverses the pipe.](images/image_6211c8.png) *(Note: Replace with your Cut Plot / Trajectories image)*
