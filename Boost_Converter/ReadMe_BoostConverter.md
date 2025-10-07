# Boost Converter Simulation (Using LTspice)

##  Objective
To simulate a boost converter using LTspice and analyze the output voltage behavior in response to a PWM switching signal.

##  Specs
- Input Voltage: 12V  
- PWM: 60% duty, 25kHz (`PULSE(0 12 0 1n 1n 24u 40u)`)  
- Inductor : 120 µH  
- Capacitor : 62 µF  
- Load Resistor: 50Ω   
- Diode: 1N5819  
- MOSFET: BSC060N10NS3  
- Simulation time: 10 ms (`.tran 0 10m 0 1u`)

##  Explanation
The MOSFET `M1` operates as a switch controlled by a PWM signal from `V2`.  
- When the switch is ON, the inductor stores energy by drawing current from the input supply.  
- When the switch is OFF, the inductor releases energy to the load through the diode, boosting the output voltage above the input.  
- The average output voltage is given approximately by:  
  Vout ≈ Vin / (1 - D)` 
  D is the duty cycle (0.6 in this case).

##  Result
- Output voltage is expected to stabilize around 30V (theoretical ideal value ≈ 12V / (1 - 0.6) = 30V).  
- Output voltage ripple is minimized by the LC filter.  

##  Files
- `boost_converter.asc` – LTspice schematic  
- `simulation_plot.png` – Simulation output as a screenshot  
- `ReadMe_BoostConverter.md` – This documentation  

