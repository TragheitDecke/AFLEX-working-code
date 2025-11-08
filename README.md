# AFLEX Fuel Analyzer v4.0

A portable, accurate ethanol content and fuel quality analyzer built with Arduino and a GM flex fuel sensor.

## Overview

This project measures ethanol content (E0-E100), fuel temperature, and detects water contamination in real-time. Perfect for testing E85 at the pump before filling up, ensuring you get what you're paying for.

**Based on open source Flex Fuel v1.0** - significantly improved with bug fixes, water detection, and enhanced accuracy.

## Features

✅ **Accurate Ethanol Measurement** - Reads 0-100% ethanol content (±1-2% accuracy)  
✅ **Temperature Compensated** - Displays fuel temperature in Fahrenheit  
✅ **Automatic Water Detection** - Warns if fuel is contaminated with water  
✅ **PWM Output** - 0-5V signal for ECU integration (NEMU compatible)  
✅ **User-Friendly Display** - 16x2 LCD with clear status messages  
✅ **Portable Design** - Battery powered, 3D printed enclosure  

## What's New in v4.0

- 🐛 Fixed critical temperature calculation bugs (division by zero)
- 💧 Added automatic water contamination detection
- 📺 Improved startup sequence with status screens
- 🎯 Enhanced fuel presence detection logic
- ⚡ Better accuracy (±1-2% vs ±3% in previous versions)
- 🔧 Fixed tick rate calculation for more precise readings

## Hardware Requirements

### Electronics
- **Arduino Uno** or Nano (ATmega328)
- **GM/Continental Flex Fuel Sensor** (50-150 Hz output)
- **16x2 LCD Display** with I2C or parallel interface
- **Water/Moisture Sensor Module**
- **12V Windshield Washer Pump** (for fuel circulation)
- **Power Supply** - 9V battery or USB power bank with regulator

### Mechanical
- 3D printed enclosure (medical grade PETG recommended)
- Fuel-resistant tubing
- Inline fuel filter
- Viton O-rings for seals
- Check valve (optional but recommended)

## Wiring Diagram

```
Arduino Pin Connections:
- Pin 8  → GM Sensor Signal (frequency input)
- Pin 3  → PWM Output (0-5V for ECU)
- Pin A0 → Water Sensor Analog Input
- Pins 2,4,5,6,7,9 → LCD Display

GM Sensor:
- Pin 1: +12V
- Pin 2: Signal → Arduino Pin 8
- Pin 3: Ground

Water Sensor:
- VCC → 5V
- GND → Ground
- A0  → Arduino Pin A0
```

## Installation

1. **Clone this repository:**
   ```bash
   git clone https://github.com/TraghettDecke/AFLEX-working-code.git
   ```

2. **Open in Arduino IDE:**
   - Open `AFLEX_4.0.ino`
   - Install required library: `LiquidCrystal.h`

3. **Upload to Arduino:**
   - Select your board (Arduino Uno/Nano)
   - Select correct COM port
   - Click Upload

4. **Calibrate Water Sensor:**
   - Monitor `waterLevel` reading in dry air (typically 0-100)
   - Test with clean fuel (should be similar)
   - Test with water-contaminated fuel (typically 400+)
   - Adjust threshold in code if needed:
     ```cpp
     if (waterLevel > 300) {  // Adjust this value
     ```

## Usage

1. **Power on the device** - Displays startup sequence
2. **Connect fuel sample** - Pump fuel through the sensor
3. **Wait for "Analyzing fuel..."** message
4. **Read results:**
   - Ethanol percentage (0-100%)
   - Frequency reading (Hz)
   - Temperature (°F)
   - Water status (OK or WARNING)

### Display Examples

**Normal Reading:**
```
Ethanol: 75%
52Hz  68°F  OK
```

**Water Contamination:**
```
*** WARNING ***
WATER DETECTED!
```

## How It Works

The GM flex fuel sensor outputs a frequency signal that varies with ethanol content:
- **50 Hz** = E0 (0% ethanol / pure gasoline)
- **150 Hz** = E100 (100% ethanol)

Temperature is encoded in the duty cycle of the signal. The Arduino measures both frequency and duty cycle to calculate ethanol content and temperature simultaneously.

Water detection uses a separate conductivity sensor, as water conducts electricity while gasoline and ethanol do not.

## Accuracy

- **Ethanol Content:** ±1-2% (tested against known samples)
- **Temperature:** ±2°F
- **Water Detection:** Binary (Present/Not Present)

*Note: E85 from gas stations typically varies from E51-E83, so small variations are normal.*

## Troubleshooting

**"SENSOR ERROR" message:**
- Check GM sensor connections
- Verify sensor is getting 12V power
- Ensure signal wire isn't damaged

**Erratic readings:**
- Add pull-up resistor (1-4.7kΩ) on signal line
- Check for electrical noise/interference
- Ensure proper grounding

**Water sensor false positives:**
- Adjust threshold value in code
- Clean sensor contacts
- Verify sensor is fully submerged during test

## Future Improvements

- [ ] Bluetooth data logging
- [ ] Battery level indicator
- [ ] Calibration mode via button
- [ ] SD card data storage
- [ ] Android/iOS companion app

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Share your build photos

## Credits

- Original Flex Fuel v1.0 - Open source foundation
- GM/Continental - Flex fuel sensor specifications
- Arduino Community - Library support

## License

This project is open source. Feel free to use, modify, and distribute.

**Important:** Always follow local regulations regarding fuel handling and testing.

## Safety Warning

⚠️ **Working with fuel is dangerous!**
- Work in well-ventilated areas
- Keep away from ignition sources
- Use fuel-resistant materials
- Follow proper safety procedures
- Ensure all electrical connections are sealed

## Contact

Questions or suggestions? Open an issue on GitHub!

---

**Made with 🔧 for the tuning community**
