# Problem 1

# **Investigating the Range as a Function of the Angle of Projection**

## **1. Motivation**
Projectile motion, while seemingly simple, provides a rich foundation for understanding fundamental physics principles. The problem is straightforward: analyze how the range of a projectile depends on its angle of projection. However, beneath this simplicity lies a complex framework involving both linear and quadratic relationships.

This topic is particularly compelling due to the number of free parameters involved, such as:

- **Initial velocity** $v_0$

- **Gravitational acceleration** $g$

- **Launch height** $h$


These parameters give rise to a diverse set of solutions that describe real-world phenomena, from the arc of a soccer ball to the trajectory of a rocket.

---

## **2. Theoretical Foundation**
To analyze projectile motion, we derive the governing equations from fundamental principles, primarily Newton's second law of motion.

### **2.1. Equations of Motion**
Projectile motion is governed by Newton’s Second Law:

$F = m \cdot a$

For a projectile, forces acting on the object include:
1. **Gravity** ($mg$) in the vertical direction.
2. **No horizontal forces** (ignoring air resistance initially).

Thus, the acceleration components are:

$a_x = 0, \quad a_y = -g$

Integrating these equations, we obtain the velocity components:

$v_x = v_0 \cos(\theta), \quad v_y = v_0 \sin(\theta) - g t$

Further integration gives the position equations:

$x(t) = v_0 \cos(\theta) \cdot t$

$y(t) = v_0 \sin(\theta) \cdot t - \frac{1}{2} g t^2$

The horizontal and vertical motion of a projectile are governed by kinematic equations:

- **Horizontal motion (constant velocity):**

$$x(t) = v_0 \cos(\theta) t$$

- **Vertical motion (accelerated motion due to gravity):**

$$y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2$$


where:

- $x(t)$ and $y(t)$ are the projectile's position at time $t$.
- $v_0$ is the initial velocity.
-  $\theta$ is the launch angle.
- $g$ is the gravitational acceleration (typically 9.81 m/s² on Earth).


These fundamental equations describe projectile motion and will now be used to analyze range and time of flight.

---

### **2.2. Time of Flight**
The total time the projectile spends in the air can be determined by setting $y(t) = 0$:

$t_f = \frac{2 v_0 \sin(\theta)}{g}$

### **2.3. Range Equation**
The range $R$ is the total horizontal distance traveled before the projectile lands.
Using $t_f$ in the horizontal motion equation:

$R = v_0 \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g}$

Using the trigonometric identity $2\sin(\theta) \cos(\theta) = \sin(2\theta)$, we obtain:

$R(\theta) = \frac{v_0^2}{g} \sin(2\theta)$

### **2.4. Maximum Range**
The maximum range occurs when $\sin(2\theta)$ is maximized, which happens at $\theta = 45^\circ$:

$R_{max} = \frac{v_0^2}{g}$

---

## **3. Analysis of the Range**

### **3.1. Dependence on Angle**
- The range follows a **symmetrical** pattern around $\theta = 45^\circ$.
- Angles $\theta$ and $90^\circ - \theta$ result in the same range.

### **3.2. Effect of Initial Velocity**
- Higher $v_0$ leads to a longer range, proportional to $v_0^2$.

### **3.3. Effect of Gravity**
- A larger $g$ (such as on Jupiter) reduces range, while a smaller $g$ (such as on the Moon) increases it.


#### **📌 Improved Range Plot with Annotations**
```python
import numpy as np
import matplotlib.pyplot as plt

# Define parameters
v0 = 20  # Initial velocity (m/s)
g = 9.81  # Gravity (m/s^2)
theta = np.linspace(0, 90, 100)  # Angle range from 0 to 90 degrees

# Compute range
R = (v0**2 * np.sin(np.deg2rad(2 * theta))) / g

# Plot the range vs. angle
plt.figure(figsize=(10, 6))
plt.plot(theta, R, label='Range (R)', color='blue')

# Mark the maximum range at 45°
plt.axvline(45, color='red', linestyle='--', label='Max Range at 45°')
plt.text(46, max(R)-2, "Maximum Range", color='red')

plt.xlabel('Projection Angle (θ) [Degrees]')
plt.ylabel('Range (R) [m]')
plt.title('Projectile Range as a Function of Launch Angle')
plt.grid(True)
plt.legend()
plt.show()
```
![alt text](image-5.png)
### **4. Implementation: Python Visualization**
We implement a computational tool to visualize the range as a function of the angle.


## 🚀 Projectile Motion Simulation

This simulation demonstrates the **parabolic trajectory of a projectile** launched at a given angle and velocity.  
Users can **adjust the launch angle and initial speed**, allowing them to observe how different conditions affect projectile motion.

### 📌 **How It Works?**
- The user selects a **launch angle (0° - 90°) and initial velocity (5 - 50 m/s)**.
- Pressing the **"Start Simulation"** button runs the animation based on the selected values.
- A **moving particle (blue dot) follows a curved trajectory due to gravity**.
- The **graph dynamically updates** to show the horizontal and vertical motion.

### 🖥 **Use Cases**
✅ **Understanding projectile motion in physics courses.**  
✅ **Basic modeling for engineering and ballistic calculations.**  
✅ **Trajectory analysis for real-world problems.**  

🔗 **Run the Simulation on Google Colab:**  
[Link text](https://colab.research.google.com/drive/1U-gdNsOIBkSQR3tMoc0KqLe4vPOr5lib?usp=sharing
)
---

## **5. Air Resistance & Improved Models**
In reality, projectiles experience **air resistance** proportional to velocity:

$F_{drag} = - k v^2$

The equations of motion now become:

$a_x = -\frac{k}{m} v_x, \quad a_y = -g - \frac{k}{m} v_y$

### **📌 Visualization with Air Resistance**
```python
import numpy as np
import matplotlib.pyplot as plt
 
# Projectile parameters
v0 = 50  # Initial velocity (m/s)
angle = 45  # Launch angle (degrees)
g = 9.81  # Gravitational acceleration (m/s^2)
mass = 0.5  # Mass of the object (kg)
drag_coefficient = 0.1  # Air resistance coefficient (kg/m)
 
# Helper functions
def trajectory_no_air_resistance(v0, angle, g, t):
    angle_rad = np.radians(angle)
    x = v0 * np.cos(angle_rad) * t
    y = v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    return x, y
 
def trajectory_with_air_resistance(v0, angle, g, mass, drag_coefficient, dt=0.01):
    angle_rad = np.radians(angle)
    vx = v0 * np.cos(angle_rad)
    vy = v0 * np.sin(angle_rad)
    x, y = 0, 0
    x_positions, y_positions = [x], [y]
 
    while y >= 0:
        ax = -drag_coefficient * vx / mass
        ay = -g - (drag_coefficient * vy / mass)
        vx += ax * dt
        vy += ay * dt
        x += vx * dt
        y += vy * dt
        x_positions.append(x)
        y_positions.append(y)
 
    return x_positions, y_positions
 
# Simulation time for the case without air resistance
t_max = 2 * v0 * np.sin(np.radians(angle)) / g
t = np.linspace(0, t_max, num=500)
 
# Calculations
x_no_air, y_no_air = trajectory_no_air_resistance(v0, angle, g, t)
x_with_air, y_with_air = trajectory_with_air_resistance(v0, angle, g, mass, drag_coefficient)
 
# Plot
plt.figure(figsize=(10, 6))
plt.plot(x_no_air, y_no_air, label="Without air resistance", linestyle="--")
plt.plot(x_with_air, y_with_air, label="With air resistance", linestyle="-")
plt.title("Projectile motion: comparison with and without air resistance")
plt.xlabel("Distance (m)")
plt.ylabel("Height (m)")
plt.legend()
plt.grid()
plt.show()
```
![alt text](image-6.png)

 ## Projectile Motion with and Without Air Resistance (with Bouncing)

### 1️⃣ What Does This Code Do?

This Python script simulates and visualizes projectile motion with and without air resistance, including bounces off the ground. The animation shows how air resistance affects the motion of a projectile compared to the idealized case with no drag.

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
from IPython.display import HTML
 
# Parameters
m = 1.0  # Mass [kg]
g = 9.81  # Gravitational acceleration [m/s^2]
k = 0.1  # Air resistance coefficient [kg/s]
v0 = 20  # Initial velocity [m/s]
theta = np.radians(45)  # Initial angle [degrees -> radians]
dt = 0.02  # Time step [s]
T = 5  # Simulation time [s]
elasticity = 0.7  # Coefficient of restitution
 
# Function to calculate trajectory without air resistance
def trajectory_no_drag(v0, theta, g, dt, T, elasticity):
    x, y = [0], [0]
    vx, vy = v0 * np.cos(theta), v0 * np.sin(theta)
    t = 0
    while t < T:
        x.append(x[-1] + vx * dt)
        y_new = y[-1] + vy * dt - 0.5 * g * dt**2
        vy -= g * dt
        if y_new < 0:  # Bounce off the ground
            vy = -vy * elasticity
            y_new = 0
        y.append(y_new)
        t += dt
    return x, y
 
# Function to calculate trajectory with air resistance
def trajectory_with_drag(v0, theta, g, k, m, dt, T, elasticity):
    vx, vy = v0 * np.cos(theta), v0 * np.sin(theta)
    x, y = [0], [0]
    t = 0
    while t < T:
        ax = - (k / m) * vx
        ay = -g - (k / m) * vy
        vx += ax * dt
        vy += ay * dt
        x.append(x[-1] + vx * dt)
        y_new = y[-1] + vy * dt
        if y_new < 0:  # Bounce off the ground
            vy = -vy * elasticity
            y_new = 0
        y.append(y_new)
        t += dt
    return x, y
 
# Compute trajectories
x_no_drag, y_no_drag = trajectory_no_drag(v0, theta, g, dt, T, elasticity)
x_drag, y_drag = trajectory_with_drag(v0, theta, g, k, m, dt, T, elasticity)
 
# Initialize animation
fig, ax = plt.subplots(figsize=(8, 5))
ax.set_xlim(0, max(max(x_no_drag), max(x_drag)))
ax.set_ylim(0, max(max(y_no_drag), max(y_drag)))
ax.set_xlabel("Distance [m]")
ax.set_ylabel("Height [m]")
ax.set_title("Projectile motion with and without air resistance (with bounces)")
ax.grid()
 
point_no_drag, = ax.plot([], [], 'bo', label="Without air resistance")
point_drag, = ax.plot([], [], 'ro', label="With air resistance")
traj_no_drag, = ax.plot([], [], 'b--', alpha=0.5)
traj_drag, = ax.plot([], [], 'r--', alpha=0.5)
ax.legend()
 
# Initialization function
def init():
    point_no_drag.set_data([], [])
    point_drag.set_data([], [])
    traj_no_drag.set_data([], [])
    traj_drag.set_data([], [])
    return point_no_drag, point_drag, traj_no_drag, traj_drag
 
# Function to update the animation
def update(frame):
    if frame < len(x_no_drag):
        point_no_drag.set_data([x_no_drag[frame]], [y_no_drag[frame]])
        traj_no_drag.set_data(x_no_drag[:frame+1], y_no_drag[:frame+1])
 
    if frame < len(x_drag):
        point_drag.set_data([x_drag[frame]], [y_drag[frame]])
        traj_drag.set_data(x_drag[:frame+1], y_drag[:frame+1])
 
    return point_no_drag, point_drag, traj_no_drag, traj_drag
 
# Create animation
frames = max(len(x_no_drag), len(x_drag))
ani = FuncAnimation(fig, update, frames=frames, init_func=init, blit=False, interval=20)
 
# Display animation in Colab
plt.close()
HTML(ani.to_html5_video())
```
### Link To The Simulation Above On Google Colab
https://colab.research.google.com/drive/1JAPKrMDEgJBFYaxuZgfnd50JqxAKGi-t?usp=sharing



---

## **7. Conclusion**
- The range equation follows a clear mathematical pattern.
- Maximum range occurs at **45°**, confirmed analytically and numerically.
- **Including air resistance shows a significant reduction in range**.
- This study has applications in sports, engineering, and physics simulations.

---

## **8. References & Further Reading**
- Resnick, R., & Halliday, D. (2004). *Fundamentals of Physics*.
- MIT OpenCourseWare: Classical Mechanics Lectures.
- NASA’s trajectory analysis for spacecraft launches.
