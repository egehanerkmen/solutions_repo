# 🧪 Waves: Interference Patterns on a Water Surface

## 🎯 Step 1: Choose a Regular Polygon

To analyze wave interference from multiple coherent sources, we begin by selecting a **regular polygon**. Each vertex of this polygon acts as a **point wave source** on a two-dimensional water surface.

- We choose a **regular pentagon** (5 sides).
- The polygon is centered at the origin $(0,0)$.
- The radius $R$ of the circumcircle defines the distance from the center to each vertex.

> This setup ensures symmetrical placement of sources and allows for clear observation of interference patterns.

---

## 🧮 Step 2: Determine Coordinates of Vertices

To calculate the positions of the wave sources located at the vertices, we use the formula for a regular polygon inscribed in a circle:

- Let the number of vertices be $N$.
- Each vertex is positioned at:

$$
(x_i,y_i)=\left(R\cos\left(\frac{2\pi i}{N}\right),\ R\sin\left(\frac{2\pi i}{N}\right)\right)
$$

where $i=0,1,2,\dots,N-1$
---

![image](https://github.com/user-attachments/assets/f733dc26-8cf0-41fb-a606-58e001b9751f)


---

## 🌊 Step 3: Define Wave Parameters

Each wave emitted from the sources is described by:

- **Amplitude**: $A$
  
- **Wavelength**: $\lambda$
  
- **Frequency**: $f$
  
- **Initial Phase**: $\phi$
  

From these, we compute:

- **Wave number**:
  
$$
k=\frac{2\pi}{\lambda}
$$

- **Angular frequency**:
  
$$
\omega=2\pi f
$$

---

## 🔁 Step 4: Formulate Individual Wave Equations

Each wave $\eta_i(x,y,t)$ emitted from the source located at $(x_i,y_i)$ is given by:

$$
\eta_i(x,y,t)=\frac{A}{\sqrt{r_i}}\cdot\cos(kr_i-\omega t+\phi)
$$

where:

$$
r_i=\sqrt{(x-x_i)^2+(y-y_i)^2}
$$

- This expression models **circular wavefronts** on the water surface.
- The $1/\sqrt{r_i}$ decay factor reflects the diminishing amplitude with distance.

---

### 🔬 Step 5: Apply Superposition Principle

According to the principle of superposition, the total wave displacement at any point $(x,y)$ and time $t$ is the sum of the contributions from all $N$ sources:

$$
\eta_{\text{sum}}(x,y,t) = \sum_{i=1}^{N} \eta_i(x,y,t)
$$

Where $\eta_i(x,y,t)$ is the wave displacement from the $i^{th}$ source. This summation accounts for constructive and destructive interference patterns, as the waves combine at each point $(x,y)$ based on the phase differences between them. Constructive interference occurs when the waves are in phase, amplifying the displacement, while destructive interference happens when the waves are out of phase, leading to partial or complete cancellation.

Thus, the total displacement $\eta_{\text{sum}}(x,y,t)$ represents the result of wave interactions across the entire system of sources.

---

### 🖥️ Step 6: Simulate the Displacement Over a 2D Grid

To simulate the wave displacement over the water surface, we first define a 2D spatial grid representing the region of interest. Let the grid be defined for $x, y \in [-L, L]$, where $L$ is the spatial extent of the grid. A finer grid resolution leads to better visual accuracy but requires more computational resources.

1. **Define Grid**: 
   - $x, y$ are linearly spaced between $-L$ and $L$, where $L$ is the maximum spatial range.
   - We use meshgrid functions to create a grid of points at which the displacement will be calculated.

2. **Choose a Time Snapshot**:
   - For visualization purposes, we can choose a fixed time $t$ (e.g., $t=0$) to compute and observe the wave interference pattern at that specific moment.

3. **Evaluate Total Displacement**:
   - For each grid point $(x, y)$, compute the displacement $\eta_{\text{sum}}(x,y,t)$ as the sum of displacements from all $N$ sources.
   - This step involves iterating over all the sources and applying the wave equation for each one.

This simulation provides us with a matrix of values representing the wave surface at a given time, which can be visualized to study the interference effects.

---

### 🎨 Step 7: Visualize and Analyze Interference Patterns/Plot

![image](https://github.com/user-attachments/assets/b8f65312-ba2b-4cf9-9a37-0624304765bd)
---

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
A = 1.0      # Amplitude
lambda_ = 1.0  # Wavelength
f = 1.0      # Frequency
phi = 0       # Initial Phase
R = 5.0      # Radius of the polygon
L = 10       # Grid size limit
N = 5        # Number of sources (for pentagon)

# Calculate wave number and angular frequency
k = 2 * np.pi / lambda_
omega = 2 * np.pi * f

# Coordinates of the sources (vertices of a regular polygon)
theta = np.linspace(0, 2 * np.pi, N, endpoint=False)
x_sources = R * np.cos(theta)
y_sources = R * np.sin(theta)

# Define grid for simulation
x_vals = np.linspace(-L, L, 400)
y_vals = np.linspace(-L, L, 400)
X, Y = np.meshgrid(x_vals, y_vals)

# Function to calculate displacement from one source
def displacement(x, y, x_i, y_i, A, k, omega, t, phi):
    r_i = np.sqrt((x - x_i)**2 + (y - y_i)**2)
    return (A / np.sqrt(r_i)) * np.cos(k * r_i - omega * t + phi)

# Simulate total displacement by summing contributions from all sources
def total_displacement(X, Y, x_sources, y_sources, A, k, omega, t, phi):
    eta_sum = np.zeros_like(X)
    for i in range(len(x_sources)):
        eta_sum += displacement(X, Y, x_sources[i], y_sources[i], A, k, omega, t, phi)
    return eta_sum

# Choose a fixed time t = 0 for visualization
t = 0
eta_sum = total_displacement(X, Y, x_sources, y_sources, A, k, omega, t, phi)

# Visualize the displacement using contour plot
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, eta_sum, levels=100, cmap='RdBu')
plt.colorbar(label='Displacement')
plt.title("Interference Pattern: Water Surface Displacement")
plt.xlabel("X")
plt.ylabel("Y")
plt.show()
```

---




