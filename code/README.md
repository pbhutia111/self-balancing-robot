# Code

Firmware / control code for the robot.

Drop your sketch here, e.g. `self_balancing_robot.ino`, plus any helper files or libraries.

## Structure suggestion
- `self_balancing_robot.ino` — main sketch (setup + loop, reads IMU, runs PID, drives motors)
- `config.h` — pin assignments and PID gains in one place
- `libraries/` — any custom/vendored libraries

## Notes
- IMU sample rate and loop timing matter for stable PID — keep the loop interval consistent.
- Keep `Kp`/`Ki`/`Kd` easy to change (top of file or `config.h`) while tuning.
