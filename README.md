# Analog-Computer
A simple general purpose analog computer.

# Introduction
The Analog Computer V 1.0 is constructed with the purpose of being used as a general purpose yet simple analog computer capable of solving some simpler differential equations. To use the analog computer, wires must be set up between the pins of various functions on the board and an output sent to an oscilloscope to display the output voltage. A useful resource for how to set up the analog computer to simulate various things is [here](https://the-analog-thing.org/THAT_First_Steps.pdf). Which shows various Differential equations and how to solve them using an analog computer. However, The-Analog-Things's analog computer has multipliers and comparators which this analog computer does not have built in, this allows their analog computer to solve a wider range of differential equations, however it is entirely possible to solve such equations using this analog computer by using external multipliers and circuits on breadboards to expand its capabilities. Power for such circuits may be taken from the +15v, -15v and ground rails available on the board, however it is important to remember to take care as the +15/-15 v power supply can only supply a limited current. Remember to always check components datasheets before use.

![Photo of the finished circuit board design.](/Images/Board.PNG)
### Figure 1. Finished board design showing the general board layout.

# Integrators
![Screenshot of the inputs/outputs for the integrators.](/Images/integrator.PNG)
### Figure 2. Inputs/outputs for the integrators.

```math
V_{out} = - \int V_{in} dt + V_{IC}
```

The integrators are the heart of the analog computer, they integrate voltages over time. To allow for multiple voltages to be summed and integrated they have multiple inputs all connected to a summing junction, one of the inputs is weighted for 10x. 
Note that the integrators invert the signal they integrate.
The integrators have a time constant of 1000s^(-1)
Pinout:
* OUTPUTS – Output of the integrator, both pins are hard wired together (V_out). 
* X10 – Input weighted to be 10x the input value.
* INPUTS – Inputs for the integrator, all 3 are connected to the same summing junction via 10k and 1k resistors (V_in).
* IC – Initial condition, this is the starting value for the integrator and is the +c that is added after integration, note that this pin is only used when the integrator is not operating and is only for constant voltages (V_IC).

# Summers
![Screenshot of the inputs/outputs for the summers.](/Images/Summer.PNG)
### Figure 3. Inputs/outputs for the summers.

```math
V_{out} = \sum V_{in}
```

The summers are made to continuously sum voltages, they allow for multiple inputs including one 10x input, all three inputs are connected to the same summing junction. Note that the summer does not invert the sum of the signals, this is important as some analog computers do invert their signals.
* OUTPUT – Output of the summer, sum of input voltages (V_out).
* X10 – Input weighted to be 10x the input value.
* INPUTS – Inputs for the summer, all 3 are connected to the same summing junction via 10k and 1k resistors (x10 input) (V_in).

# Inverters
![Screenshot of the inputs/outputs for the inverters.](/Images/inverter.PNG)
### Figure 4. Inputs/outputs for the inverters.

```math
V_{out} = - V_{in}
```
The inverters continuously invert the voltage present at their input.
OUT – Output pin (V_out), inverted voltage.
IN – Input pin (V_in), voltage to be inverted.

# Coeficents
![Screenshot of the inputs/outputs for the Coeficents.](/Images/Coef.PNG)
### Figure 4. Inputs/outputs for the Coeficents.

```math
V_{out} = aV_{in} {0<=a<=1}
```
Coefficients or Coef’s take an input voltage and multiply it by a constant factor between 0 and 1, then output this voltage. The factor can be changed by adjusting the 4 coefficient potentiometers at the bottom of the board.
OUT – Output pin (V_out), output voltage.
IN – Input pin (V_in), input voltage.

# Trigger and Reset
![Screenshot of the inputs/outputs for the inverters.](/Images/Trigger.PNG)
### Figure 4. Outputs for the Trigger and reset.

The trigger and reset system is designed to reset the integrators to their respective initial conditions when specified. There are two modes which may be selected using the switch at the top of the board that says ‘MANUAL AUTO ‘. When Manual is selected, the integrators will continuously integrate indefinitely unless the reset button is pressed, this will reset the integrators to their initial conditions and a new integration will start.

When auto is selected the integrators will automatically reset after a fixed time interval, this time interval can be set by the potentiometer at the top of the board labelled reset rate. This also allows for the coefficients to be adjusted and see their effect in real time.

The trigger outputs are for attaching oscilloscopes to see the repeating output, the signal is between 0 and 5v and is high while operating, the oscilloscope should be set up to trigger on the rising edge of the signal.

While the analog computer is in normal operation the ‘OPERATING’ led will be illuminated.
