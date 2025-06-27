# Robotic-Chess
This is my progress on creating a physical board for two-player remote chess matches.

The goal of this project is to have to 2 chess boards that roboticaly move pieces based on opponent actions and communicate through a private central server.
The main mechanical system of each board is a coreXY gantry operated by two stepper motors and a belt system.
The movement of pieces is done through a magnet under the board and zinc bottom plated pieces.
The electrical system requires a direct outlet connection with an AC-DC converter to output 12V 5A and buck converter to reduce to 5V 5A.
The piece detection is an array of photodiodes controled by an arduino mega. I will have the circuit diagram posted for the array and power system posted seperate.
The brains of the system is a raspberry pi zero 2W. This communicated with the central server through ssh and the arduino through serial.
There is a button to end your turn afterwhich the arduino reads the photoresistor array to determine covered tiles and sends the information to the ras pi which sends everyting off to the central server.
The central server then determines which piece moved where and sends that information to the opponents board where the the piece is then moved.
The cycle continues until one player wins.

The benefit of having a system like this is being able to have a physical board in front of you.
