Recently ive been looking for elegant solution of
the simpliest arduino/avr based spwm device or a more
common name the inverter. And after some scretching of the 
internet, doing my researches in that field, finally
i came up with a simple approach of homebrew
dc/ac inverter
* The main idea was using these proto boards 
  From arduino.cc project like nano, uno etc.
* Also to use the chipest and simple circuitry
  so anyone else could do it for themselves
* Especially for those people in Ukraine suffering
  from shelling and blackouts on a daily basis

1. Concept
To get an alternating current wave out of dc supply
we have to pulse width modulate the sine wave.
The h-bridge topology is what we need.
In general we should provide short pulses for high 
and low power mosfets performing conducting with
the load. To create a positive half wave we open
The corresponding diagonal of the bridge, and vise
Versa for a negative. So in that way the current on 
the load gets alternated every 10ms.

2. Software
The original idea and the schematics comes from site
http://radiokot.ru and the author is константин_KoSS_89
as he claims himself.
Timer1 with its output compare rigisters has been applied.
It was initialized as a center alligned pwm.
We have to predefine some magic numbers
to provide our bridge with pwm cycles.
There is an array of bytes that keeps time for high and low 
mosfet in each diagonal to be opened. Those registers of 
timer1 OCR1A and OCR1B are being 
updated with those numbers from byte array.

3. Hardware
To drive the bridge i applied two half-bridge drivers
IR2104. It features a dead time insertions of approx 500ns,
shutdown capability, and opposite signal generation so on the 
input it has low or high signal and on the output it has both
high and low. Thus it neads only to pins of timer
to get working. Those generated signals are then applied
to the 6~7 volt AC transformer (50Hz with iron core). So the secondary winding
is outputting those 220 volts AC.
