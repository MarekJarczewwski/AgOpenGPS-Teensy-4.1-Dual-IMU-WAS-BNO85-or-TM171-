📦 Hardware
Required

Teensy 4.1

2x IMU:

BNO85 (RVC mode)
OR

TM171 (UART)

Serial Ports (default)
Device	Port
Chassis IMU	Serial5
Knuckle IMU	Serial3
⚙️ Configuration
1️⃣ Set steering sensitivity (CPD)

In AOG:

Steer Sensor Counts

Range internally scaled 70%–130%.

2️⃣ Drift calibration (optional)

Inside code:

const float CH_DRIFT_LEFT_360  = -2.1f;
const float CH_DRIFT_RIGHT_360 = -2.1f;

const float KN_DRIFT_LEFT_360  = 0.1f;
const float KN_DRIFT_RIGHT_360 = 0.1f;

Measure full 360° rotation error and adjust.

3️⃣ Auto-zero parameters
AUTOZERO_SPEED_MIN
AUTOZERO_YAWRATE_MAX
AUTOZERO_DELTA_MAX
AUTOZERO_TIME_MS
AUTOZERO_BETA

Defaults are stable for most tractors.

📡 UDP Output

PGN 253 – Steering angle

PGN 250 – Sensor values

Compatible with standard AOG UDP Autosteer

🛠 Installation

Open in Arduino IDE

Select:

Board: Teensy 4.1

USB Type: Serial + Ethernet

Compile & upload

Configure AOG

Set zero steering in AOG

⚠ Important Notes

Ensure correct IMU orientation.

Knuckle IMU must rotate strictly with steering axis.

Mount rigidly.

Use shielded wiring for UART if long runs.

🤝 Community

This implementation was developed and refined through practical field testing.

Feel free to fork, improve, and share results.

If you test this on your machine, please share:

Tractor model

IMU type

Drift values

Field results

The version of the file with the test ending is improved with frame synchronization, which reduces angle differences during fast turns, and an experimental improvement in handling over bumps.

I've devised a method that solves the problem of suspended cabs rocking sideways when a wheel hits a pothole. Using a sensor mounted as a WAS on the steering knuckle, you can detect the bump in advance, using the front wheel as a bump scanner before the rear wheel hits the pothole. Anticipating the bump, you can freeze the setpoint momentarily to prevent a sudden swing.

I've already implemented this in the code; you just need to manually select the parameters for your tractor and enter them into the code, such as the distance between the front and rear wheels, the freeze time, and the bump detection thresholds.


Of course, the code also states that it only works when driving straight and is inactive when the wheels are turned so as not to block the steering when cornering.




📜 License

Open-source for AgOpenGPS community use.
