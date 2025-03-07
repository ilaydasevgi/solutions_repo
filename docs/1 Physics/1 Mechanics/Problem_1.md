# Problem 1
```markdown
# **Projectile Motion Analysis**

## **1. Theoretical Foundation**
Projectile motion follows Newton's laws, with motion governed by:

- Horizontal displacement: $$ x = v_0 \cos(\theta) t $$
- Vertical displacement: $$ y = v_0 \sin(\theta) t - \frac{1}{2} g t^2 $$

Solving for time of flight, $$ t_f $$, we get:
$$
    t_f = \frac{2 v_0 \sin(\theta)}{g}
$$

Using $$ t_f $$ in the horizontal equation, the range (R) is:
$$
    R = \frac{v_0^2 \sin(2\theta)}{g}
$$

## **2. Analysis of the Range**
- The range depends on the angle $$ \theta $$, initial velocity $$ v_0 $$, and gravity $$ g $$.
- Theoretical maximum range occurs at $$ \theta = 45^\circ $$.

## **3. Practical Applications**
- Sports (e.g., soccer, basketball)
- Engineering (e.g., artillery, rockets)
- Astrophysics (e.g., space launch trajectories)

## **4. Implementation**

### **Python Simulation**
$$
\text{import numpy as np} \\
\text{import matplotlib.pyplot as plt} \\

\text{def projectile\_motion(\theta, v0, g=9.81):} \\
\quad \theta_{rad} = \text{np.radians}(\theta) \\
\quad R = \frac{v_0^2 \sin(2 \theta_{rad})}{g} \\
\quad \text{return R} \\

\text{def plot\_range\_vs\_angle(v0, g=9.81):} \\
\quad \text{angles} = \text{np.linspace}(0, 90, 100) \\
\quad \text{ranges} = [\text{projectile\_motion}(\theta, v0, g) \text{ for } \theta \text{ in angles}] \\

\quad \text{plt.figure(figsize=(8, 5))} \\
\quad \text{plt.plot(angles, ranges, label=f'v0 = {v0} m/s')} \\
\quad \text{plt.xlabel('Angle of Projection (degrees)')} \\
\quad \text{plt.ylabel('Range (m)')} \\
\quad \text{plt.title('Projectile Range vs Angle of Projection')} \\
\quad \text{plt.legend()} \\
\quad \text{plt.grid()} \\
\quad \text{plt.show()} \\

\text{# Example usage} \\
\text{plot\_range\_vs\_angle(v0=20)} 
$$

### **Graphical Representation**
This script visualizes the range of a projectile as a function of projection angle.

## **5. Limitations and Extensions**
- **Limitations:** Ignores air resistance, wind, and terrain variations.
- **Improvements:** Add drag forces, different launch heights, or varying gravitational fields.
```

