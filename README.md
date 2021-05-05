# Testing_Rig
This program sends for a defined time period random values ( = direction, steps and delay times) to an arduino 
for moving a stepper motor randomly back and forth with random steps and a random delay between the steps ( =>
determing speed)

it is designed to work with ... stepper_turntable_v2_python2arduino_v2.ino ...

The key functions are:
    sendToArduino(str) which sends the given string to the Arduino. The string may 
                       contain characters with any of the values 0 to 255

    recvFromArduino()  which returns an array. 
                         The first element contains the number of bytes that the Arduino said it included in
                             message. This can be used to check that the full message was received.
                         The second element contains the message as a string
    residual functions are for grabbing streaming information from Trodes and saving this off in separate excel and txt files


 the overall process:
   1) open the serial connection to the Arduino - which causes the Arduino to reset
   2) User defined values for commutator type, ID and Lab ID are entered
   3) start streaming in Trodes
   3) run this program and wait for a message from the Arduino to give it time to reset
   4) loop through a series of random values sent to the arduino for a specified period; feedback to and from the
    arduino is given
   5) results (=packet drops, disconnects) are grabbed from Trodes debugLog files and given as different ouptput files

 the message to be sent to the Arduino starts with < and ends with >
    the message content comprises 3 integers
    these numbers are sent as their ascii equivalents
    for example <1,200,1500>
    this means set the motor counterclockwise, for 200 steps with a delay of 1.5 ms between each step interval 

 receiving a message from the Arduino involves
    waiting until the startMarker is detected
    saving all subsequent bytes until the end marker is detected

 NOTES
       this program does not include any timeouts to deal with delays in communication
