<h1><B> Q1 </B></h1>
<h3><b>TASK A Q1</b></h3>

<h3><b>TASK B Q2 </b></h3>
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
<h2><B>PART B _ FLOWCHART</B> </h2>

<h2><B></B>PART B _ 1</B></h2>
<B>EASYEDA LINK:</B> 

<H2><B>PART B _ 2</B></H2>


