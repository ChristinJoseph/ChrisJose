Task 1-
Here's what I understood from your problem:
You need to control a motor using the Sabertooth motor driver based on data received from an RC transmitter. Specifically, you're controlling Motor 1 via the S1 input of the Sabertooth.

The motor control data is being received from an RC transmitter. This transmitter is configured to transmit data within extended limits, which likely means the range of control values is broader than usual.

The data from the RC transmitter is being received by an SBUS receiver module. SBUS is a serial communication protocol that typically sends data for multiple channels in a single data packet.

 The task requires setting up the code to read SBUS data, interpret it, and then send the appropriate signals to the motor driver based on that data.

