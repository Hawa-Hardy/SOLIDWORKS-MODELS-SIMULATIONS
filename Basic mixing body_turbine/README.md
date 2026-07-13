# Multi-Inlet Fluid Mixing Chamber: Internal Flow Analysis

## Project Overview
This project evaluates the internal flow dynamics and mixing behavior of water inside a three-port cylindrical manifold chamber. The system features two tangential inlets introducing fluid at different velocities and a single perpendicular bottom outlet. The analysis investigates how the dual asymmetric inlets affect velocity distribution, internal pressure gradients, and fluid residence behavior within the main mixing hub.

### Core Engineering Specifications
* **Fluid Domain:** Internal, Single-Phase Incompressible Fluid (Water).
* **Thermal Conditions:** Adiabatic Walls (Zero heat transfer to the environment).
* **System Units:** Metric SI (m, kg, s).

---

## 1. Geometry Preparation & Volume Verification
To ensure a valid, watertight computational domain inside the manifold:
* **Lid Engineering:** Planar lids were modeled and applied to the faces of **Inlet 1**, **Inlet 2**, and the **Outlet** to seal the internal cavity.
* **Volume Isolation:** Setup criteria excluded isolated internal material cavities lacking active flow boundaries to optimize computational efficiency.
* **Fluid Body Generation:** Evaluated the sealed internal volume using the **Check Geometry** tool. A dedicated fluid-body assembly part was generated directly from the cavity volume. This step verified that the extracted fluid domain accurately matched the design specifications without geometry gaps or computational leaks.

![Figure 1: Isometric section view of the mixing chamber detailing the internal fluid domain.](images/image_e4fa0e.png)

---

## 2. Boundary Conditions
To simulate asymmetric fluid injection, boundary conditions were applied directly to the internal faces of the sealed lids:

| Flow Component | Boundary Condition Type | Value | Parameters |
| :--- | :--- | :--- | :--- |
| **Inlet 1 (Left)** | Inlet Velocity | 5 m/s | Normal to face |
| **Inlet 2 (Right)** | Inlet Velocity | 3 m/s | Normal to face |
| **Outlet (Bottom)**| Static Pressure | 101,325 Pa | Ambient environmental pressure |

---

## 3. Convergence Goals
To ensure mathematical stability and terminate the solver based on physics rather than a fixed iteration count, **Surface Goals** were established on the internal face of the outlet lid (**Lid 3**):
* **SG Average Velocity:** Tracks the stabilization of fluid velocity exiting the system.
* **SG Average Temperature:** Monitors convergence of the fluid energy equation.

---

## 4. Simulation Results & Engineering Insights

### Convergence Verification
The solver achieved fully stable mathematical convergence within 115 iterations. Both target parameters reached flat, horizontal asymptotic profiles, confirming that the numerical results are stable and clear of truncation errors.

![Figure 2: Convergence plots demonstrating stable horizontal asymptotic profiles for outlet temperature and velocity.](images/images_e50cd7.png)

### Velocity Profile & Fluid Dynamics
* **Maximum Velocity:** Hit a peak value of **11.77 m/s** concentrated strictly within the throat of the bottom outlet pipe.
* **Chamber Acceleration:** As water transitions from the larger mixing hub into the constricted 400 mm outlet pipe, the flow accelerates rapidly due to the conservation of mass (venturi effect), transforming pressure energy into kinetic energy.

![Figure 3: Mid-plane velocity cut plot highlighting rapid flow acceleration at the outlet throat.](images/image_e50caf.png)

### Trajectory Profiles
* **Vortex Formation:** The flow trajectories demonstrate that the asymmetric velocities (5 m/s vs. 3 m/s) combined with the tangential inlet positioning generate a strong rotational swirl (vortex) inside the main chamber. 
* **Mixing Efficiency:** This induced swirling action creates a highly efficient mixing zone, optimizing fluid homogenization before discharging through the bottom outlet.

![Figure 4: 3D Flow trajectories colored by fluid temperature showing the internal swirling vortex structure.](images/image_e50ccf.png)
