# Buck Converter Simulation with Ideal Switch (Using LTspice)

##  Objective
To simulate a buck converter in LTspice using an ideal voltage-controlled switch and observe the output voltage behavior.

##  Specs
- Input Voltage: 12V DC
- Switching Frequency: 250kHz
- Duty Cycle: 50%
- Inductor: 100µH
- Capacitor: 1µF
- Load Resistor: 40Ω
- Simulation Time: 2ms
- PWM Signal: Controlled using `PULSE(0 1 0 0 0 {Ton} {T})`
- Switch Model:  
  `.model Q1 Sw(Ron = 0.001 roff = 1Meg Vt = 0.5)`

##  Parameters
- `.param fsw = 250k` → Switching frequency
- `.param T = 1/fsw` → Switching period
- `.param d = 0.5` → Duty cycle
- `.param Ton = D*T` → ON time

##  Explanation
The switch `S1` (model Q1) is toggled by a PWM signal defined with parameters. The simulation checks how the average output voltage relates to the input voltage and duty cycle (Vout ≈ Vin × D).

##  Result
- Output voltage should stabilize around 6V.
- The LC filter reduces ripple.
- The waveform shows expected buck converter behavior: 
  When the switch is on, the inductor charges.
  When off, the diode carries current.

##  Files
- `buck_converter_final.asc` → LTspice schematic of the buck converter
- `simulation.png` → Simulation output as a screetshot
- `README_buck_converter.md` → This documentation

# Boost Converter Simulation with Real Components (Using LTspice)

##  Objective
To simulate a boost converter in LTspice using a real MOSFET and diode, and analyze how the output voltage increases above the input voltage under PWM control.



##  Specs
- Input Voltage: 12V DC  
- Switching Frequency: 100 kHz (approximated from period `T = 10µs`)  
- Duty Cycle: 70% (Ton = 7µs, Toff = 3µs)  
- Inductor: 175 µH  
- Capacitor: 4.7 µF  
- Load Resistor: 10 Ω  
- Simulation Time: 3 ms  
- PWM Signal: Controlled using `PULSE(0 30 0 0.05u 0.05u 7u 10u)`  
- MOSFET Model: IPB067N08N3  
- Diode Model: RFN10BM3S



##  Explanation
The N-channel MOSFET `M1` (IPB067N08N3) is toggled by a PWM signal defined with a 70% duty cycle. When the MOSFET is ON, current flows through the inductor and stores energy in its magnetic field. When the MOSFET turns OFF, the energy stored in the inductor is released through the diode `D1` (RFN10BM3S) into the output capacitor `C1` and the load `R1`.

This behavior allows the circuit to boost the output voltage **above the input voltage**.


##  Result
- Output voltage is expected to increase above 12V (depending on load and duty cycle).
- The inductor stores energy during the MOSFET’s on-time and releases it during off-time.
- The Schottky diode allows current flow to the output while blocking reverse current.
- The capacitor smooths the output voltage ripple.

##  Files
- `buck_converter_ideal.asc` → LTspice schematic of the ideal buck converter
- `simulation.png` → Simulation output of the ideal converter as a screenshot
- `buck_converter_realistic.asc` → LTspice schematic of the realistic buck converter
- `README_buck_converter.md` → This documentation

