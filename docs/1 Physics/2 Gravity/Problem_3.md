#  Problem 3:
# Trajectories of a Freely Released Payload Near Earth

---
Before diving into theory, explore how real spacecraft move using NASA’s official 3D simulation platform:

🌐 [NASA Eyes on the Solar System](https://eyes.nasa.gov/)

> Real-time orbits, mission tracking, and gravity interactions!

---
##  Motivation

When a payload is released from a moving rocket near Earth, it can follow a wide range of trajectories based on its **initial speed, direction, and altitude**. These can include:

- Reentry into Earth’s atmosphere,
- Stable orbits (elliptical or circular),
- Escape into space.

Understanding these trajectories is crucial for:

- Satellite deployment,
- Reentry planning,
- Interplanetary missions.

This problem blends **orbital mechanics** with **numerical simulation**, providing practical insight into real-world space mission planning.

---

## Governing Physics

To better understand gravitational attraction and orbital motion, you can explore this interactive simulation:

🌐 [PhET: Gravity and Orbits](https://phet.colorado.edu/en/simulation/gravity-and-orbits)

> Visualize how mass, distance, and velocity affect planetary orbits and satellite motion in real time!

### Newton’s Law of Universal Gravitation

The gravitational force acting on a payload is:

$$
\vec{F} = -\frac{GMm}{r^2} \hat{r}
$$

Where:

- \( G = 6.674 \times 10^{-11} \, \text{m}^3/\text{kg} \cdot \text{s}^2 \) is the gravitational constant,
- \( M = 5.972 \times 10^{24} \, \text{kg} \) is Earth’s mass,
- \( m \) is the mass of the payload (cancels out later),
- \( r \) is the distance between Earth’s center and the payload,
- \( \hat{r} \) is the unit vector pointing toward Earth’s center.

Using Newton’s Second Law:

$$
\vec{a} = \frac{\vec{F}}{m} = -\frac{GM}{r^2} \hat{r}
$$

This gives us the acceleration at any point, which we use for simulation.

---

##  Orbital Energy and Trajectories

Total specific mechanical energy of the payload:

$$
\epsilon = \frac{v^2}{2} - \frac{GM}{r}
$$

- \( \epsilon < 0 \): Elliptical orbit (bound)
- \( \epsilon = 0 \): Parabolic trajectory (escape)
- \( \epsilon > 0 \): Hyperbolic trajectory (escape)

Escape velocity at distance \( r \):

$$
v_{\text{esc}} = \sqrt{\frac{2GM}{r}}
$$

Escape velocity decreases with altitude since gravitational pull weakens. It is given by:

$$
v_{\text{esc}} = \sqrt{\frac{2GM}{r}}
$$

Below is a plot showing how escape velocity changes with altitude:

![ Alt Text](888.png)


##  Numerical Simulation (Euler Method)

We use the **Euler method** to simulate the motion of the payload. It updates position and velocity step-by-step using:

$$
\vec{v}_{n+1} = \vec{v}_n + \vec{a}_n \cdot \Delta t
$$

$$
\vec{r}_{n+1} = \vec{r}_n + \vec{v}_{n+1} \cdot \Delta t
$$

### Assumptions:

- Earth is a point mass at origin.
- Motion is in 2D space (x, y).
- Only gravity affects the payload (no atmosphere, drag, etc.).

---

##  Python Implementation

```python
import numpy as np

# Constants
G = 6.67430e-11
M = 5.972e24
R_earth = 6.371e6

# Initial conditions
altitude = 300e3
r0 = R_earth + altitude
v0 = 7500  # m/s
theta = np.radians(0)  # launch angle

x = [r0]
y = [0]
vx = [0]
vy = [v0]

dt = 1
t_max = 8000
N = int(t_max / dt)

print("Time(s)\tX(km)\tY(km)\tSpeed(km/s)\tDistance(km)")

for i in range(N):
    r = np.sqrt(x[-1]**2 + y[-1]**2)
    ax = -G * M * x[-1] / r**3
    ay = -G * M * y[-1] / r**3

    vx_new = vx[-1] + ax * dt
    vy_new = vy[-1] + ay * dt

    x_new = x[-1] + vx_new * dt
    y_new = y[-1] + vy_new * dt

    distance_km = np.sqrt(x_new**2 + y_new**2) / 1000
    speed_kms = np.sqrt(vx_new**2 + vy_new**2) / 1000

    print(f"{i*dt}\t{x_new/1000:.2f}\t{y_new/1000:.2f}\t{speed_kms:.2f}\t{distance_km:.2f}")

    if distance_km * 1000 <= R_earth:
        print("\n>> Payload has impacted the Earth at t =", i*dt, "seconds.")
        break

    x.append(x_new)
    y.append(y_new)
    vx.append(vx_new)
    vy.append(vy_new)

## 🔍 Explore Further: Beyond Earth

While this project focuses on payloads near Earth, it's also valuable to understand more complex gravitational dynamics.

🎥 **SkyMarvels™ – Solar System Barycenter**  
How the Sun moves due to gravitational pulls from the planets — visualized with Celestia.

[![Solar System Barycenter](https://img.youtube.com/vi/1iSR3Yw6FXo/0.jpg)](https://www.youtube.com/watch?v=1iSR3Yw6FXo)

> Barycenters explain why the Sun itself moves slightly — important for understanding motion in multi-body systems.
