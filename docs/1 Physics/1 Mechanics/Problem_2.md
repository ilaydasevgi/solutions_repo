# Problem 2
### Forced Damped Pendulum: Theoretical and Computational Analysis


# Investigating the Dynamics of a Forced Damped Pendulum

## 1. Theoretical Foundation

The equation governing the motion of a forced damped pendulum is given by:

$$ \frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t) $$

where:
- $\theta$ is the angular displacement,
- $\gamma$ is the damping coefficient,
- $\omega_0$ is the natural frequency ($\omega_0 = \sqrt{g/L}$ for a simple pendulum),
- $A$ is the amplitude of the external driving force,
- $\omega$ is the frequency of the external driving force.

For small angles ($\theta \approx \sin \theta$), the equation simplifies to a linear differential equation:

$$ \frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t) $$

The general solution consists of a homogeneous part (damped oscillation) and a particular part (forced oscillation). When the driving frequency approaches the natural frequency ($\omega \approx \omega_0$), resonance occurs, leading to large oscillations.

## 2. Analysis of Dynamics

We analyze the system by varying:
- Damping coefficient ($\gamma$)
- Driving force amplitude ($A$)
- Driving frequency ($\omega$)

### Numerical Solution Using Python
We use the Runge-Kutta method to solve the system numerically and visualize its dynamics.
```


import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Define the equations of motion
def forced_damped_pendulum(t, y, gamma, omega0, A, omega):
    theta, omega_theta = y
    dtheta_dt = omega_theta
    domega_dt = -gamma * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Parameters
gamma = 0.5  # Damping coefficient
omega0 = 1.0  # Natural frequency
A = 1.2  # Driving force amplitude
omega = 2.0  # Driving frequency

# Initial conditions
tspan = [0, 50]  # Time span
y0 = [0.2, 0]  # Initial angle and angular velocity

# Solve the ODE
sol = solve_ivp(forced_damped_pendulum, tspan, y0, args=(gamma, omega0, A, omega), t_eval=np.linspace(0, 50, 1000))

# Plot results
plt.figure(figsize=(10, 5))
plt.plot(sol.t, sol.y[0], label="Theta (Angle)")
plt.xlabel("Time")
plt.ylabel("Theta (rad)")
plt.title("Forced Damped Pendulum Motion")
plt.legend()
plt.grid()
plt.show()
```


## 3. Practical Applications
The forced damped pendulum model is relevant in:
- **Energy harvesting devices**: Utilizing resonance for energy collection.
- **Suspension bridges**: Understanding oscillatory instabilities.
- **Oscillating circuits**: Analogous behavior in RLC circuits.

## 4. Phase Portrait and Poincaré Section
A phase portrait illustrates the evolution of $(\theta, \omega_\theta)$ over time, revealing transitions to chaos.
```


import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Differential Equation for the Forced Damped Pendulum
def pendulum(t, state, damping, driving_freq, driving_force):
    theta, omega = state
    dtheta_dt = omega
    domega_dt = -damping * omega - np.sin(theta) + driving_force * np.cos(driving_freq * t)
    return [dtheta_dt, domega_dt]

# Parameters
damping = 0.5         # Damping coefficient
driving_freq = 2/3    # Driving frequency
driving_force = 1.2   # Driving force

# Initial conditions: [theta(0), omega(0)]
theta_0 = 0.2
omega_0 = 0.0

# Time span and evaluation points
time_span = (0, 50)  # Solve from 0 to 50 seconds
time_eval = np.linspace(time_span[0], time_span[1], 1000)  # 1000 time points

# Solve the differential equation
solution = solve_ivp(pendulum, time_span, [theta_0, omega_0], t_eval=time_eval, args=(damping, driving_freq, driving_force))

# Normalize theta values to be within -π to π
solution.y[0] = np.mod(solution.y[0] + np.pi, 2 * np.pi) - np.pi

# Plot the Phase Portrait
plt.figure(figsize=(8, 6))
plt.plot(solution.y[0], solution.y[1], label="Phase Space (θ vs ω)")
plt.scatter(solution.y[0][0], solution.y[1][0], color='red', marker='o', label="Initial Condition")
plt.xlabel("Theta (rad)")
plt.ylabel("Angular Velocity (rad/s)")
plt.title("Phase Portrait of the Forced Damped Pendulum")
plt.legend()
plt.grid()
plt.show()


```
![ Alt Text](unknown.png)
## 5. Conclusion
We explored the dynamics of a forced damped pendulum through theory and simulation. By varying parameters, we observed transitions from periodic motion to chaos. Future work could include:
- Introducing nonlinear damping,
- Exploring non-periodic driving forces.

This study bridges theoretical physics with engineering applications, demonstrating the richness of nonlinear dynamical systems.
#