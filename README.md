# PID Controller Simulator

An interactive, web-based PID controller simulator with real-time step response visualization, auto-tuning, and performance metrics analysis.

![PID Controller Simulator](screenshot.png)

## Features

- **Plant Selection** — Choose between First-Order and Second-Order systems
  - 1st Order: G(s) = K / (τs + 1) with adjustable gain K and time constant τ
  - 2nd Order: G(s) = ωn² / (s² + 2ζωns + ωn²) with adjustable natural frequency ωn and damping ratio ζ
- **PID Tuning Sliders** — Real-time adjustment of Kp, Ki, Kd with instant graph updates
- **Auto-Tune** — Ziegler-Nichols method for automatic PID parameter calculation
- **Step Response Plot** — Real-time Recharts visualization showing setpoint and plant output
- **Error Signal Plot** — Separate error tracking graph
- **Performance Metrics:**
  - Rise Time (10-90%)
  - Percentage Overshoot
  - Settling Time (2% band)
  - Steady-State Error
- **Anti-Windup** — Integral clamping to prevent windup saturation
- **Transfer Function Display** — Live formula with current parameter values

## How to Use

1. Open `index.html` in any modern web browser
2. Select a plant type (1st or 2nd order)
3. Adjust plant parameters using the sliders
4. Tune PID gains manually or click **Auto-Tune**
5. Observe the step response and performance metrics update in real-time

## Tech Stack

- **React 18** — UI framework
- **Recharts** — Charting library for step response and error plots
- **Babel** — JSX transformation
- **CSS** — Custom dark theme styling

## Simulation Details

- Discrete-time PID with configurable time step (dt = 0.005s)
- Euler integration for plant dynamics
- State-space representation for 2nd order systems
- Metrics calculated by analyzing simulated output data array
- Auto-tuning uses Ziegler-Nichols open-loop (1st order) and ultimate gain (2nd order) methods
