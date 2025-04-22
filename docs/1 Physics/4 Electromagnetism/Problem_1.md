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
---

# 🧲 Lorentz Force – Parameter Exploration & Visualization

## 3. 🧪 Parameter Exploration

To fully understand the dynamics of charged particle motion, we introduce interactive control over the physical parameters in the Lorentz force equation:

$$
\mathbf{F} = q\mathbf{E} + q\mathbf{v} \times \mathbf{B}
$$

---

### 🎛️ Parameters to Explore

- **Electric Field Strength**: $\mathbf{E} = (E_x, E_y, E_z)$  
  Adjust the intensity and direction of the electric field.

- **Magnetic Field Strength**: $\mathbf{B} = (B_x, B_y, B_z)$  
  Set uniform or directional magnetic fields.

- **Initial Velocity**: $\mathbf{v}_0 = (v_x, v_y, v_z)$  
  Define the starting motion of the particle.

- **Particle Properties**:
  - Charge $q$
  - Mass $m$

---

### 🧠 Effects of Parameters

- Increasing $E$ leads to linear acceleration in the direction of the field.
- Increasing $B$ affects the curvature (cyclotron frequency).
- The ratio $\frac{q}{m}$ plays a crucial role in determining:
  - Radius of curvature (Larmor radius)
  - Drift velocity in crossed fields.
- Initial velocity $\mathbf{v}_0$ sets the nature of the trajectory: linear, spiral, or helical.

---

### 🧮 Python Code – Interactive Parameter Setup

```python
import numpy as np  # Ensure numpy is imported

# Editable Parameters
q = 1.0  # Charge (C)
m = 1.0  # Mass (kg)
E = np.array([0.0, 1.0, 0.0])  # Electric field vector (V/m)
B = np.array([0.0, 0.0, 1.0])  # Magnetic field vector (T)
v = np.array([1.0, 0.0, 0.0])  # Initial velocity (m/s)
r = np.array([0.0, 0.0, 0.0])  # Initial position (m)

# Time settings
dt = 0.01
steps = 1000

trajectory = []

for _ in range(steps):
    F = q * (E + np.cross(v, B))  # Lorentz force calculation
    a = F / m  # Acceleration
    v = v + a * dt  # Velocity update
    r = r + v * dt  # Position update
    trajectory.append(r.copy())

trajectory = np.array(trajectory)
```
---

# 4. 🧭 Visualization of Particle Motion

![image](https://github.com/user-attachments/assets/efbcc556-d96c-4dc4-a403-a1b1b7791787)
---
```python
import numpy as np
import matplotlib.pyplot as plt

# Generate dummy trajectory data
trajectory = np.array([[i, np.sin(i)] for i in np.linspace(0, 10, 100)])

# Plot trajectory
plt.figure(figsize=(6, 6))
plt.plot(trajectory[:, 0], trajectory[:, 1], label="Charged Particle Path")
plt.title("2D Trajectory of Charged Particle")
plt.xlabel("x (m)")
plt.ylabel("y (m)")
plt.grid(True)
plt.axis("equal")
plt.legend()
plt.show()
```
---

![image](https://github.com/user-attachments/assets/bd6804de-5069-4944-b051-04bcf750110a)
---

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D  # Ensure correct import

# Example trajectory data (Replace with actual simulation data)
trajectory = np.array([[i, np.sin(i), np.cos(i)] for i in np.linspace(0, 10, 100)])

# Create figure & 3D axis
fig = plt.figure(figsize=(8, 6))  # Set figure size for better scaling
ax = fig.add_subplot(111, projection='3d')

# Plot trajectory
ax.plot(trajectory[:, 0], trajectory[:, 1], trajectory[:, 2], label="Charged Particle Path")

# Labels & Title
ax.set_title("3D Trajectory of Charged Particle")
ax.set_xlabel("x (m)")
ax.set_ylabel("y (m)")
ax.set_zlabel("z (m)")
ax.legend()  # Add legend for clarity

# Show plot
plt.show()
```
---
## 📐 Physical Concepts

Understanding the motion of a charged particle under electromagnetic fields involves several key physical quantities.

---

### 🔄 Larmor Radius ($r_L$)

The radius of circular motion in a uniform magnetic field is given by:

$$r_L=\frac{mv_\perp}{|q|B}$$

Where:
- $m$: mass of the particle  
- $v_\perp$: velocity component **perpendicular** to the magnetic field  
- $q$: charge of the particle  
- $B$: magnitude of the magnetic field  

The Larmor radius determines how tightly the particle spirals around the magnetic field lines.

---

### 🔁 Cyclotron Frequency ($\omega_c$)

The angular frequency of the circular motion (also called **gyrofrequency**) is:

$$\omega_c=\frac{|q|B}{m}$$

- Represents how quickly the particle orbits in the magnetic field  
- Independent of the particle’s velocity  

---

### ✖️ $\mathbf{E} \times \mathbf{B}$ Drift Velocity

When a particle is in **crossed electric and magnetic fields**, it experiences a net drift, independent of charge or mass:

$$\mathbf{v}_{\text{drift}}=\frac{\mathbf{E} \times \mathbf{B}}{B^2}$$

- Direction of drift is perpendicular to both $\mathbf{E}$ and $\mathbf{B}$  
- The magnitude depends on the strength and orientation of both fields  
- No net force in the drift direction — the motion is **uniform**  

---

> 🧠 These concepts are fundamental in understanding plasmas, particle traps, and devices like cyclotrons and tokamaks.







