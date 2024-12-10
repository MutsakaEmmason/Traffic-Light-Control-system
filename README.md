# Traffic-Light-Control-system.
A microcontroller-based traffic light control system using four Arduino boards, designed to handle a single-direction road. The project features pedestrian crossing control, obstacle detection using an ultrasonic sensor, and dynamic light adjustments, implemented with direct register manipulation.

Features

Traffic Light Control: Red, Yellow, and Green LEDs cycle with default timings.

Pedestrian Crossing: Push button triggers an interrupt to ensure safe crossing.

Obstacle Detection: Ultrasonic sensor monitors road width for obstacles.

Dynamic Backtracking: Adjusts light sequence based on pedestrian or obstacle presence.

EEPROM Integration: Stores and retrieves road width data.

Direct Register Manipulation: Utilizes ADC, GPIOs, interrupts, counters, timers, and serial communication without standard Arduino libraries.

Serial Logging: Logs state changes and events for monitoring.

Hardware Requirements

Arduino Uno (4 boards)

Red, Yellow, Green LEDs (3 per board, with resistors)

Push Button (with debounce circuitry)

Ultrasonic Sensor (e.g., HC-SR04)

Resistors (220Ω for LEDs)

Breadboards and Jumper Wires

Pin Connections

Board 1 (Master Controller)

LEDs:

Red LED: Pin 3

Yellow LED: Pin 4

Green LED: Pin 5

Serial Communication:

TX: Pin 1

RX: Pin 0

Board 2 (Push Button)

Push Button:

Button Pin: Pin 2

Serial Communication:

TX: Pin 1

RX: Pin 0

Board 3 (Ultrasonic Sensor)

Ultrasonic Sensor:

Trigger Pin: Pin 7

Echo Pin: Pin 6

Serial Communication:

TX: Pin 1

RX: Pin 0

Board 4 (EEPROM Manager)

Serial Communication:

TX: Pin 1

RX: Pin 0

Software Requirements

Arduino IDE (Version 1.8.0 or later)

Serial Monitor (for debugging and monitoring)

Connect Hardware:

Assemble the circuit according to the pin connections mentioned above.

How It Works

Default Operation:

The traffic light cycles through Red (10s), Yellow (5s), and Green (10s).

Pedestrian Crossing:

When the push button is pressed, the lights backtrack to Red to allow safe crossing.

Red light stays on for 10 seconds.

Obstacle Detection:

The ultrasonic sensor monitors the road width (default: 20 cm).

If an obstacle is detected, the red light stays on until the obstacle is cleared.

Serial Monitoring:

Logs state changes and commands from the master controller.

Serial Monitor Outputs

Board 1 (Master):

R: Red LED On

Y: Yellow LED On

G: Green LED On

Board 2 (Ultrasonic):

O: Obstacle detected

C: Clear road

Board 3 (Button):

PRESSED: Button press detected

Board 4 (EEPROM):

WIDTH:20: Current road width (from EEPROM)

WIDTH UPDATED: New width saved

Project Structure

traffic-light-control/
├── board1_master.ino    # Code for Board 1
├──board2_ultrasonic.ino  # Code for Board 2
├──board3_button.ino  # Code for Board 3
├── board4_eeprom.ino    # Code for Board 4
└── README.md            # Documentation

Future Improvements

Expand to multi-directional traffic control.

Add real-time clock (RTC) for advanced scheduling.

Integrate IoT for remote monitoring.


