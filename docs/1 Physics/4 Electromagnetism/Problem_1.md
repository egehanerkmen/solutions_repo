# Problem 1

# 🧲 Electromagnetism – Lorentz Force Simulation

## 1. Exploration of Applications

The **Lorentz force** governs the motion of charged particles in the presence of electric and magnetic fields and is given by:

$$
\mathbf{F} = q\mathbf{E} + q\mathbf{v} \times \mathbf{B}
$$

Where:
- $\mathbf{F}$: Force on the particle
  
- $q$: Charge of the particle
   
- $\mathbf{E}$: Electric field
  
- $\mathbf{v}$: Velocity of the particle
  
- $\mathbf{B}$: Magnetic field

---

### 🔬 Real-World Applications

- **Particle Accelerators**  
  Charged particles are accelerated and steered using electric and magnetic fields. Cyclotrons and synchrotrons use the Lorentz force to maintain circular motion and acceleration.

- **Mass Spectrometers**  
  Used to measure the mass-to-charge ratio $\frac{m}{q}$ of ions. Particles enter magnetic fields and follow curved paths, with curvature depending on their properties.

- **Plasma Confinement (Tokamaks)**  
  Plasma is confined in magnetic fields to achieve nuclear fusion conditions. Helical paths and drift are observed due to complex field geometries.

- **Astrophysical Jets & Cosmic Rays**  
  Particles in space travel under the influence of electromagnetic fields, displaying relativistic helical or spiral paths.

---

### ⚙️ Role of $\mathbf{E}$ and $\mathbf{B}$ Fields

- **Electric Fields** accelerate particles linearly:

  $$\mathbf{F}_E = q\mathbf{E}$$

- **Magnetic Fields** change the direction of motion (not speed):

  $$\mathbf{F}_B = q\mathbf{v} \times \mathbf{B}$$

  Leading to circular or helical trajectories depending on the orientation of $\mathbf{v}$ and $\mathbf{B}$.

---

## 2. Simulating Particle Motion

We simulate the motion of a charged particle under different field conditions using numerical integration (e.g., Euler method or Runge-Kutta).

### ⚛️ Simulation Parameters

- $q$: charge  
- $m$: mass  
- $\mathbf{v}_0$: initial velocity vector  
- $\mathbf{E}$: electric field vector  
- $\mathbf{B}$: magnetic field vector  

---

## 2.1 🧭 Uniform Magnetic Field Only

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants and initial conditions
q = 1.0
m = 1.0
B = np.array([0, 0, 1])
E = np.array([0, 0, 0])
v = np.array([1.0, 0.0, 0.0])
r = np.array([0.0, 0.0, 0.0])

dt = 0.01
steps = 1000
trajectory = []

for _ in range(steps):
    F = q * np.cross(v, B)
    a = F / m
    v = v + a * dt
    r = r + v * dt
    trajectory.append(r.copy())

trajectory = np.array(trajectory)

plt.plot(trajectory[:, 0], trajectory[:, 1])
plt.title("Charged Particle in Uniform Magnetic Field")
plt.xlabel("x")
plt.ylabel("y")
plt.axis("equal")
plt.grid()
plt.show()
```
---

# 2.2 ⚡ Uniform Electric and Magnetic Fields (Parallel)

```python
# Set E and B fields
E = np.array([0.0, 0.0, 1.0])
B = np.array([0.0, 0.0, 1.0])

v = np.array([1.0, 0.0, 0.0])
r = np.array([0.0, 0.0, 0.0])
trajectory = []

for _ in range(steps):
    F = q * (E + np.cross(v, B))
    a = F / m
    v = v + a * dt
    r = r + v * dt
    trajectory.append(r.copy())

trajectory = np.array(trajectory)

fig = plt.figure()
ax = fig.add_subplot(projection='3d')
ax.plot(trajectory[:, 0], trajectory[:, 1], trajectory[:, 2])
ax.set_title("Uniform E and B Fields (Parallel)")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
plt.show()
```
---

# 2.3 ✖️ Crossed Electric and Magnetic Fields

```python
# Crossed fields
E = np.array([1.0, 0.0, 0.0])
B = np.array([0.0, 0.0, 1.0])

v = np.array([0.0, 0.0, 0.0])
r = np.array([0.0, 0.0, 0.0])
trajectory = []

for _ in range(steps):
    F = q * (E + np.cross(v, B))
    a = F / m
    v = v + a * dt
    r = r + v * dt
    trajectory.append(r.copy())

trajectory = np.array(trajectory)

plt.plot(trajectory[:, 0], trajectory[:, 1])
plt.title("Crossed E and B Fields")
plt.xlabel("x")
plt.ylabel("y")
plt.axis("equal")
plt.grid()
plt.show()
```


