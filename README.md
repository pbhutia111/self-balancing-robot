# PID Self-Balancing Robot

A two-wheeled self-balancing robot that stays upright using a PID control loop driven by
an IMU (accelerometer + gyroscope). This repo holds everything needed to understand,
build, and recreate the project — the **code**, the **CAD files**, the **wiring/hardware**
details, and my **notes**.

![Robot photo](media/cover.jpg)
<!-- Drop a photo of the robot at media/cover.jpg and it will show up here -->

## What it does

The robot reads its tilt angle from an IMU, compares it to the target (upright = 0°), and
the PID controller computes a motor response that drives the wheels to cancel the tilt —
balancing it like an inverted pendulum.

## Repository layout

| Folder | What goes here |
|--------|----------------|
| [`code/`](code/) | Firmware / control code (Arduino, etc.) |
| [`cad/`](cad/) | 3D models and CAD source — chassis, mounts, brackets (STL + editable source) |
| [`hardware/`](hardware/) | Wiring diagrams, bill of materials, pin maps |
| [`docs/`](docs/) | Notes, PID tuning logs, design decisions, math |
| [`media/`](media/) | Photos and videos of the build |

## Hardware (fill in your actual parts)

- **Microcontroller:** _e.g. Arduino Uno / ESP32_
- **IMU:** _e.g. MPU-6050_
- **Motors:** _e.g. 2× N20 geared DC motors / NEMA-17 steppers_
- **Motor driver:** _e.g. L298N / TB6612FNG_
- **Power:** _e.g. 2S LiPo / 18650 cells_
- **Chassis:** 3D printed (see [`cad/`](cad/))

See [`hardware/bill-of-materials.md`](hardware/bill-of-materials.md) for the full parts list.

## PID control, briefly

```
error      = target_angle - measured_angle
integral  += error * dt
derivative = (error - last_error) / dt
output     = Kp*error + Ki*integral + Kd*derivative
```

`output` is sent to the motors. Tuning `Kp`, `Ki`, `Kd` is most of the work — my tuning
notes live in [`docs/pid-tuning.md`](docs/pid-tuning.md).

## Build / upload

1. Open the sketch in [`code/`](code/) with the Arduino IDE (or PlatformIO).
2. Install the IMU library (e.g. the MPU-6050 library).
3. Select your board + port and upload.
4. Calibrate the IMU, then tune the PID gains.

## License

Released under the [MIT License](LICENSE) — free to use, modify, and build on.
Attribution appreciated.

## Author

**Palden Bhutia** ([@pbhutia111](https://github.com/pbhutia111))
