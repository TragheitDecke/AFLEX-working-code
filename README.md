# AFLEX-working-code
Ethanol Analyzer 2.0
/*******************************************************
    ________    _______  __    ________  __________ 
   / ____ / /   / ____/ |/ /   / ____/ / / / ____/ / 
  / /__/ / /   / __/  |   /   / /_  / / / / __/ / /  
 / ___  / /___/ /___ /   |   / __/ / /_/ / /___/ /___
/_/  /_/_____/_____//_/|_|  /_/    \____/_____/_____/
v2.0 - Taken from open source Flex Fuel v1.0
This program will sample a 50-150hz signal depending on ethanol 
content, and output a 0-5V signal via PWM.
The LCD will display ethanol content, hz input, mv output, fuel temp
Connect PWM output to NEMU Breakoutboard on ADC0-3, and tune
the "AFLEX FUEL SETUP" tab accordingly. NOTE: Lowpass filter to
be used on output.
Input pin 8 (PB0) ICP1 on Atmega328
Output pin 3 PWM
********************************************************/

