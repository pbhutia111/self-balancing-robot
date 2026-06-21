# Bill of Materials (BOM)

### Compute
| Component | Qty | Notes |
|-----------|-----|-------|
| ESP32 Dev Module | 2 | One runs FOC motor control, one drives the eye display |

### Motors + drivers
| Component | Qty | Notes |
|-----------|-----|-------|
| GM4108H gimbal motor | 2 | 11 pole pairs, BLDC, ~10 Ω/phase, one per wheel |
| DRV8313 driver | 2 | 3-PWM mode, one per motor |

### Sensing
| Component | Qty | Notes |
|-----------|-----|-------|
| AS5047P magnetic encoder | 2 | 14-bit SPI, one per motor — shared SPI bus, separate CS lines |
| Diametric magnet | 2 | One on each motor shaft for the encoder |
| MPU-6050 IMU | 1 | Tilt/balance sensing, on I²C |

### Power
| Component | Qty | Notes |
|-----------|-----|-------|
| MP1584EN buck converter | 1 | Steps 12 V down to logic rails |
| 12 V supply / battery | 1 | Main power for the motor drivers |

### Display (eyes)
| Component | Qty | Notes |
|-----------|-----|-------|
| ILI9341 TFT display | 1 | Animated eyes, driven by the second ESP32 |

### Frame
| Component | Qty | Notes |
|-----------|-----|-------|
| 3D-printed chassis | 1 | See [../cad](../cad) — Head, Arm support, motor cover, outside cover |
| Wheels, screws, standoffs, wiring | — | |

## Wiring / pin map

Fill in the actual ESP32 pins you used.

### Balance ESP32 — motors (FOC)
| Signal | ESP32 pin | Connects to |
|--------|-----------|-------------|
| Motor A PWM (3×) | | DRV8313 #1 IN1/IN2/IN3 |
| Motor A enable | | DRV8313 #1 nSLEEP/EN |
| Motor B PWM (3×) | | DRV8313 #2 IN1/IN2/IN3 |
| Motor B enable | | DRV8313 #2 nSLEEP/EN |
| Encoder SPI SCK | | AS5047P SCK (shared) |
| Encoder SPI MISO | | AS5047P MISO (shared) |
| Encoder SPI MOSI | | AS5047P MOSI (shared) |
| Encoder A CS | | AS5047P #1 CSn |
| Encoder B CS | | AS5047P #2 CSn |
| IMU SDA | | MPU-6050 SDA (I²C) |
| IMU SCL | | MPU-6050 SCL (I²C) |

### Eyes ESP32 — display
| Signal | ESP32 pin | Connects to |
|--------|-----------|-------------|
| TFT SCK | | ILI9341 SCK |
| TFT MOSI | | ILI9341 MOSI |
| TFT CS | | ILI9341 CS |
| TFT DC | | ILI9341 DC |
| TFT RST | | ILI9341 RST |

Add a wiring diagram image here (e.g. `wiring.png`) once you have one.
