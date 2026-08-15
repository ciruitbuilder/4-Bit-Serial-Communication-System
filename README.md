DESCRIPTION

This is a 4 bit Serial communication system that takes 4 input bits, puts each of the bit one by one from the least significant bit(LSB) to the most significant bit(MSB) into a single wire. This data is collected and displayed by a receiver which is synchronized with the transmitter using a shared clock through a second wire. 

THE BUILD:

TRANSMITTER:

For the transmitter circuit, my objective was to design a logic circuit, that when a 4 bit number is entered in a parallel manner, and all of those parallel inputs are connected into a single wire through tri state buffer. These tri state buffers are used to enable each of those buffers one at a time to transfer the input bits one by one into the main data wire.

The logic mechanism i use to acheive this one by one enabling is designed by myself from scratch. The explanation on how i built the system in given below(called the "Enabling Circuit")


 Enabling Circuit:

 <img width="688" height="300" alt="cell explanation" src="https://github.com/user-attachments/assets/69422008-3a0b-4234-ab5f-113e80f3ce94" />

