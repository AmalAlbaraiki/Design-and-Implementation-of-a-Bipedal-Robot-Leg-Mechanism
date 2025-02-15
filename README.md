# Design-and-Implementation-of-a-Bipedal-Robot-Leg-Mechanism


1. Introduction

Bipedal locomotion in humanoid robots presents significant 
challenges, including balance control, precise joint coordination, and efficient gait cycles. 

This report outlines a structured approach to designing and implementing a robotic leg system capable of achieving stable walking motion.

2. Input Parameters

Before implementing the walking algorithm, key parameters must be defined:

- Leg Dimensions:

  - \( L_1 \) = Thigh length (Hip to Knee)

  - \( L_2 \) = Shin length (Knee to Ankle)

  - \( L_3 \) = Foot height (Ankle to Ground)

- Joint Angles:Hip, Knee, and Ankle angles

- Walking Speed \( V_{step} \)

- Step Length \( L_{step} \)

- Step Time \( T_{step} \)

- Sensors: IMU (Inertial Measurement Unit), Encoders

- Actuators:Servo Motors or DC Motors with Encoders

3. Forward Kinematics Calculation

To determine the final position of the foot based on joint angles:

\[
X = L_1 \cos(\theta_{hip}) + L_2 \cos(\theta_{hip} + \theta_{knee})
\]

\[
Y = L_1 \sin(\theta_{hip}) + L_2 \sin(\theta_{hip} + \theta_{knee})
\]

4. Inverse Kinematics Calculation

Given the desired foot position \( (X_d, Y_d) \), the required joint angles are computed:

\[
\theta_{knee} = \cos^{-1} \left( \frac{X_d^2 + Y_d^2 - L_1^2 - L_2^2}{2 L_1 L_2} \right)

\]

\[
\theta_{hip} = \tan^{-1} \left( \frac{Y_d}{X_d} \right) - \tan^{-1} \left(

 \frac{L_2 \sin(\theta_{knee})}{L_1 + L_2 \cos(\theta_{knee})} \right)
\]

5. Stability Control and Zero Moment Point (ZMP) Adjustment

For stable walking, the center of mass (CoM) should remain above the supporting foot. 

The robot’s tilt angle is monitored using the IMU, and corrective actions are applied if necessary:

\[
\theta_{hip} = \theta_{hip} - K_p (\theta_{tilt} - \theta_{setpoint})
\]

where \( K_p \) is a proportional control constant for tilt correction.

6. Gait Cycle Execution

6.1 Stance Phase

- One foot remains on the ground, supporting the body’s weight.

- The CoM shifts above the supporting foot.

- The torso leans toward the supporting leg to maintain balance.

6.2 Swing Phase

- The opposite foot lifts off the ground, bending the knee by  30° - 45°.

- The leg moves forward by \( L_{step} \).

- The knee extends as the foot touches the ground.

7. IMU-Based Balance Adjustment

1. The IMU continuously measures tilt angles.

2. If deviation exceeds a predefined threshold, corrective 
movements are applied.

3. If imbalance occurs, the body weight is redistributed to the supporting foot.

8. PID Control for Motor Optimization

To ensure smooth motor movement and reduce oscillations, a PID controller is implemented:

\[
output = K_p \times error + K_i \times \sum error + K_d \times \frac{d(error)}{dt}
\]

where:
- \( K_p \): Proportional gain (controls immediate response)

- \( K_i \): Integral gain (corrects accumulated errors)

- \( K_d \): Derivative gain (reduces oscillations)

9. Conclusion

The proposed algorithm ensures that the bipedal robot achieves a stable and balanced walking motion.

- Forward and inverse kinematics accurately determine foot 
placement.

- ZMP stability control prevents tipping.

- PID-based motor control minimizes oscillations.

- Real-time IMU feedback enhances balance adjustments.

By integrating these components, the robot is capable of smooth, realistic walking without excessive tilt or instability.

