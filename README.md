Connections:
   
 Sensor Pins:
        GND: Connect to Arduino GND.
        VCC: Connect to Arduino 5V.
        SIG: Connect to a digital pin on the Arduino (e.g., D8).

    LCD Pins (as in your 6-pin setup):
        RS: Pin 12
        EN: Pin 11
        D4 to D7: Pins 5, 4, 3, 2
Explanation:

    Sensor Status: The sensor detects the black line (returns LOW) or the white surface (returns HIGH), and this is displayed on the LCD.
    LCD Output: The LCD will show either "On Line" or "Off Line" based on the sensor's reading.
    Delay: A small delay is added to make the LCD easier to read.

This simple setup allows you to visually monitor whether the sensor is on or off the line.
