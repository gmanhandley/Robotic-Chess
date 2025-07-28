# Robotic-Chess
This is our progress on creating a physical board for two-player remote chess matches.
The idea is to make three boards within a budget of $1000 and 30 days.
This project is very much a work in progress but I am updating it with information, diagrams, and code as I work through it.

## What is it?
The goal of this project is to have to 2 chess boards that roboticaly move pieces based on opponent actions and communicate through a private central server.
The main mechanical system of each board is a coreXY gantry operated by two stepper motors and a belt and pully system.
The movement of pieces is done through a magnet under the board and zinc bottom plated pieces.
The electrical system requires a direct outlet connection with an AC-DC converter to output 12V 5A and buck converter to reduce to 5V 5A.
The piece detection is an array of photodiodes controled by an arduino mega. we will have the circuit diagram posted for the array and power system posted seperate.
The brains of the system is a raspberry pi zero 2W. This communicated with the central server through ssh and the arduino through serial.
There is a button to end your turn afterwhich the arduino reads the photoresistor array to determine covered tiles and sends the information to the ras pi which sends everyting off to the central server.
The central server then determines which piece moved where and sends that information to the opponents board where the the piece is then moved.
The cycle continues until one player wins.

## Mechanical Systems
### The Gantry
The mechanical system was the first portion of the project to be planned out. From the start we knew that we wanted the system to work by using a magnet on a gantry beneath the board to drag the pieces on the other side.
From here we needed to decide on how we wanted the gantry system to work.
We decided that we wouldnt try and reinvent the wheel and browsed a few different systems used commonly in 3D printers.
After looking through a our options, we settled on using a core-XY system which I have provided a diagram for below.
We chose this system because all of the brackets could be easily 3D printed and both of the motors were on the same side which I will explain the importance of shortly.
Given that printer fillament is much cheaper that buyable brackets and wood, anything that could be 3D printed was.
Doing this also gave lots of creative freedom on how parts could look as well as addition functionality in places where it was needed.
Before I talk about the brackets that I made, I should talk about how the core-XY system actually works.
#### How does it work?
The diagram that I provided is top down view and shows how things allign in the XY-plane but we need to focus on the Z-axis to understand it fully.
Each black circle in the diagram is actually a stack of pullys and the colored lines are drive belts.
Each pully stack consists of two pullys, one toothed and the other smooth, as well as three small washers to prevent rubbing.
Which pully goes on top or bottom depends on how the system is set up, but the the toothed pullys interact with the toothed side of the belt and the smooth pullys interact with the smooth side.
The red and blue lines are drive belts that sit at different positions on the Z-axis and only interact with the pullys on that plane.
So the drive belt on bottom interacts only with the pullys on the bottom of each stack and vice versa.
Where the belts cross at the top, they do not collide but cross over or under each other.
<img width="520" height="552" alt="Image" src="https://github.com/user-attachments/assets/09db13cd-5efd-45a4-b1ca-fb58bdc8525f" />
#### The Brackets
There are a total of four different brackets that I needed to design and print.
The bracket for the y-axis rails, x-axis rail, and each corner bracket.
I started with the y-axis brackets as they could be used to hold the rails together for a physical representation.
These brackets had two main purposes, to hold the x-axis rail in place and to house a couple pully stacks.
I went through a couple iterations to find what worked best for our needs, and ended up with a design that effectively hung the x-axis rail from the bottom of the y-axis rails.
This was necessary because we bought a premade chessboard and didnt have enough clearance and we need to leave clearance for the magnet mechanism.
This did add height but it turned out to be a good thing by the end of the project.
I have provided the solidworks files in this page so anyone can use and modify to their needs as well.

### Magnetic Activation

## Electrical System

## Embedded Systems

## Backend Software
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
