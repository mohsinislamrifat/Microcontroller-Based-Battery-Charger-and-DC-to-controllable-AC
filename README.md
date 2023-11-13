# Microcontroller-Based-Battery-Charger-and-DC-to-controllable-AC
In this Project we used three different type of circuits such as Battery charger Circuit, Inverter Circuit and AC voltage controller Circuit.

Circuit Operation:
Circuit (i): Battery Charger Circuit
• An AC supply (220 v) is connected to a step down transformer’s primary sideand from the
secondary side it gives approximate 12 v AC voltage.
• A LED as an indicator is connected with the secondary site of the transformerby a resistor.
• There is a bridge rectifier connected with the 12 volt AC and it gives 12 voltDC.
• The capacitor removes the ripple voltage.
• This DC is connected to a rechargeable battery and the battery will berecharged if
there is a supply (AC) to the transformer’s primary side.
• To show the battery voltage into the LCD display (and serial monitor) we usethe
ARDUINO Analog Read feature.
• Battery voltage goes to the Arduino Analog Pin (A1) via two resistors (usingVDR),
Arduino reads the voltage and monitors into the LCD.
• In Arduino program we have used the equations,
𝑦=𝑥∗(5.0/1023.0) 𝑏𝑎𝑡𝑡𝑉𝑜𝑙𝑡=𝑦/{𝑅2/(𝑅1+𝑅2)}


Circuit (ii): DC to AC Converter / Inverter Circuit
• In our country we use 50~60 Hz AC frequency.
• Arduino UNO’s Digital Pin number ‘6’ can generate a (square wave) PWM of62500 Hz
frequency, where cycle length is 256 (0~255).
• But, by the help of a divisor, we can generate (62500/1024 = ) 61.035 Hz.
Forthis purpose,following setting is needed to use:
TCCR0B = TCCR0B & 0b11111000 | 0x05
{Reference: http://playground.arduino.cc/Main/TimerPWMCheatsheet}
Here the duty cycle 50% is achieved, in the Arduino code Analog Write(255*50% ≈ )
127.
• This PWM signal is read by a digital pin of Arduino and another two digital pins are giving
two individual pulses, while pulse(1) is HIGH, pulse(2) is LOW and vice versa.
• There are two NPN transistors, which are controlled by the Arduino pulses.
• The operation is like this- while transistor(1) is forwardly biased therefore current conducts
from Collector to Emitter; transistor(2) is reversely based, so no current conducts.
• Transistors’ Collectors are connected to two N-channel Power MOSFETs. And the Emitters
are Grounded.
• We know that, the n-MOSFET is switched ‘ON’ if the Gate voltage is higher than its
threshold voltage (say, VGS = 1); switched ‘OFF’ if the Gate voltage is lower than its threshold
voltage (say, VGS = 0).
• Here, first half period of one cycle, when transistor(1) is in forward biased, there is no
MOSFET(1) Gate voltage because the current is directly bypassed to the ground via transistor(1) and
the MOSFET(1) goes OFF state.
• During this period transistor(2) is in reverse biased and MOSFET(2) goes ON state.
• Next half period of that cycle, same but opposite operation occurs.
• This allows the DC voltage to be produced across the primary of the transformer at alternate
intervals. It is 6v AC.
• The 6v AC signal across the primary of the transformer is then stepped up to 220v AC signal
across the transformer secondary.
• Thus we get converted 220 volt AC from 6 volt DC.


Circuit (iii): AC Voltage Controller Circuit
• The inverter’s output voltage (220v AC) can be controlled by an AC controller.
• An AC voltage controller contains a DIAC, a TRIAC, a Capacitor, resistors and a
Potentiometer (POT).
• The DIAC is a full-wave or bi-directional semiconductor switch that can be turned on in both
forward and reverse polarities. The TRIAC is also bi-directional, just like a DIAC, but it needs a
Gate signal to conduct current.
