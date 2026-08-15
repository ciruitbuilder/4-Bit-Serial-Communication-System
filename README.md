DESCRIPTION

This is a 4 bit Serial communication system that takes 4 input bits, puts each of the bit one by one from the least significant bit(LSB) to the most significant bit(MSB) into a single wire. This data is collected and displayed by a receiver which is synchronized with the transmitter using a shared clock through a second wire. 

THE BUILD:

TRANSMITTER:

For the transmitter circuit, my objective was to design a logic circuit, that when a 4 bit number is entered in a parallel manner, and all of those parallel inputs are connected into a single wire through tri state buffer. These tri state buffers are used to enable each of those buffers one at a time to transfer the input bits one by one into the main data wire.

The logic mechanism i use to acheive this one by one enabling is designed by myself from scratch. The explanation on how i built the system in given below(called the "Enabling Circuit")


 Enabling Circuit:

 <img width="688" height="300" alt="cell explanation" src="https://github.com/user-attachments/assets/69422008-3a0b-4234-ab5f-113e80f3ce94" />

1. The pair of SR latches:

   the objective of this basic unit fo the mechanism is to, save binary 1 in a SR latch when clock goes low to high, save binary 0 in the SR latch when clock goes    high to low and pass the clock access to its next unit(by enabling its successive unit's tri state buffer and disabling its own).

   these bits which are saved and change with time in the first SR latch(towards the left, lets call it latch A and the other on latch B) is used to enable the       tri state buffers of the parallel input bits
   
