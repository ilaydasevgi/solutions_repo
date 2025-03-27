#  Problem 1
# : Investigating the Range as a Function of the Angle of Projection

---

##  Motivation

Projectile motion is one of the most fundamental topics in classical mechanics. Despite its apparent simplicity, it provides a deep insight into the laws of motion and the effects of initial conditions on trajectory.

The central question here is:

> "How does the **range** (horizontal distance traveled) of a projectile depend on the **angle** at which it is launched?"

By investigating this, we uncover the elegant symmetry in projectile motion and how various physical parameters influence the outcome.

---

##  1. Theoretical Foundation

We begin with the ideal case of projectile motion:
- No air resistance
- Constant gravitational acceleration \( g \)
- Launch from ground level

Let:
- \( v_0 \): initial launch speed  
- \( \theta \): launch angle (in degrees or radians)  
- \( g \): gravitational acceleration  
- \( R \): horizontal range  
- \( T \): time of flight  
- \( h = 0 \): launch and landing at the same height

###  Equations of Motion

Horizontal motion (no acceleration):

$$
x(t) = v_0 \cos(\theta) \cdot t
$$

Vertical motion (accelerated):

$$
y(t) = v_0 \sin(\theta) \cdot t - \frac{1}{2} g t^2
$$

At \( y = 0 \), the projectile lands, giving total time of flight:

$$
T = \frac{2 v_0 \sin(\theta)}{g}
$$

Substitute into \( x(t) \) to find **range**:

###  Range Equation:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

This equation shows that:
- The range depends **sinusoidally** on the **angle**
- Maximum range occurs at \( \theta = 45^\circ \)
- It's symmetric around \( 45^\circ \) (e.g., \( 30^\circ \) and \( 60^\circ \) give same range)

---

##  2. Analysis of the Range

###  Effect of Varying Launch Angle:

From the formula:

$$
R(\theta) = \frac{v_0^2}{g} \cdot \sin(2\theta)
$$

We see that:
- \( R(\theta) = R(90^\circ - \theta) \)
- Maximum at \( \theta = 45^\circ \)

###  Effect of Initial Speed \( v_0 \):

Range increases **quadratically** with speed:

$$
R \propto v_0^2
$$

###  Effect of Gravity \( g \):

Range is **inversely** proportional to gravity:

$$
R \propto \frac{1}{g}
$$

Thus, on the Moon (where \( g \) is smaller), the range is longer for the same \( v_0 \).

---

##  3. Practical Applications

Real-world uses of projectile motion include:

- **Sports**: Basketball, soccer, archery (tuning angle for maximum distance)
- **Engineering**: Ballistics, cannon design
- **Space physics**: Lunar or Mars landings, estimating motion in low gravity

More advanced models include:
- Launching from an **elevated position**
- **Air resistance** (drag force)
- **Wind** or **spin effects**

---

##  4. Python Simulation: Range vs Angle

We now simulate how the **range changes with angle**, keeping other parameters constant.

### Constants:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravitational acceleration (m/s^2)
angles_deg = np.linspace(0, 90, 500)  # launch angles in degrees
angles_rad = np.radians(angles_deg)

# Function to compute range
def compute_range(v0, g, angles_rad):
    return (v0**2 * np.sin(2 * angles_rad)) / g

# Single v0 case
v0_single = 20  # m/s
range_single = compute_range(v0_single, g, angles_rad)

# Multiple v0s for comparison
v0_list = [10, 20, 30]
ranges_multiple = [compute_range(v, g, angles_rad) for v in v0_list]

# Plot: Single Range vs. Angle
plt.figure(figsize=(8, 5))
plt.plot(angles_deg, range_single, label=f'v0 = {v0_single} m/s', color='blue')
plt.axvline(45, color='red', linestyle='--', label='Max Range at 45°')
plt.title('Projectile Range vs. Launch Angle')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (meters)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

# Plot: Multiple Initial Velocities
plt.figure(figsize=(8, 5))
for i, v0 in enumerate(v0_list):
    plt.plot(angles_deg, ranges_multiple[i], label=f'v0 = {v0} m/s')
plt.title('Range vs. Angle for Different Launch Speeds')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (meters)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

