# Experiment 6:
# Current Mirror Circuit
## Part A
## Aim:
 Design and Analyze Current mirror circuit as active load in amplifier circuit.
**Given** :
- Power Supply (V<sub>DD</sub>) = 1.8V.
- Power Consumption (P) <= 1mW. 
- Gain (A<sub>v</sub>) > -10V/V.

### Perform
- DC Ananlysis
- Transient Analysis
- AC Analysis
- Extract required parameters

## Components Required:
- MOSFET(NMOS,PMOS)
- Resistors
- Current source
- Voltage supply
- Connecting wires

## Theory
### Function:
The primary purpose of a current mirror is to replicate a current flowing through one active device (the "input" transistor) to another active device (the "output" transistor), maintaining a constant current regardless of load conditions.
In this specific configuration, the two PMOS transistors are used to create a current mirror, with the NMOS transistor acting as a current source or sink. 
### Operation:
- The input current is set by an external source, which flows through the input PMOS transistor. 
- The voltage drop across the input PMOS transistor is mirrored by the output PMOS transistor. 
- This mirrored voltage drop, in turn, controls the current flow through the output PMOS transistor, creating a mirrored current.

## Circuit Diagram

![Image](https://github.com/user-attachments/assets/f5bd39e0-d8e9-46bd-954a-145ff21f8ad8)

- Input bias Voltages(V<sub>2</sub> and V<sub>3</sub>= 0.95V): A DC current that flows into or out of the amplifier's input pins to establish a defined operating point, ensuring proper amplification and preventing saturation. 
- Power Supply(V<sub>1</sub>=1.8V): Provides the necessary DC voltage levels (positive and negative) to bias the MOSFETs, enabling them to operate in the desired amplification region and ensuring proper signal amplification and stability.
- Output Nodes(V<sub>out1</sub>): The output is taken from this terminal.
- PMOS(M2,M3) and NMOS(M1): NMOS typically acting as a current sink (drawing current towards ground) and PMOS acting as a current source (supplying current from the positive supply). 
- Current source (I<sub>ref</sub>): The current source's role is to provide a stable and well-defined reference current

Calculations:<br>
I<sub>t</sub>=P/V<sub>DD</sub>.<br>
I<sub>t</sub>=I<sub>ref</sub>+I<sub>x</sub>.<br>

## DC Analysis(1:1)

### Steps to Perform DC Analysis in LTspice XVII:
1. Build the circuit as per the diagram shown above and set the values of the voltage sources,resistors as per the calculated values.
2. Next go to **SPICE Directive** and type **.lib filename.lib or .lib filepath.lib** to import the Library file.
3. Click **OK**, and place the generated command on the schematic.
4. After importing the library file name the two mosfet as CMOSN.
5. Set the channel length value of M<sub>1</sub> as 180nm and  we have to vary the value of the width to get a desired value of I<sub>D</sub> and V<sub>out</sub>
6. Repeat the same steps with M<sub>2</sub> mosfet.
7. Now go to **Edit simulation command** and select **DC op pnt**.
8. Click **OK**, and place the generated command on the schematic.
9. Next click on run button, you will get a pop up window which gives us information about operating point.It includes the values of V<sub>out</sub> and I<sub>D</sub>.

As we know I<sub>t</sub>=I<sub>ref</sub>+I<sub>x</sub><br>
Therefore, for 1:1 ratio I<sub>ref</sub>=Ix<sub>x</sub>br>
So,I<sub>ref</sub>=I<sub>t</sub>/2<br>
I<sub>t</sub>=P/V<sub>DD</sub><br>
I<sub>t</sub>=1mW/1.8V<br>
I<sub>t</sub>=0.555mA.<br>
Therefore,I<sub>ref</sub>=0.2778mA.<br>

To obtain the current value according to the given ratio, the provided values of W/L for M1 is 3um/180nm , M2 is 3um/180nm, and M3 is 3um/180nm.<br>
Vin is selected in such a way that it should be in saturation region so the given Vin is 0.838V.<br>

OUTPUT:

![Image](https://github.com/user-attachments/assets/a41e51b1-a35c-475c-854d-16af4a2f0c67)

### Analyzing the current mirroring circuit by changing the w and L but maintaing the same ratio.

**(a)L=180nm.**

We know the (w/L) ratio is 16.667.

Therefore for L=180nm the w=3um.

|Mosfet     |  I<sub>d</sub>                 | 
|-----------|---------------------|
|  M1       |   0.000277527       |             
|  M2       |   0.000277527       |         
|  M3       |   0.0002778         |             

**(b)L=500nm.**

We know the (w/L) ratio is 16.667.

Therefore for L=500nm the w=8.334um.

|Mosfet     |  I<sub>d</sub>                  |  
|-----------|-----------------------|
|  M1       |   0.000281241         |             
|  M2       |   0.000281241         |             
|  M3       |   0.0002778           |             

**(c)L=1um.**

We know the (w/L) ratio is 16.667.

Therefore for L=1um the w=16.667um.


|Mosfet     |  I<sub>d</sub>                   | 
|-----------|-----------------------|
|  M1       |   0.000280654         |             
|  M2       |   0.000280654         |             
|  M3       |   0.0002778           |             

## Transient Analysis

### Steps to Perform Transient Analysis in LTspice XVII
1. After setting the operating point, we will give sine wave as the input for both the gate terminals of the mosfet.
2. Next set the **Amplitude** as 50mV and **Frequency** as 1kHz for both V<sub>2</sub> and V<sub>3</sub>.
3. You should specify the AC amplitude for each voltage source separately. You have two voltage sources, you can set their AC amplitudes as follows:
 - First Voltage Source(V<sub>2</sub>): **AC amplitude** = 1
 - Second Voltage Source(V<sub>3</sub>): **AC amplitude** = -1
4. Next set **phi[deg]** for V<sub>3</sub> as 180.
5. Now go to **Edit Simulation cmd** and select **Transient**.
6. Give **stop time** as per your convenience, here it is 5m.
7. Click **OK**, and place the generated command on the schematic.
8. Verify the response and note the phase shift and signal gain.


![Image](https://github.com/user-attachments/assets/4a440a69-f0b9-46cb-ab46-74ac451959a9)

INPUT:

![Image](https://github.com/user-attachments/assets/c62f9169-72ab-4ef2-843d-e601be447097)

OUTPUT:

![Image](https://github.com/user-attachments/assets/6041cebc-b8d6-4d4c-9611-35583355ceef)

The Expected gain of the circuit is -10V/V.But the obtained gain from the transient analysis is -10.12V/V.

## AC Analysis

### Steps to Perform AC Analysis in LTspice XVII:

1. Go to Simulate > Edit Simulation Cmd.
2. In the AC Analysis tab, choose Decade as the sweep type.
3. Specify the number of points per decade and set the frequency range from 0.1Hz to 1THz.
4. Click OK and place the generated command on the schematic.
5. Ensure that the input voltage source has an AC amplitude of 1V.
6. Click the Run button to start the analysis.
7. Examine the gain and phase plots.
8. Determine key characteristics such as bandwidth and gain margin.

![Image](https://github.com/user-attachments/assets/636e9b0b-5769-4497-b82a-003412e191f3)

 OUTPUT:
 
![Image](https://github.com/user-attachments/assets/34f2279c-0fd6-4b1c-90f6-f3d95a0443d6)

The Expected gain in db of the circuit is 20db.But the obtained gain from the AC analysis(frequency response) is 22.117db.

|Parameter      |Theory value  | Practical value |
|---------------|--------------|-----------------|
|Av(in dB)      | 20dB         | 22.117dB         |
|Av(in V/V)     | 10           | 10.12            |

**3db Bandwidth:**

The obatined 3db B.W=2.253GHz.

![Image](https://github.com/user-attachments/assets/4c9f54bb-8fcd-49f3-8c97-8d90e143613e)

## DC Analysis:(for mirror ratio 1:2)

As we know I<sub>t</sub>=I<sub>ref</sub>+I<sub>x</sub><br>
Therefore, for 1:2 ratio 2*I<sub>ref</sub>=I<sub>x</sub><br>
So,I<sub>ref</sub>=I<sub>t</sub>/3<br>
I<sub>t</sub>=P/V<sub>DD</sub<br>
I<sub>t</sub>=1mW/1.8V<br>
I<sub>t</sub>=0.555mA.<br>
Therefore,I<sub>ref</sub>=0.185mA.<br>

To obtain the current value according to the given ratio, the provided values of W/L for M1 is 6um/180nm , M2 is 6um/180nm, and M3 is 3um/180nm.<br>
Vin is selected in such a way that it should be in saturation region so the given Vin is 0.763V.<br>

![Image](https://github.com/user-attachments/assets/792237e5-ca5c-4a18-938d-8cf86e65bf7f)

OUTPUT:

![Image](https://github.com/user-attachments/assets/d6b1ba32-0f98-43f5-b57a-8624733312e1)

## Transient Analysis

### Steps to Perform Transient Analysis in LTspice XVII
1. After setting the operating point, we will give sine wave as the input for both the gate terminals of the mosfet.
2. Next set the **Amplitude** as 50mV and **Frequency** as 1kHz for both V<sub>2</sub> and V<sub>3</sub>.
3. You should specify the AC amplitude for each voltage source separately. You have two voltage sources, you can set their AC amplitudes as follows:
 - First Voltage Source(V<sub>2</sub>): **AC amplitude** = 1
 - Second Voltage Source(V<sub>3</sub>): **AC amplitude** = -1
4. Next set **phi[deg]** for V<sub>3</sub> as 180.
5. Now go to **Edit Simulation cmd** and select **Transient**.
6. Give **stop time** as per your convenience, here it is 5m.
7. Click **OK**, and place the generated command on the schematic.
8. Verify the response and note the phase shift and signal gain.

![Image](https://github.com/user-attachments/assets/73700227-f1c9-4959-9f7b-451a2113ce76)

INPUT:

![Image](https://github.com/user-attachments/assets/482b6bc0-1a1a-4115-959f-76b6a4cb1d22)

OUTPUT:

![Image](https://github.com/user-attachments/assets/a13ee9d1-08a3-441e-9a23-c97182fb14e6)

The Expected gain of the circuit is -10V/V.But the obtained gain from the transient analysis is -11.36V/V.


## AC Analysis

### Steps to Perform AC Analysis in LTspice XVII:

1. Go to Simulate > Edit Simulation Cmd.
2. In the AC Analysis tab, choose Decade as the sweep type.
3. Specify the number of points per decade and set the frequency range from 0.1Hz to 1THz.
4. Click OK and place the generated command on the schematic.
5. Ensure that the input voltage source has an AC amplitude of 1V.
6. Click the Run button to start the analysis.
7. Examine the gain and phase plots.
8. Determine key characteristics such as bandwidth and gain margin.


![Image](https://github.com/user-attachments/assets/9cd5cb62-1b5b-4c7b-858b-704d2a5a957e)

 

The Expected gain in db of the circuit is 21.34db.But the obtained gain from the AC analysis(frequency response) is 24.55db.

|Parameter      |Theory value  | Practical value |
|---------------|--------------|-----------------|
|Av(in dB)      | 21.34dB      | 24.55dB         |
|Av(in V/V)     | 10           | 11.36          |

**3db Bandwidth:**

The obatined 3db B.W=1.186GHz.

![Image](https://github.com/user-attachments/assets/60a9df80-3b1b-41b5-b14f-8215f75df050)

### **Comparison Table:**
| **Parameter**  | **Mirror Ratio 1:1** (Theory) | **Mirror Ratio 1:1** (Practical) | **Mirror Ratio 1:2** (Theory) | **Mirror Ratio 1:2** (Practical) |
|---------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| Av (in dB)    | 20 dB                        | 22.117 dB                     | 21.34 dB                     | 24.55 dB                     |
| Av (in V/V)   | 10                           | 10.12                          | 10                           | 11.36                         |
| 3 dB Bandwidth | -                            | 2.253 GHz                     | -                            | 1.186 GHz                     |  


## Inference:

- The implemented current mirror circuit accurately replicates the reference current with minimal deviation, demonstrating effective current mirroring across different W/L ratios.

- When the W/L ratio is varied while maintaining the same proportionality, the drain current (Id) remains nearly constant, confirming the reliability of the mirror circuit.

- The measured amplifier gain is slightly higher than the theoretical prediction for both mirror ratios, likely due to minor mismatches in transistor parameters or simulation-related variations.

- An increase in the mirror ratio from 1:1 to 1:2 results in a higher gain, as anticipated. However, this also leads to a reduction in bandwidth—from 2.253 GHz to 1.186 GHz.

- Overall, the simulation results align closely with theoretical expectations, validating both the circuit design and the simulation methodology.



## Part B

## Aim:
Design the differential amplifier using the same design specification as Experiment-3. Perform DC analysis,trasient and AC analysis.

## DC Analysis

- Repeat the same steps as mentioned in the above section.

![Image](https://github.com/user-attachments/assets/8ef76f51-e4b2-469e-b4ed-2fa01ff3582b)

Here’s a well-structured explanation of the DC Analysis for your circuit while ensuring that all MOSFETs operate in the saturation region and match the experimental results.

1. Circuit Overview

The circuit comprises six MOSFETs (labeled M1 through M6), each with specified (W/L) ratios. It is essential to ensure that all transistors operate in the saturation region throughout the analysis for accurate performance. The given width-to-length ratios for the transistors are as follows:

- M1: 108 μm / 180 nm
- M2: 108 μm / 180 nm
- M4: 108 μm / 180 nm
- M3: 49.1 μm / 180 nm
- M5: 57.33 μm / 180 nm
- M6: 57.33 μm / 180 nm

To preserve consistency with Experiment 3, the circuit must maintain the same DC operating point, which includes both the current levels and node voltages. Accordingly, the biasing conditions are selected to match those of the previous experiment.

![Image](https://github.com/user-attachments/assets/2cceda88-b45c-4953-82ef-5f89d74089e1)


## Transient Analysis

- Repeat the same steps as mentioned in the above section.

Circuit Diagram:

![Image](https://github.com/user-attachments/assets/d9721172-90ac-4507-80cb-f209b5f9fdb8)


INPUT:

![Image](https://github.com/user-attachments/assets/d29de8c7-91f6-471f-8afc-b95161aa0ed0)

OUTPUT:

![Image](https://github.com/user-attachments/assets/fcf711dc-4d72-4097-9948-bab749e0348f)

The Expected gain of the circuit is -8.6V/V.But the obtained gain from the transient analysis is -13.979V/V.

## AC Analysis

- Repeat the same steps as mentioned in the above section.

Circuit Diagram:

![Image](https://github.com/user-attachments/assets/1bfcd546-2f16-4a24-a6f2-53143182cb63)


The Expected gain in db of the circuit is 22.72db.But the obtained gain from the AC analysis(frequency response) is 23.46db.

|Parameter      |Theory value  | Practical value |
|---------------|--------------|-----------------|
|Av(in dB)      | 21.34dB      | 23.46dB          |
|Av(in V/V)     | 8.6          | 13.979           |

![Image](https://github.com/user-attachments/assets/f399a75e-d2e7-4f46-930b-c552aec7adb2)



**3db Bandwidth:**

The obatined 3db B.W=400.0834MHz.

 ![Image](https://github.com/user-attachments/assets/e4acc891-9d80-4cc1-9dfb-543e7616c284)


## Inference

- The observed gain, which exceeds expected values, may be attributed to additional gain contributions arising from parasitic effects or mismatches between devices.

- The measured high bandwidth of 406.16 MHz indicates that the amplifier is well-suited for high-frequency applications.

- Moreover, the deviation in gain could also result from an underestimation of the drain resistance or variations in transconductance across the devices.


# Experiment-06
