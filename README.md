# PID Self-Balancing Robot

A two-wheeled self-balancing robot that stays upright using a PID control loop on top of
**field-oriented control (FOC)** of two BLDC gimbal motors. A dedicated second ESP32 drives
a TFT display with animated eyes, giving the robot some personality while it balances. This
repo holds everything needed to understand, build, and recreate the project — the **code**,
the **CAD files**, the **wiring/hardware** details, and my **notes**.

![Robot photo](media/cover.jpg)
<!-- Drop a photo of the robot at media/cover.jpg and it will show up here -->

## What it does

The robot reads its tilt angle from an MPU-6050 IMU, compares it to the target (upright = 0°),
and a PID controller computes a torque command. That command is realized through **FOC** on
two GM4108H BLDC gimbal motors — each with an AS5047P magnetic encoder for accurate rotor
position — so the wheels apply smooth, precise torque to cancel the tilt, balancing the robot
like an inverted pendulum. A separate ESP32 runs an ILI9341 TFT display showing animated eyes.

## Repository layout

| Folder | What goes here |
|--------|----------------|
| [`code/`](code/) | Firmware / control code (Arduino, etc.) |
| [`cad/`](cad/) | 3D models and CAD source — chassis, mounts, brackets (STL + editable source) |
| [`hardware/`](hardware/) | Wiring diagrams, bill of materials, pin maps |
| [`docs/`](docs/) | Notes, PID tuning logs, design decisions, math |
| [`media/`](media/) | Photos and videos of the build |

## Hardware

**Compute**
- **2× ESP32 Dev Module** — one runs FOC motor control, one drives the eye display

**Motors + drivers**
- **2× GM4108H gimbal motor** — BLDC, 11 pole pairs, ~10 Ω/phase, one per wheel
- **2× DRV8313 driver** — 3-PWM mode, one per motor

**Sensing**
- **2× AS5047P magnetic encoder** — 14-bit SPI, shared SPI bus with separate CS lines
- **2× diametric magnet** — one on each motor shaft for the encoder
- **1× MPU-6050 IMU** — tilt/balance sensing, on I²C

**Power**
- **1× MP1584EN buck converter** — steps 12 V down to the logic rails
- **1× 12 V supply / battery** — main power for the motor drivers

**Display (eyes)**
- **1× ILI9341 TFT display** — animated eyes, driven by the second ESP32

- **Chassis:** 3D printed (see [`cad/`](cad/))

See [`hardware/bill-of-materials.md`](hardware/bill-of-materials.md) for the full parts list and pin map.

## Control: PID + FOC

The balance loop is PID; the motor layer is FOC.

**Balance (PID)** — runs on the IMU tilt angle:
```
error      = target_angle - measured_angle
integral  += error * dt
derivative = (error - last_error) / dt
torque_cmd = Kp*error + Ki*integral + Kd*derivative
```

**Motors (FOC)** — `torque_cmd` becomes the q-axis current target for each gimbal motor.
The AS5047P encoder gives rotor angle, so the DRV8313 can apply the right phase voltages
to produce smooth torque even at very low speeds — exactly what balancing needs.

Tuning `Kp`, `Ki`, `Kd` is most of the balance work — my tuning notes live in
[`docs/pid-tuning.md`](docs/pid-tuning.md).

## Build / upload

> 🚧 **Code is still in progress** — waiting on the motors to arrive. Once they're here and
> the robot is balancing, I'll upload the working code to [`code/`](code/).

There are two firmwares — one per ESP32.

1. Open the project in [`code/`](code/) with the Arduino IDE or PlatformIO.
2. Install libraries: **SimpleFOC** (motor control), the MPU-6050 IMU library, and the
   ILI9341 display library.
3. **Balance ESP32:** flash the FOC + balance firmware. Run encoder alignment / pole-pair
   calibration for each GM4108H first, then tune the PID gains.
4. **Eyes ESP32:** flash the display firmware for the ILI9341.

## License

Released under the [MIT License](LICENSE) — free to use, modify, and build on.
Attribution appreciated.

## Author

**Palden Bhutia** ([@pbhutia111](https://github.com/pbhutia111))
