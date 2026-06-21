# Bill of Materials (BOM)

Fill in the actual parts you used, with links where helpful.

| Qty | Part | Spec / Model | Notes / Link |
|-----|------|--------------|--------------|
| 1 | Microcontroller | _Arduino Uno / ESP32_ | |
| 1 | IMU | _MPU-6050_ | accel + gyro |
| 1 | Motor driver | _L298N / TB6612FNG_ | |
| 2 | Motors | _N20 geared DC / NEMA-17_ | |
| 2 | Wheels | | |
| 1 | Battery | _2S LiPo / 2× 18650_ | |
| - | Frame | 3D printed | see ../cad |
| - | Wires, headers, screws | | |

## Wiring / pin map

| Signal | MCU pin | Connects to |
|--------|---------|-------------|
| IMU SDA | | MPU-6050 SDA |
| IMU SCL | | MPU-6050 SCL |
| Motor A IN1 | | driver IN1 |
| Motor A IN2 | | driver IN2 |
| Motor B IN3 | | driver IN3 |
| Motor B IN4 | | driver IN4 |

Add a wiring diagram image here (e.g. `wiring.png`) once you have one.
