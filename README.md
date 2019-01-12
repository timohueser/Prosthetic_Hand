# Prosthetic_Hand_V1
## Overview
The aim of this project is to design a 3D printable hand prosthesis. The hand uses 6 cheap geared DC motors that are readily available from Ebay and other places for it's 6 degrees of freedom. Motor control is achieved through a custom made Motor driver PCB that also handles force measurements for each finger. All the 3D models in STEP and STL format are available in this repository, as well as the KiCad design files and schematic of the PCB. The Hand is fully self contained and only requires an external Power supply and a SPI control signal to be operated.

## Technical Details
### Fingers
The fingers are fully 3D printable and have 2 joints that move proportional to each other. It was decided to use rigid parts to drive the fingers instead of a string based system. This increases reliability and overall robustness but gives up some of the compliance that a string based system allows. The finger gets driven by a geared DC motor with a lead screw attached to its ouput shaft. A lead screw mechanism has the advantage of not being backdrivable, so the motor does not need to supply the holding torque for the fingers and only needs to be active during movement. With the motor gear ratio choosen the hand achieves reasonable movement speeds while still being able to apply ample force for tasks like picking up everyday objects. Unfortunately the way the lead screw mechanism is implemented in this version of the hand is not very durable, this is mainly due to the low quality of the lead screw and nut and the assymetric way the force gets applied to the lead screw with the current design. Version 2 of the prostehic hand mostly solves this reliability problem. Version 2 also replaces the cheap geared motors used in this version with high quality Maxon Dc motors that can produce significantly more power because of their higher efficiency. Also overall reliability of motor windings and the gearbox are obvious drawbacks of using the cheap motors compared to high quality ones. 

### Thumb
Similar to the other fingers the thumb uses a lead screw machanism to be positioned. In contrast to the other fingers the thumb has two degrees of freedom controlled by two seperate motors. One motor is placed inside the thumb itself and is responsible for flexion and extension of the thumb while the other sits inside the palm of the hand and controls abduction and adduction. This allows a variety of disserent gripping patterns, that the hand can switch bewtween quickly and without needing to be manually adjusted with the other hand. Having one of the motors inside the thumb is necessary to fit the realtively big motors choosen for this project inside the hand, but leads to a less than optimal weight distribution.
Furthermore the exact geometry, like for example the axis of rotation for abduction, still requires a lot of finetuning since the current geometry causes very unnatural positioning of the thumb for certain gripping patterns. Adding compliance to the abduction/adduction joint is a aim for version two, that is expected to greatly improve the capability of the hand to addapt do different objects.

### Motor Driver PCB
The motor driver PCB is based on the L293D Quad Half-H Driver to power the 6 DC motors. It needs to be supplied by a 9-12V motor power supply and a 3-5V supply for the logic and current sense circuitry. The motor supply should be able to handle at least 2 Amps of peak current draw. The motor driver ICs are controlled by a simple 74HC595 shift register, this enables very simple control over the hand over a standard SPI protocoll. Unfortunately there is no encoder readout for the motors for reasons of space constraint. This limits the precision the fingers can be positioned at significantly. 
In addition to motor drive capabilities the circuit also has 6 current sensors, consisting of a current sense resistor and a differential amplifier for each motor to monitor the strain on the motors. This can either be used as crude force feedback to the user of the hand or to limit the torque the hand can apply and stop motors from stalling as soon as the grip is closed. It is also useful as a homing feature since as mentioned previously there is no direct position readout for the fingers. 
Despite adding this position readout using motor drivers with better efficiency is is one of the major improvements that need to be made for the motor driver PCB used in version 2 of the prosthetic hand. The L293D drivers are very inneficient compared to more modern motor driver ICs and produce a lot of excess heat that builds up quickly in the tight and isolated environment the PCB is installed in. In addition many modern motor driver ICs have features like thermal cutoffs and motor current monitoring already built in, allowing for a much more compact PCB design. 
