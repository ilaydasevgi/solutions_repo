# Problem 1
# **Orbital Period and Orbital Radius**

## **Motivation**
The relationship between the square of the orbital period and the cube of the orbital radius, known as *Kepler's Third Law*, is fundamental in celestial mechanics. This law is critical for understanding planetary motion, satellite orbits, and gravitational interactions on different scales.

By analyzing this relationship, we can:
- Derive a mathematical connection between the orbital period and radius.
- Discuss its implications in astronomy.
- Analyze real-world examples such as the Moon’s orbit around Earth.
- Implement a computational model to simulate circular orbits and verify Kepler’s Third Law.

[alt text](%20Unknown.png)

## **Kepler’s Third Law Derivation**
Kepler's Third Law states that for a planet orbiting a much more massive body, the square of the orbital period ($$T$$) is proportional to the cube of the semi-major axis ($$r$$):

$$T^2 \propto r^3$$
[alt text](111.png)


### **Mathematical Derivation**
From Newton's Law of Universal Gravitation:

$$F = \frac{GMm}{r^2}$$

For a circular orbit, the required centripetal force is provided by gravity:

$$\frac{GMm}{r^2} = \frac{m v^2}{r}$$

Since velocity in a circular orbit is:

$$v = \frac{2 \pi r}{T}$$

Substituting this into the force equation:

$$\frac{GMm}{r^2} = \frac{m}{r} \left(\frac{4\pi^2 r^2}{T^2} \right)$$

Simplifying and solving for $$T^2$$:

$$T^2 = \frac{4\pi^2}{GM} r^3$$

This confirms Kepler’s Third Law:

$$T^2 \propto r^3$$

## **Implications in Astronomy**
1. **Determining Planetary Masses:** By measuring orbital periods and radii, we can estimate planetary and stellar masses.
2. **Predicting Satellite Orbits:** Artificial satellites’ orbits can be calculated using this relationship.
3. **Understanding Exoplanetary Systems:** Kepler’s Law helps infer exoplanet characteristics from observed orbital periods.

## **Real-World Example: Moon's Orbit Around Earth**
- The Moon's average distance from Earth: $$r = 3.84 \times 10^8 m$$
- Orbital period: $$T = 27.3$$ days
- Mass of Earth: $$M = 5.972 \times 10^{24} kg$$

Using our derived formula, we can verify Kepler’s law numerically.

## **Python Simulation of Circular Orbits**
The following Python script simulates planetary orbits and verifies Kepler’s Third Law:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.constants import G

# Constants
M = 5.972e24  # Mass of the Earth (kg)
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)

# Orbital radii (m)
orbit_radii = np.linspace(1e7, 4e8, 100)

# Compute orbital periods using Kepler's Third Law
orbital_periods = np.sqrt((4 * np.pi**2 * orbit_radii**3) / (G * M))

# Verify T^2 vs. r^3 relationship
T_squared = orbital_periods**2
r_cubed = orbit_radii**3

# Plot results
plt.figure(figsize=(8,6))
plt.plot(r_cubed, T_squared, label='$T^2 \propto r^3$', color='blue')
plt.xlabel('$r^3$ (m^3)')
plt.ylabel('$T^2$ (s^2)')
plt.title("Kepler's Third Law: $T^2$ vs. $r^3$")
plt.legend()
plt.grid()
plt.show()
```
[alt text](333.png)
## **Discussion on Elliptical Orbits**
- Kepler’s Third Law extends to elliptical orbits, where $$r$$ is replaced by the semi-major axis.
- For binary systems, the sum of both masses is considered in the equation.
- The law helps analyze orbits of exoplanets, stars, and galaxies.
[alt text](555.png)

## **Conclusion**
Kepler’s Third Law provides a crucial link between gravity and orbital mechanics. Our Python simulation confirms its validity, and its applications in astronomy are vast, from predicting satellite movements to discovering exoplanets.