<h1><B> Q1 </B></h1>
<h2><b>TASK A Q1</b></h2>
(a) Feed Forward Control:<br>
It is not necessary for us to know the current state of the system for  controlling it. This can be done with an open loop controller (; a feedforward controller)<br>
We have a reference, signal from the reference is fed forward through the controller and through the system, without ever getting to know the intial state of the system.<br>
Why feed forward control fails? <br>
Because it's not realistic enough and it is not robust to disturbances (noise). This control system works well only if there's no uncertainty, and the dynamics of both the system and the environment is well known.<br>
Entering Feedback control (;closed  loop control)<br>
in feedback loop, the controller uses both the reference and the current state of the system, to determine the action. It is a self- correcting mechanism. This controller comes in handy especially when the dynamics of the system or the disturbances caused by the environment aren't really known. <br>
So, it's seems to be much more dangerous than the feed forward controller, because it could go completely haywire. It seems to change the dynamics of the system. Analysis of these controllers is necessary.<br>
Types:<br>
Linear controllers , PID, Full state feedback<br>
Non linear controllers , ON OFF, Sliding mode <br>
Robust controllers, mu controller<br>
Adaptive controllers, Optimal controllers, Predictive controllers, Intelligent controllers.<br>
<br>
(b) low level motion control system<br>

For controlling any system, we need to consider a few thing:<br>
- controller <br>
- need to under the dynamics of the system<br>
- we need to consider the sensors we use, the noise it might produce<br>
- ways to reduce is noise so that the we get the desired output<br>
- ways to reduce the disturbance of the environment<br>
Main process: the robot <-- desired velocity, command.---> motor actuators(system)<br>
- disturbances are caused by the surrounding and especially in this case<br>
-  choosing the right sensor is equally essential<br<
- general classification of sensors: active and passive<br>
- choices considered: hall effect active magnetic sensor (Uses an external power source to detect magnetic fields. It is the most common for ROS 2 because it works at zero speed and provides a clean digital square wave)<br>
Passive Magnetic (Variable Reluctance): Induces its own current. These are cheaper and rugged but "go blind" when the robot moves slowly, making them poor for precise navigation.
Optical Sensors- high precision,very sensitive to dust, oil and mud.<br>
Capacitive sensors: high precision, rugged ti dust, oil etc. cons: can be sensitive to strong electromagnetic noise .<br>
best approach would be to go with active sensors because they produce less noise when compared to passive ones. and since the robot would be dealing with real life terrains, it shouldn't be sensitive to dust. and so far, the hall effect magnetic sensor proves to be more useful. cost is also reasonable.<br>
<br>
Now coming to the controller to be used,<br>
*On-OFF controller: Either fully on or off <br>
*Pros: extremely simple to implement, no parameters to tune<br>
*cons: large oscillations around setpoint<br>
*Noise Handling: noise causes chattering<br>
choices: PID Controller, Cascaded PID Controller, On-OFF controller<br>
*Cascaded PID Control has two loops - the Inner loop which controls fast dynamics and the Outer Loop which control slow dynamics like position control<br>
*Pros: Better handling of dynamics with multiple time scales when compared to classical PID Controller<br>
*Cons: Tuning is more complex, More Parameters <br>
*Noise Handling: Each loop can filter noise appropriate to it's bandwidth <br>
*PID Controller: <br>
*Pros: Good balance of perfomance and simplicity <br>
*Cons: Poor to moderate with significant delays/frictions<br>
* Noise handling- requires filtering (; low pass filter on derivative)<br>
- Best Choice : Cascaded PID Control , because it provides the best trade off between perfomance, robustness and implementation complexity for system with multiple dynamics.<br>
  
<h2><b>TASK B Q1</b></h2>
LINK TO GOOGLE NOTEBOOK:<br>
*Velocity Control Code and Tuning <br>
https://colab.research.google.com/drive/18Xy-2NBZ2KHjzY68AeUTxTbdUbRl1IzM?usp=sharing<br>
*Position Control and Tuning<br>
https://colab.research.google.com/drive/1D_jXjcwNX5t0EuK1DQT2Zc0uS6b2Gd4c?usp=sharing<br>

As one<b> increases the proportional gain, the system becomes faster </b>, but care must be taken not make the system unstable. Once P has been set to obtain a desired fast response, the integral term is increased to stop the oscillations. <b> The integral term reduces the steady state error, but increases overshoot.</b> Some amount of overshoot is always necessary for a fast system so that it could respond to changes immediately. The integral term is tweaked to achieve a minimal steady state error. Once the P and I have been set to get the desired fast control system with minimal steady state error, the derivative term is increased until the loop is acceptably quick to its set point. Increasing derivative term decreases overshoot and yields higher gain with stability but would cause the system to be highly sensitive to noise.<br>
Observation: <br>
As ki increases, the frequency looks like it reduces for position control. 
The main reason this happens is because position plant/ system already has an integrator and when we add another Integrator Controller, the phase change produced will be around -180°(2 integrators)  , which changes the polarity of the system, reduces damping, slows dynamics and  reduces the frequency of the system. (plots are in the Google collab) <br> 
The velocity plant will have a phase change of -90° ( 1 integrator) , and therefore, the value of ki isn't as high as it was in the case of the position plant. And that's why visually , velocity vs time graph looks more stable than the position vs time graph from the same values of kp,ki,kd.<br>
<br> The Ziegler-Nichols method is a method that comes in handy, whenever the error differences are not linear and when "trialandError" isn't really helping.  This method is similar to the "trialandError" method  , but by figuring out kp (or any of the other constant values) we can get the other values. <br>


<h2><b>TASK B Q2 </b></h2>
LINK TO GOOGLE NOTEBOOK: <BR>
https://colab.research.google.com/drive/1ZdIQa1U8x3bAU8oKOSm8XI_kqtKOjtg2?usp=sharing
<h1><b> Q2 </b></h1>
<H2>1</H2>
what we are dealing with:
unstable power suppy---<br>
  * introduces noise and interference to the system(any unwanted electrical signals that disrupt the clean flow of information or power between the components.) <br>
  * affect the signal integrity and cause EMC issues(measure of how clean and accurate the signal is , EMC- electromagnetic compatability, so basically the electromagmentic interference from the unstable power supply could leak into the other components, resulting in less accuracy)<br>
Components utilized:<br>
  * Regulator<br>
  * Decoupling Units<br>
Components needed mostly depends on the system, if the IC is the really fast, or needs huge amounts of current, then a power trace would be recommended to prevent  overheating , noise and also to prevent voltage drop, so that full voltage reaches the chip.<br>
<img width="654" height="207" alt="image" src="https://github.com/user-attachments/assets/d7be797d-0185-4344-8785-34d8e4083e29" />
The Circuit provided is considered to be a very effective model because of the different types of decoupling units it uses, which seem to cover majority of the noise frequency range.<br>
This is my reference.<br>
1. Regulator: <br>
LDO-- Linear voltage regulators<br>
-- less effective due to heat loss<br>
-- clean signal<br>
--cheaper<br>
--less complex<br>
-- voltage drop<br>
Switching Regulators-- uses high frequency switching and energy storing elements like the inductors and capacitors to convert voltage effectively.<br>
-- Noise, creates EMI<br>
-- expensive<br>
-- more complex<br>
--longer battery life<br>
Hybrid of Switching and LDO -- comparatively lesser noise than switching regulators, really efficient <BR>
-- disadvantages: more components, more cost (order of placement: SWITCHING REGULATORS---> LDO)<BR>
Switching regulators  produce noise because they switch at high frequencies causing RIPPLE, and EMI.<br>
So, we try to filter out the noise, either by attaching a LDO (low pass filter,ripple supressor (low to mid frequencies)) later to the circuit , or Decoupling units like Local Decoupling (that reduces the noise that enters the loads), or Capacitors ( ceramic or caps )- these cover HIGH frequency ripple and high frequency spikes<br>
because Z ( impedance ) for a capacitor is 1/2pifC ( resistance is inversely proportional to Z) , or a ferrite bead(high resistance to high frequency noise).<br>
<br>

Main reason to choose Hybrid switching regulators is because the battery is unstable, and this regulator even converts highly unstable power supply to stable ones.
We can also use power traces , which reduces EMI from leaking into the other components, and a few other decoupling units like, bulk decoupling, for more accuracy . And the
regulators come with their own caps.<br>
So, I believe this to be an effecient circuit because it reduces noise (if present) significantly, the decoupling units takes care of all frequency ranges of noise, EMI from
both the battery and the regulators are taken care of, by  the ferrite bead. And also not having every regulator as a LDO, reduces heat (not that there are no other methods available). A fuse prevents short circuiting. Different loads have different uses and hence parallel connection from the battery to the loads are done this way<br>
<br>
1. Switching regulator + Decoupling units + MotorControllers ( high current usage, so no LDO, ferrite bead is not neccesary because the load produces noise)<br>
<br>
2. Switching regulator + Ferrite Bead + LDO + Decoupling units + Encoder ( really sensitive to noise, we require precise signals)<br>
   <br>
3. Buck + LDO+ Decoupling Units+ Microcontroller ( buck does high- low stable signal convertion , Doesn't necessarily need LDO)<br>
<br>
4. Switching +  decoupling units + Orin ( high current usage)<br>
<img width="768" height="723" alt="image" src="https://github.com/user-attachments/assets/48891009-7e38-4b54-884c-2cb05cc372c7" />
<h2><b> 2 NEED FOR DIFFERENT SUBSYSTEMS IN A BOT </b></h2>
Different subsystems in the bot have different current and noise requirements. Motors draw high current and introduce switching noise, while the microcontroller and encoders require clean and stable power. Supplying them independently using separate regulators prevents noise coupling, improves efficiency, isolates faults, and increases battery runtime.  <br>
<br>
In order to control current independently, different approaches can be used such as relays, BJTs, MOSFET switches, LDO regulators or switching regulators. Relays are bulky and slow, and BJTs are less efficient for higher currents. For a battery-powered bot( + unstable one),  efficiency and compact size are important, so switching regulators and MOSFET-based power stages are more suitable.  I thought buck/buck-boost regulators with LDOs and filtering components were most suitable because switching regulators seem to convert unstable voltages to stable ones .<br>
<h2><b> 3 SAFETY </b></h2>
In a battery-powered bot, safety is crucial because high current draw, shorts, or sudden malfunctions could damage the battery or other components. To handle this, each subsystem is powered through separate regulated branches. This isolation ensures that a fault, noise, or voltage spike in one subsystem does not affect the others.<BR>
The regulators themselves provide voltage stability, current limiting, and thermal protection, which prevents excessive current in normal operation and helps avoid overheating. Proper trace widths for high-current paths and decoupling capacitors near sensitive loads further protect against voltage spikes or motor-induced noise.<BR>
For extreme cases, like a short circuit that exceeds the regulator’s limits, fuses or resettable polyfuses can be added at the battery input or before individual branches. This combination of regulated power, branch isolation, thermal/current protection, and optional fuses ensures that the system remains safe and reliable under both normal and unexpected conditions.<BR>

<h2><B>PART B _ FLOWCHART</B> </h2>
<img width="1080" height="336" alt="image" src="https://github.com/user-attachments/assets/f55198cc-d647-474a-9296-1fcb9197e8d3" />

<h2><B></B>PART B _ 1</B></h2>
<B>EASYEDA LINK:</B> 
https://oshwlab.com/rshanju/abhiyaan_pcb
https://pro.easyeda.com/editor#id=f8850334c7514b8fa20221f70373bff0
<H2><B>PART B _ 2</B></H2>
A battery's charge percentage can be calculated using the Coulomb counting method, which integrates the current drawn over time: Q= Integral I of dt.<br>
Then the state of charge is: (1-(Q/Qrated))*100 <br>
where Qrated is the battery’s rated capacity from its datasheet.<br>
The battery runtime is the estimated time the battery can continue supplying the load and can be calculated as: T= Qremaining/ Iaverage<br>
To measure I= I(t), either a current sensor IC (power management IC) or a shunt resistor can be used. The microcontroller periodically samples the current and performs the integration and averaging to compute the SoC and remaining runtime. SOH (State of Health ) is also important for calculation.

<h1> <b> Q3 </b></h1>
<h2> <b> Wired communication (1) </b></h2>
UART: (Universal Asynchronous Receiver/Transmitter)<br>
Best for: Simple, point-to-point communication.<br>
Speed: Low to medium<br>
Pros: Very low hardware complexity, easy to implement, data transfer is bi-directional,  checks for data loss by using the parity bit , only uses 2 wires, far more noise tolerant than I2C.<br>
Cons: Only supports communication between two devices, limited data transfer speed, relies heavily on the BaudRate of the individual UART Units for data transfer.<br>
<br>
I chose UART because the task requires transferring a small number sequence from one Arduino (or any microcontroller) to another. The maximum data size is only about 16 bits, and not all at once. Therefore, even UART’s relatively low data rate is more than sufficient for this application.<br>
Since both devices are Arduino UNOs operating at the same baud rate, synchronization errors are minimized. It seems for a reliable communication, the baud rates of both UART units typically needs to be within about 10% of each other, which is easily satisfied here.<br>
Additionally, the system only requires point-to-point communication and is a  simple setup. Once Arduino 1 sends the number sequence, the communication task is complete.<br>
<br>
I2C (Inter-Integrated Circuit)<br>
Best for: Connecting multiple devices with minimal wiring [ uses two lines - SDA ( Serial Data Line - used for data transfer) - SCL ( Serial Clock Line- clocks the time), data transfer isn't continuous ( happens in packets of 8 bits), MultiMaster - MultiSlave Communication protocol, after every 8 bit - the master device  acknowledges whether the slave device understood the previous 8 bit sequence (helps in preventing any sort of data loss)]<br>
Speed: Less than SPI.<br>
Pros: Supports up to 128 devices, requires only two wires(SDA and SCL), error detection facilities <br>
Cons: Requires careful address management, speed limitations, Very susceptible to noise and interference.<br>
<br>
SPI (Serial Peripheral Interface)<br>
Best for: High-speed communication with multiple peripherals.<br>
Speed: Higher than UART and I2C.<br>
Pros: Full-duplex communication, higher data transfer rates.<br>
Cons: More complex hardware, requires more pins (MISO, MOSI, SCLK, SS) , doesn't check for errors.<br>

<h2><b> CAN Communication </b></h2>
CAN:( Controller Area Network Protocol)<br>
-Widely used in automobile industry for reliable communication<br>
Pros: Bus topology , two wires ( CANH, CANL), tolerant to noise , error detection facilities ( CRC ) , differential methods helps in reducing errors, multiple nodes ( depends on whether it's a 11 bit or a 29 bit address)<br>
<br>
"CAN is most efficient in alienating noise from the environment without disturbing the readings "-  This is based on the differential method, CANBUS utilises. So, the wiring in a CANBUS is a twisted pair of CAN High and CAN low wires. Data is transmitted as the voltage difference between the two lines, rather than the voltage of a single wire with respect to ground. During transmission, both lines carry opposite voltage levels. So, when there is an external noise , both the CAN High and CAN low experience voltage spikes. But, the CAN receiver  works only with the difference between these two signals, and thus, effectively cancelling out the noise.
<img width="1586" height="692" alt="image" src="https://github.com/user-attachments/assets/b82498ea-fba2-4cf6-bd85-7f95d22fb3e5" />

<h2> <b> SIMULATION LINKS </b></h2>
https://www.tinkercad.com/things/erwICdZkVpA-abhiyaan2/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=c8vVt2wSSZkv-X_DKJlkScPARwrNJrRmhH60th8sm7Q
https://www.tinkercad.com/things/8mVY30VmV38-abhiyaan/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard%2Fdesigns%2Fcircuits&sharecode=c7bHuLZ_mh3UdyWbKgUoOqgCoMYWGOkaUBIicBPE6DI <br>
I wrote the code , but the simulation doesn't work.

<h2><b> Wireless protocols</b></h2>
*Wifi <br>
*Zigbee <br>
*Z Wave <br>
*Bluetooth <br>
*IR <br>
* NRF <br>
* NCF <br>
All these are protocols that are used in embedded devices. RF for instance, is the technology responsible for Wifi and Cellullar networks. RF communication can provide long range, high data rates, but it is susceptible to interference because many devices share the same frequency baand .So, RF has a long range, high data tranfer speed but is highly susceptible to noise.<br>

Wifi's underlying technology is RF. Wifi provides high data ratesm long range (within 100 m) and wasy internet connectivity. However, it consumes high power abd nay suffer from congestion and interference in crowded environments.<br>
 Bluetooth is a short range communication protocol (approc.10 m), low data transfer speeds and it is susceptible to noise.<br>
Zigbee is designed for low powerm low data rate sensor networks. It supports mesh networking and can connect muliple nodes effeciently. Commonly used in smart home systems.<br>
Z-wave is similar to Zigbee , but operates at lower frequency, reducing interference. It provides reliable short range communication and is used in home automation.<br>
 IR , again short range, less susceptibe to noise but requires direct line of sight (making it less usable) . In this case, it is best to use "Wifi" , because all the short ranges can't satisfy the range and all the others ,which have longer ranges are beyond our requirement. 

<h2> <b> REFERENECES:</b></h2>
Source: Altium https://share.google/wL8GfEMuJNEOGgKoL<br>
Intro to Arduino Programming.pdf https://share.google/fqGr6IcAfXLxWtYzZ<br>
GitHub - Mahmoud-Ibrahim-93/Communication-between-2-Microcontrollers: CSE4 Lab https://share.google/mAT2zQeaJzUa6mzv1<br>
I2C vs SPI vs UART – Introduction and Comparison of their Similarities and Differences - Total Phase https://share.google/6TXs2LGMP0T4y9Q2t<br>
Communication protocols: UART, I2C and SPI - HiBit https://share.google/gdI3UzkiZ2xWe0kcq<br>
An Overview of UART Protocols | Ezurio https://share.google/tf4UM9t2gSwXcYRoV<br>
Sending data noisy environment - Other Hardware / General Electronics - Arduino Forum https://share.google/K6I5Ge6Vsxwmv6cKo<br>
Best communication between two microcontrollers : r/embedded https://share.google/QKzzzE0G5RENsJoB5<br>
Source: YouTube https://share.google/b3I9kbGxfTb7Dke5o<br>
UART between two microcontrollers | All About Circuits https://share.google/mktdqW4Cz25Ot8CsH<br>



