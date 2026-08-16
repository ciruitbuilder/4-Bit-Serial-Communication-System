DESCRIPTION

This is a 4 bit Serial communication system that takes 4 input bits, puts each of the bit one by one from the least significant bit(LSB) to the most significant bit(MSB) into a single wire. This data is collected and displayed by a receiver which is synchronized with the transmitter using a shared clock through a second wire. 

THE BUILD:

TRANSMITTER AND RECIEVER:

For the transmitter circuit, my objective was to design a logic circuit, that when a 4 bit number is entered in a parallel manner, and all of those parallel inputs are connected into a single wire through tri state buffer. These tri state buffers are used to enable each of those buffers one at a time to transfer the input bits one by one into the main data wire. Recciever too uses a similar enabling circuit, but the difference is the tri state buffers are inverted do that the data is loaded into a array of sr latches from the incoming ,single data wire as the buffers are enabled one at a time.

The logic mechanism i use to acheive this one by one enabling is designed by myself from scratch. The explanation on how i built the system in given below(called the "Enabling Circuit")


 Enabling Circuit(called "unit" here):

 <img width="688" height="300" alt="cell explanation" src="https://github.com/user-attachments/assets/69422008-3a0b-4234-ab5f-113e80f3ce94" />

1. The pair of SR latches:

the objective of this basic unit fo the mechanism is to, save binary 1 in a SR latch when clock goes low to high, save binary 0 in the SR latch when clock goes    high to low and pass the clock access to its next unit(by enabling its successive unit's tri state buffer and disabling its own).

these bits which are saved (and change with time due to the clock) in the first SR latch(towards the left, lets call it latch A and the other on latch B) is       used to enable the tri state buffers of the parallel input bits.
latch A is used to save the main bit, and latch B is used to save the "usage history" of the main bit, once the latch A is set, its designed so that it            automatically sets latch B, logically indicating latch A has already been set once, this information is later used by further logic circuits to disable this       unit's clock and enable clock for its successive unit

2. Pair of tri state buffers:

the Q of latch A is connected to the main clock of the system through two tri state buffers, for setting both the latches at once when clock goes from low to   high. One tri state buffer is for enabling clock for rising pulse(enabled by default) and disable it once the latch A has been reset by falling clock pulse     (high to low)[i.e in short for units that has usage history : used(latch B in in set state)], another one is to not allow clock access for the successive units
until the current unit(which as clock access) has its latch A reset by the falling clock pulse.

3. XOR gate:

The xor gate is used here to disable the clock access(using one of the tri state buffers) of the unit once the falling clock pulse resets latch A(while leaving    latch B set). Specifically, i chose a XOR gate because, when the latch A is reset, latch B remains set, so latch A stores 0 and latch B stores 1, to indicate      this state logically to cut clock access, i needed a gate that gives a output different than its normal state(when it receives both 1 and 1 or 0 and 0 in its      inputs[happens when clock pulse rises and also when history of usage is 0(the unit hasn't been used yet)]) when both of its inputs are different, which turned     out to be XOR gate.

the output of this xor gate is inverted(to have the clock enabled by default until the latch A and B store 0 and 1 respectively) and connected to enable of one    of tri sate buffers, inputs of xor gates are connected to respective outputs of each latches

4. the AND gate:
   
the and gate connected to the reset pin of the latch A is responsible for resetting the latch A once the clock pulse fell from 0 to 1, this is achecived by        creating an inverted clock pulse(using NOT gate) of the original clock and feeding it to the andgate. AND gate is used here instead of just directly feeding       the inverted clock into the reset pin is because to only allow the reset operation to happen when the latch A in in set state(storing 1).

This unit is replicated multiple times , equal to the number of necessary bits of data we need to transfer(here, 4 bits) and each individual unit's latch A 's output 1 is connected to the enable of the tri state buffers of the input switches and output latches

Both the receiver and transmitter share the same clock(clock of transmitter) and inverted clock to maintain synchronous read of transmitted date to respective bits

INPUT AND OUTPUT SR LATCHES:

The SR latch at the tranmitter circ
