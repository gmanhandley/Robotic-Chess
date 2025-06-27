# Robotic-Chess
This is our progress on creating a physical board for two-player remote chess matches.
The idea is to make three boards within a budget of $1000 and 30 days.
This project is very much a work in progress but I am updating it with information, diagrams, and code as I work through it.

The goal of this project is to have to 2 chess boards that roboticaly move pieces based on opponent actions and communicate through a private central server.
The main mechanical system of each board is a coreXY gantry operated by two stepper motors and a belt and pully system.
The movement of pieces is done through a magnet under the board and zinc bottom plated pieces.
The electrical system requires a direct outlet connection with an AC-DC converter to output 12V 5A and buck converter to reduce to 5V 5A.
The piece detection is an array of photodiodes controled by an arduino mega. we will have the circuit diagram posted for the array and power system posted seperate.
The brains of the system is a raspberry pi zero 2W. This communicated with the central server through ssh and the arduino through serial.
There is a button to end your turn afterwhich the arduino reads the photoresistor array to determine covered tiles and sends the information to the ras pi which sends everyting off to the central server.
The central server then determines which piece moved where and sends that information to the opponents board where the the piece is then moved.
The cycle continues until one player wins.

We want to talk about why some of these choices were made during the planning for this project.
The reason we chose to use a coreXY gantry is because it is well documented with the rise of 3D printing and relatively simple to build.
Another benfit to this system is its versitile shape meaning it can be planar or stacked depending on the system you are making.
We chose a stacked configuration and made some custom modeled and printed brackets to save money. We will post all STL files used in the project.
The reason behind using a photoresistor array for piece detection is because it cheap and effective. Having a piece on top of one will change the measured value ouput by that photoresistor.
We then use software to determine if a space is occupied.
The photoresistors are inset to the board with the wiring beneath to keep everyting clear of the pieces moving on top.
A camera detection system may be easier to implement, however we wanted everthing contained internally for a cleaner look.
We used and ras pi zero 2W because they are cheap and can have an internet connection for communication with other devices.
They also have some GPIO pins that could be used if needed, however we do not for the project as it is now.
We use an arduino mega because it has enough analog input pins as well as a low power requirement.
We are using a central server because the ras pi chosen has very little processing power and a server was already available for use at no additional cost.
If the server were not already availiable we would have chosen ras pi with more processing power to aavoid a pricey server.

There are many parts to this project, and with that there are even more learning opportunities.
As computer engineering and computer science students, creating the mechanical system proved very challenging with the creation of custom brackets and introduction to new mechanical systems.
The electrical and power system were also very imformative and required much research into aviliable electrical components.
The networking and communication between a server multiple ras pi boards and microcontrollers is integral in getting the multiplayer aspect of the game to work.
The embedded software for controlling the stepper motors and reading the sensor array provided experience in C++ and using microcontrollers.
The server program is currently under development.

The benefit of having a system like this is being able to have a physical board in front of you.
While this is certainly less convienient than using digital solutioons like chess.com, it is pretty cool to see the pieces magically move in front of you as the game progresses.
Ther are many things that we considered doing for this project but were cut for lack of time or budget.
Perhapse the largest cut features were an internal rechargable battery and a screen to display relevent information during each turn.
