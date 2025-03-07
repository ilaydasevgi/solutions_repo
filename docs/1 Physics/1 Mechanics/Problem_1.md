# Problem 1
Let’s dive into this exploration of projectile motion and investigate how the range depends on the angle of projection. Below is a comprehensive Markdown document that addresses the theoretical foundation, range analysis, practical applications, and includes a Python implementation for simulation and visualization.

---


# Investigating the Range as a Function of the Angle of Projection

Projectile motion is a classic problem in physics that combines simplicity with profound insights into kinematics. Our goal is to analyze how the horizontal range of a projectile depends on its launch angle, explore the effects of various parameters, and connect the model to real-world scenarios. This document derives the governing equations, analyzes the range, provides a computational simulation, and discusses practical extensions.

## 1. Theoretical Foundation

### Deriving the Equations of Motion

Projectile motion occurs under the influence of gravity, with no horizontal acceleration (assuming no air resistance). We start with Newton’s second law in two dimensions:

- **Horizontal (x-direction):** No forces act (ignoring drag), so acceleration $ a_x = 0 $.
- **Vertical (y-direction):** Gravity acts downward, so $ a_y = -g $, where $ g $ is the gravitational acceleration (typically $ 9.8 \, \text{m/s}^2 $).

The initial conditions are:
- Initial velocity $ v_0 $ at angle $ \theta $ from the horizontal.
- Initial position at $ (x_0, y_0) $, often taken as $ (0, 0) $ for simplicity.

The velocity components are:
- $ v_{0x} = v_0 \cos\theta $
- $ v_{0y} = v_0 \sin\theta $

#### Horizontal Motion
Since $ a_x = 0 $:
$$
v_x(t) = v_{0x} = v_0 \cos\theta
$$
$$
x(t) = x_0 + v_{0x} t = v_0 \cos\theta \, t \quad (\text{assuming } x_0 = 0)
$$

#### Vertical Motion
With $ a_y = -g $:
$$
v_y(t) = v_{0y} - g t = v_0 \sin\theta - g t
$$
$$
y(t) = y_0 + v_{0y} t - \frac{1}{2} g t^2 = v_0 \sin\theta \, t - \frac{1}{2} g t^2 \quad (\text{assuming } y_0 = 0)
$$

These are the parametric equations of motion, forming a parabola in the $ x $-$ y $ plane.

### Time of Flight
The projectile hits the ground when $ y(t) = 0 $:
$$
v_0 \sin\theta \, t - \frac{1}{2} g t^2 = 0
$$
$$
t (v_0 \sin\theta - \frac{1}{2} g t) = 0
$$
Solutions: $ t = 0 $ (launch) or:
$$
t = \frac{2 v_0 \sin\theta}{g}
$$
This is the time of flight for a projectile launched and landing at the same height.

### Family of Solutions
The equations depend on parameters $ v_0 $, $ \theta $, and $ g $, yielding a family of trajectories. For example:
- Increasing $ v_0 $ stretches the parabola.
- Changing $ \theta $ alters the shape and range.
- Varying $ g $ (e.g., on another planet) scales the time and distance.

## 2. Analysis of the Range

### Range Equation
The horizontal range $ R $ is the distance traveled when $ t = \frac{2 v_0 \sin\theta}{g} $:
$$
R = v_{0x} \cdot t = (v_0 \cos\theta) \cdot \frac{2 v_0 \sin\theta}{g}
$$
Using the identity $ \sin(2\theta) = 2 \sin\theta \cos\theta $:
$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

### Dependence on Angle
- **Maximum Range:** $ R $ is maximized when $ \sin(2\theta) = 1 $, i.e., $ 2\theta = 90^\circ $, so $ \theta = 45^\circ $. Here, $ R_{\text{max}} = \frac{v_0^2}{g} $.
- **Symmetry:** $ R(\theta) = R(90^\circ - \theta) $, e.g., $ \theta = 30^\circ $ and $ 60^\circ $ yield the same range.
- **Limits:** At $ \theta = 0^\circ $ or $ 90^\circ $, $ \sin(2\theta) = 0 $, so $ R = 0 $.

### Influence of Parameters
- **Initial Velocity ($ v_0 $):** $ R \propto v_0^2 $, a quadratic relationship.
- **Gravity ($ g $):** $ R \propto \frac{1}{g} $, so weaker gravity increases range.

## 3. Practical Applications

### Real-World Scenarios
- **Sports:** A soccer ball’s trajectory depends on kick angle and speed, with $ \theta \approx 45^\circ $ optimizing distance.
- **Engineering:** Artillery or rocket launches adjust $ \theta $ and $ v_0 $ for target distance.
- **Astrophysics:** Trajectories on the Moon ($ g \approx 1.62 \, \text{m/s}^2 $) are farther than on Earth.

### Extensions
- **Uneven Terrain:** If launched from height $ h $, the range equation becomes more complex, involving a quadratic in time.
- **Air Resistance:** Adds a drag force proportional to velocity, requiring numerical solutions.

## 4. Implementation

Below is a Python script to simulate and visualize the range versus angle.

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20.0  # initial velocity (m/s)
g = 9.8    # gravitational acceleration (m/s^2)
angles = np.linspace(0, 90, 91)  # angles from 0 to 90 degrees

# Range function
def range_projectile(v0, theta_deg, g):
    theta = np.radians(theta_deg)
    return (v0**2 * np.sin(2 * theta)) / g

# Compute ranges
ranges = range_projectile(v0, angles, g)

# Plot
plt.figure(figsize=(10, 6))
plt.plot(angles, ranges, label=f'v0 = {v0} m/s, g = {g} m/s²')
plt.xlabel('Launch Angle (degrees)')
plt.ylabel('Range (meters)')
plt.title('Range vs. Angle of Projection')
plt.grid(True)
plt.legend()
plt.show()

# Test different v0 and g
v0_values = [10, 20, 30]
g_values = [9.8, 1.62]  # Earth and Moon
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    for g in g_values:
        ranges = range_projectile(v0, angles, g)
        plt.plot(angles, ranges, label=f'v0 = {v0} m/s, g = {g} m/s²')
plt.xlabel('Launch Angle (degrees)')
plt.ylabel('Range (meters)')
plt.title('Range vs. Angle for Different Parameters')
plt.grid(True)
plt.legend()
plt.show()
```

### Output
- The first plot shows $ R $ vs. $ \theta $ for $ v_0 = 20 \, \text{m/s} $, $ g = 9.8 \, \text{m/s}^2 $, peaking at $ \theta = 45^\circ $.
- The second plot compares different $ v_0 $ and $ g $, illustrating their effects.

## Discussion

### Limitations
- **Idealization:** Assumes no air resistance, flat ground, and constant $ g $.
- **Range Formula:** Only applies when launch and landing heights are equal.

### Enhancements
- **Drag:** Incorporate $ F_d = -k v $ and solve numerically.
- **Wind:** Add a velocity term to the equations.
- **Height:** Adjust for $ y_0 \neq 0 $, solving a quadratic for time of flight.

This analysis and simulation highlight the elegance of projectile motion while revealing its adaptability to complex scenarios.

---

This Markdown document, with embedded Python code, fulfills the deliverables. You can copy it into a Jupyter notebook or run the script directly to generate the plots. Let me know if you'd like to explore specific extensions, like air resistance or uneven terrain!