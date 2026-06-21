# PID Tuning Notes

A running log of how I tuned the controller. Record what you tried so you (and others) can
reproduce it.

## Method
1. Set `Ki = 0` and `Kd = 0`. Raise `Kp` until the robot reacts to tilt and oscillates
   slightly around upright.
2. Add `Kd` to damp the oscillation — the robot should settle instead of wobbling.
3. Add a small `Ki` to remove steady-state lean/drift. Keep it small to avoid windup.
4. Iterate.

## Log

| Date | Kp | Ki | Kd | Result |
|------|----|----|----|--------|
| _yyyy-mm-dd_ | _0_ | _0_ | _0_ | _what happened_ |

## Gotchas
- **Integral windup:** clamp the integral term or it overshoots after a big disturbance.
- **Loop timing:** an inconsistent `dt` makes Kd/Ki behave unpredictably.
- **IMU noise/drift:** use a complementary or Kalman filter to fuse accel + gyro.
