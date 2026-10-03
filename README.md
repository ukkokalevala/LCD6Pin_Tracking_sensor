Line Tracking Sensor with LCD Display – Project Description
Overview
This project uses an Arduino Nano to read a line-tracking sensor and display its status on a 16×2 HD44780 LCD. The sensor is positioned to detect a black line on a white A4 paper surface, making it a foundational component for line-following robots and automated guided vehicles.

Hardware Components
Component	Quantity	Notes
Arduino Nano	1	Main microcontroller
HD44780 16×2 LCD	1	Character display (parallel interface)
Line tracking sensor	1	IR reflectance sensor (e.g., TCRT5000)
A4 paper	1	White sheet with a black line (e.g., electrical tape or marker)
Jumper wires	—	For connections
10 kΩ potentiometer	1	For LCD contrast adjustment
Wiring Summary
LCD data/control pins: RS → D12, EN → D11, D4–D7 → D5, D4, D3, D2

Sensor digital output: → D8

LCD V0: to potentiometer wiper (contrast)

Power: 5 V and GND shared between Nano, LCD, and sensor

Working Principle
Reflectance sensing: The IR line-tracking sensor emits infrared light. A white surface reflects most of it back to the phototransistor, while a black line absorbs it. This produces a digital HIGH/LOW signal depending on the sensor module's logic.

Signal reading: The Arduino reads the sensor output every 200 ms via digitalRead(sensorPin).

Display logic:

HIGH → "On Track" — the sensor is over the black line.

LOW → "Off Track" — the sensor is over the white paper (or vice versa depending on module polarity).

LCD update: The second row is cleared and rewritten each cycle so the status text stays current without leftover characters.

Code Behavior
setup() initializes the LCD (16 columns × 2 rows), prints a static title "Line Tracking" on row 1, and configures pin D8 as an input.

loop() reads the sensor, refreshes row 2, and prints either "On Track" or "Off Track", then waits 200 ms for display stability.

Typical Applications
Line-following robot prototypes

Edge/position detection on paper-based test tracks

Educational demonstrations of sensor feedback and LCD interfacing

Notes & Tips
Sensor polarity: Some modules output LOW on black and HIGH on white. If the labels appear inverted, swap the if conditions or invert the read value.

Contrast: If nothing appears on the LCD, adjust the potentiometer until characters are visible.

Line width: Keep the black line ~15–20 mm wide; IR sensors have a narrow detection zone.

Height: Mount the sensor 3–5 mm above the paper for the most reliable reading.

Possible Extensions
Add motors and an H-bridge to convert this into a full line-following robot.

Use two or three sensors for steering corrections (left/center/right).

Log tracking events to EEPROM or send status over serial for debugging.

I2C vs Non-I2C LCD — Short Version
Non-I2C (Parallel HD44780)
Wires to Arduino: 6 signal + 2 power = 8 wires

Pins used: 6

Code: LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

Talks directly to the HD44780 chip

I2C LCD
Wires to Arduino: 2 signal (SDA, SCL) + 2 power = 4 wires

Pins used: 2

Code: LiquidCrystal_I2C lcd(0x27, 16, 2);

Talks through a PCF8574 backpack chip on the back of the LCD
