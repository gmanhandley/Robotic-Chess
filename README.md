# Robotic-Chess
This is our progress on creating a physical board for two-player remote chess matches.
The idea was to make three boards within a budget of $1000 and 30 days starting on June 18, 2025.
By the end of the 30 days we are $46 under budget with one board mostly assembled and the 
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
Next I designed the corner brackets which had the jobs of keeping the y-axis gantrys from slipping off the end of the rail and housig two more critical pully stacks each.
These parts turned out to be more intricate that I originally though becase the pullys need to guide the belts in very precise ways that kept them from rubbing and colliding with other pullys and other belts.
This was a game of measuring distances from reference locations and very tedious work in my experience.
However, I did manage to create a bracket that needed no revisions and all belts and pullys were clear of each other.
Thankfully I only had to crate one bracket and then I could mirror it to create the opposite corner bracket.
The x-axis bracket is not done yet and needs to be modified to incorporate the magnet mechanism.
I have provided the solidworks files in this page so anyone can use and modify to their needs as well.

### Magnetic Activation
The next mechanical problem to solve was grabbing the pieces with a magnet when we need to and letting go of them when we dont.
The obvious choice you would think would be an electromagnet.
However, strong enough electromagnets are expensive and large which made them a quite unappealing choice.
With this realizeation we looked into other types of magnets and landed on some rare-earth magnets.
We found this awesome rare earth magnet retailer called [K&J Magnetics](https://www.kjmagnetics.com/) which had a really usefull tool that showed the theoretical pull force based on magnet shape and distanc from the magnet.
Using this tool and some measurements we landed on using a stack of ring magnets that we would raise and lower with a rack and pinion system.
This is the final mechanical solution that has not been finished and I will add the details as well as solidworks files when it is finished
https://www.kjmagnetics.com/

## Electrical Systems
### Power System
For this project we used a ras-pi-2W-zero for network connectivity and an arduino-mega as our microcontroler for the detection system and motors.
The ras-pi needs 5V and around 2.5A while the arduino has a couple options for power that we were able to choose from.
For the arduino we needed to leave the USB availiable to connect to the ras-pi and we needed the 5V rail on the arduino to connect to the stepper motor drivers.
These factors left us with using the barrel jack for power which require a 12V input.
In additon to the ras-pi and arduino, we also needed to power the stepper motor drivers that controled the gantry which thankfully were able to run off of 12V as well.
This created a clear need for some sort of voltage regulation within the power system so I did some research into different ways to regulate voltage and found to main methods.
One was using a step up regulator to go from 5V to 12V but that would heavily limit the current on the 12V rail.
The other was using a buck converter to step the voltage down from 12V to 5V which didnt have as drastic an effect on current.
I chose to use a buck converter bacause I had more electronics on the 
I chose to go for a nice and plentiful 10A of current to ensure there was ample power in the case of power spikes and multiple operations ahappening at once.
### Piece Detection
### Motor drivers

## Embedded Systems

## Backend Software

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
