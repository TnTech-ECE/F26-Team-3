# <div align="center">Conceptual Design - Team 3</div>
<div align="center">Nicolas Campbell, Lucy Dunn, Sean Ottaway, Gabriel Simpkins, & Andrew Singletary</div>


## Introduction
&emsp; &emsp; Unmanned vehicles can be found all over the world being used widely to understand the environment they are being used in without using human resources. Because the environment is a big factor in all parts of the industry, there is a strong drive to improve these vehicles to withstand any condition. Data loggers gain such information about these different environments, but often they can only function on one type of vehicle, measure individual elements of the environment, or format information poorly. This causes inefficiency and higher costs to obtain this critical information.

&emsp; &emsp; To address these needs, Team 3 is conducting research and development to find a lower-cost, modular, and mass-producible data logger module able to obtain accurate time stamps and measure magnetic fields, temperature, pressure, and dynamic movement around these vehicles. Once this data logger obtains these measurements, it will be able to write this information in ULog formatting onto a microSD card to be easily understood and interpreted. This self-contained system will integrate five sensors, a microcontroller, and a power source while being mountable to unmanned vehicles and staying under $3,000 for the process of developing the module. This project is being developed for Valinor Dispatch to help with analysis of environments for various tasks of their unmanned vehicles and the health of these vehicles in these environments.

&emsp; &emsp; This proposal outlines the background of Data Loggers and a thorough evaluation of existing solutions. It will address the difficulties involved with such an embedded system and further elaborate on the need for this project. This will distinguish the restrictions on the data logger along with definitions of the measurements of success for the data logger. It will present the details of the budget, proficiencies of the team and assisting experts, the timeline with milestones of the project, and more about the stakeholder of this project, Valinor Dispatch. Finally, the proposal will end by discussing the implications of success and ethics concerns related to this data logger.


## Restating the Fully Formulated Problem
&emsp; &emsp; The objective of this project is to develop a low footprint and portable data logger for unmanned vehicles that can be attached to various types of drones and will record data onto an SD card. For data measurement, unmanned vehicles (UVs) typically only have an onboard IMU and do not have dedicated memory drives for data tracking. The Data Logger will be able to track IMU data, temperature, pressure, magnetic field strength, and log all of this data with absolute-time timestamps. Dedicated data logger units like this one exist only at high price points or high footprints. The Data Logger being designed in this project must be portable and easily transferable to any unmanned vehicles. A dedicated unit for data tracking will free up the UV to focus on navigation and achieve the task given to it while gaining more accurate data. This can help the user learn more about environments for future tasks of any UV with tasks in the same area.


### Specifications and Constraints:
&emsp; &emsp; Team 3's Data Logger (DL) has many specifications and constraints given by Valinor Dispatch as well as electrical and communication governing bodies required for the project. These specifications are to help Valinor evaluate the environments their unmanned vehicles are working in and help improve their vehicles based on the performance of them inside these environments. Here are the specifics for this DL project:


#### Specifications (Established by Valinor Dispatch)
1\.	Physical Attributes
 - The DL shall be less than 500g in mass
 - The DL shall be entirely self-contained
 - The DL shall be wallet sized (Approx. 4in x 3in x 1in.)
 - The DL may be easily attached to the outside of a UAS or UGV

2\.	Electronics
 - The DL shall have an onboard battery with enough charge to run multiple missions without being recharged
 - The DL shall record the following types of data
    - Acceleration and velocity
    - Magnetic field strength
    - Temperature
    - Pressure
    - Absolute time
 - The DL shall have an embedded LED active when data is being logged
 - The DL may use recommended MCU (STM32G474RET6) and JST connections for software updates and changes

3\.	Data
 - The DL shall write timestamped data onto an SD (or microSD) card in ULog format
 - Data shall be measured at a high enough resolution to be unimpeachable
 - The DL may follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers for this prototype


#### Constraints
1\.	General Operation Constraints
 - The DL project budget shall not exceed $3,000. This constraint was established by Valinor Dispatch in the initial project meeting.
 - The DL shall have a large operating temperature and pressure range (-20ºC ~ 60ºC). This constraint ensures that the DL will be able to operate under intense weather conditions and at higher elevations. A limited operating range would likely cause battery failure or sensor failure, resulting in partial/total loss in recorded data.

2\.	Standards and Safety Constraints
 - The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act. Hazardous materials could result in dangerous working conditions for Valinor Dispatch among other dangers to personnel working with the DL. [2]
 - The DL shall be subject to IP67 rating for Dust and Water resistance. Failure to comply with this constraint could result in permanent damage to critical DL systems and sensor failure, resulting in partial/total loss in recorded data. [4]
 - The DL shall conform to IEEE standards for thermal dissipation and handheld devices. Poor thermal dissipation can lead to dangers to personnel working with the DL or increased internal temperatures leading to permanent damage to critical DL systems and sensor failure, resulting in partial/total loss in recorded data. [3]
 - The DL shall ensure the PCB and battery are properly grounded, avoiding electrical shorts or shock. Shock could result in dangerous working conditions for Valinor Dispatch among other dangers to personnel working with the DL as well as permanent damage to critical DL systems, resulting in partial/total loss in recorded data. [5]
 - The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation. High voltage electronics can be a danger to personnel working with the DL and can increase the risk of electrical failures and shorts.


## Comparative Analysis of Potential Solutions
&emsp; &emsp; When looking at all the different ways to go about this project, there are ways that can be created from the bare bones, and there are some that can take an already existing solution and build it. This section shall hypothesize the possible solutions and present the benefits versus the disadvantages.

1\. The Bare Bones Model
&emsp; &emsp; This model includes picking out an MCU, IMU, GPS, Magnetometer, Pressure, and temperature gauge. The group would have to create the PCB to be mountable and able to use all these sensors using traces on the PCB. The group would also have to mount and use an onboard battery to power the system as well as an onboard charging system for the battery. In addition, an SD card reader is required to store the data being measured on the board. After mounting everything, the group would then have to use a MCU flasher to flash the program onto the CPU to let the CPU be able to talk to each individual sensor. On top of this, addition digital signal processing would be added to interpret the environment it is in using sensor fusion.
 - 	Benefits
    - The benefit of this system is that it would play heavily upon the electrical circuitry of the PCB which multiple group members have stated to be included in their strong suits. It also has the benefit of complete customization in the fact that the group would get to pick every single sensor that would be wanted for the specific purpose.
 - Disadvantages
    - The Disadvantage of this system is that if the company wanted to mass produce this product it would be increasingly difficult to have to source every single product to build the DL. Also, it would increase the amount of labor it would require the engineer to build the project.

2\. The Controller Add-On Model

&emsp; &emsp; This model would include the group using an already made controller module and manipulating it to have the capabilities of being a data logger. Also, addition sensors would usually need to be added to make it achieve Valinor's specifications. Team 3 would still develop a custom PCB to add these additional sensors that module does not have. The specific module that has been suggested to Team 3 is the ARK FPV Flight Controller. This flight controller module includes an MCU, IMU, Temperature, Pressure, Magnetometer, and microSD card. The suggested flight controller can be seen in Figure 1. [1]

*<div align="center">![Figure 1](https://hackmd.io/_uploads/H1xZcQjK2zx.png)</div>*
*<div align="center">Figure 1: The ARK FPV Flight Controller</div>*

1\. Benefits
    - The benefit of The Controller Add-On Model is that it is a faster and easier alternative to the bare bones model. Much less is needed to do to get this model completely functional. All that would be required is to develop a custom "Hat" PCB to hold the GPS and create a battery pack system and wire it to the Flight Controller. After this, Team 3 would be required to do some addition coding to get the new GPS sensor to work with the on-board MCU. This would make it much cheaper and faster for Valinor Dispatch if they would like to create many copies of this design. 

2\. Disadvantages
    - The disadvantage of this system is that it removes many aspects that make this project so unique. This can also limit how custom the DL can be. This route is great for the purpose of quantity and not as good for quality. This is not to discredit the chips found on the ARK Flight Controller as bad chips, but it would significantly reduce the customization of the DL. This also would mean that the project is limited by budget or capabilities of the sensors already incorporated into the flight controller. With this route, this project would be more focused on coding than engineering.

&emsp; &emsp; Looking at all the Benefits and Disadvantages for both Team 3 has decided it best to use both models and create The Bare Bones Model for the class project to be able to have a design project, and The Controller Add-On Model to supply Valinor Dispatch with the project scope desired by Valinor Dispatch. This benefits Team 3 because using the ARK flight controller utilizes previous code and wiring. This allows Team 3 to have a finished project for Valinor Dispatch if The Barebones Model gets stuck in the development.


## High-Level Solution
&emsp; &emsp; The goal of this project for Valinor Dispatch is to develop a self-contained module that records data from integrated instrumentation and seamlessly implements the module onto their existing unmanned vehicles. Another goal Team 3 has for this data logger is utilizing sensor fusion to interpret the data being obtained to have a better understanding of the environment before storing the data. This goal will be achieved separately from the final project that will be handed over to Valinor Dispatch to achieve their goals. 

&emsp; &emsp; The way Team 3 will maximize achieving Valinor's goal will be utilizing components, modules, and software that the company is already familiar with. This solution will incorporate equipment and software Valinor is already familiar with. This will reduce the amount of time and resources they will need to dedicate to making future adjustments to the module. To achieve Team 3's additional goals, the system will utilize widely available components paired with a commonly utilized MCU to help in the development process.

&emsp; &emsp; The requirements for the data logger going to Valinor Dispatch are to implement components that collect timestamps transmitted through GPS, measure magnetic field strength, ambient temperature and pressure, and vehicle acceleration. The data collected through these components is to be compiled and formatted to an SD card for Valinor Dispatch in ULog format. The module is going to be designed to run off its own battery and support USB-C charging capabilities. While a module can be developed from the ground up, Team 3 aims to follow the Controller Add-On Model for the final project being handed over to Valinor Dispatch utilizing the ARK Flight Controller. Figure 1 shows the model via a Hardware Block diagram that this module will be based off.

*<div align="center">![Figure 2](https://hackmd.io/_uploads/BkjNEjt3Me.png)</div>*
*<div align="center">Figure 2 – The Controller Add-On Model Block Diagram</div>*

Here is how the model in Figure 2 will be implemented for Valinor's data logger:
1. PCB
    - The PCB subsystem houses the GPS as well as the RGB LED. This will draw power from the Power System and communicate with the Microcontroller via serial communication. The PCB subsystem shall be small enough to fit with the ARK FPV Flight Controller. The PCB shall also isolate the GPS enough to where other sensors will not interfere with its operation.
2. ARK FPV Flight Controller
    - The ARK FPV Flight Controller will draw power from the Power System. The subsystem houses the microSD and all sensors onboard except the GPS. The ARK FPV will write data onto the microSD in ULog format and communicate with the PCB subsystem via serial communication. The ARK FPV shall be isolated from the sensors to avoid increased noise.
3. Power System
    - The Power System will regulate input power from a USB-C port and the battery while supplying the other systems with power. The Power System shall comply with grounding, shock, and hazardous material standards.

&emsp; &emsp; The requirements for the secondary module are going to be the same but include the sensor fusion goal utilizing digital signal processing through an embedded systems design. In addition, this module will be based on the Bare Bones Model presented previously in the section comparing the possible different models. Figure 2 shows the block diagram for the diagram based on the Bare Bones Model that Team 3 is designing from the ground up.

![Figure 3](https://hackmd.io/_uploads/SysF4iY2Gl.png)
*<div align="center">Figure 3 – Bare Bones Model Block Diagram</div>*

Here is how the model in Figure 3 will be implemented to achieve Team 3's additional goals:
Subsystems:
1. PCB
    - The PCB subsystem houses all sensors as well as the RGB LED. The physical PCB will also house the microSD and Microcontroller subsystems. This will draw power from the Power System and communicate with the Microcontroller via serial communication. The PCB subsystem shall be small enough to fit within housing smaller than 4 in x 3 in x 1 in. The PCB shall also isolate the sensors enough to where they will not interfere with each other’s operation.
2. Storage System and Data Analysis
    - The MicroSD will be housed on the physical PCB. The microcontroller will write data onto the microSD in ULog format. The microSD port shall be compliant with IP67 standards for dust and water resistance [4].  After writing onto the MicroSD card, the data will be analyzed, filtered, and smoothed to get clean data onto the microSD card.
3. Microcontroller
    - The Microcontroller will be housed on the physical PCB and draw power from the Power System. The microcontroller will write data onto the microSD in ULog format and communicate with the PCB subsystem via serial communication. The microcontroller shall be isolated from the sensors to avoid increased noise.
4. Power Systems
    - The Power System will regulate input power from a USB-C port and the battery while supplying the other systems with power. The Power System shall comply with grounding, shock, and hazardous material standards.

&emsp; &emsp; With these models in mind, most of the flow of the system will be similar between the different models. The operational flowchart to represent this flow can be seen in *Figure 4*. 

![Figure 4](https://hackmd.io/_uploads/rkOA4jYnzl.png)
*<div align="center">Figure 4 – Operational Flowchart for Team 3's Data Logger</div>*
*Similar to a block diagram, the flow chart aims to specify the system, but from the user's point of view rather than illustrating the arrangement of each subsystem. It outlines the steps a user needs to perform to use the device and the screens/interfaces they will encounter. A diagram should be drawn to represent this process. Each step should be represented in the diagram to visually depict the sequence of actions and corresponding screens/interfaces the user will encounter while using the device.*

&emsp; &emsp; While developing these systems, there have been constraints identified in the Specifications and Constraints section that will need to be followed in the development of these PCB systems. Team 3 plans to adhere to these constraints in the following ways:

Physical Attributes
- The DL shall be less than 500g in mass; The module will utilize multiple components as well as a battery all which are collectively under the weight limit. 
- Entirely self-contained; The DL shall be isolated and not interfere with vehicle communications or existing onboard components.
- Shall be approximately 4in x 3in x 1in; Due to the size of the components, this constraint will be achieved.
- Easily attached to the outside of a UAS or UGV; The DL will remain securely attached when mounted and will be designed to resist vibrations and shock.

Electronics
- The DL shall have an onboard battery with enough charge to run multiple missions without being recharged; An appropriate battery will be chosen that follows IEEE IEC 62133 safety requirements for portable rechargeable batteries as well as utilizing manufacturer specified charge cycles/ battery life expectancy. The battery will also be below the weight limit specified in the Physical Attributes constraints. 
- The DL shall record the following types of data... 
    - Acceleration and velocity
    - Magnetic field strength
    - Temperature
    - Pressure
    - Absolute time
    
The design will utilize the instrumentation and components necessary to achieve these goals.
- The DL shall have an embedded LED active when data is being logged; SMD LEDs will be incorporated into the design and will be tested extensively to prevent malfunctions abide by the specified constraint. 
- The DL may use recommended MCU (STM32G474RET6) and JST connections for software updates and changes; Extensive research and embedded systems designs will be tested to confirm the specified MCU will be compatible with the project. Standard JST connectors will be utilized.
Data
- The DL shall write timestamped data onto an SD (or microSD) card in ULog format; The team will research ULog formatting to confirm the data is being formatted and written correctly to the SD card as well as ensuring GPS timestamps are accurate.
- Data shall be measured at a high enough resolution to be unimpeachable; Extensive tests will be performed to ensure the data is correct.
- The DL may follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers for this prototype; The DL will not interfere with or transmit unwanted signals and comply with FCC regulations. 


General Operation Constraints
- The DL project budget shall not exceed $3,000; Components will be selected specifically to comply with the budget, also accounting for assembly and bench testing.
- The DL shall have a large operating temperature and pressure range (-20ºC ~ 60ºC);
  Extensive bench testing will be performed, so the module operates within the specified temperature and pressure ranges. Additional temperature regulation techniques may be implemented to obtain this objective. 


Standards and Safety Constraints
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act; [2]; Team 3 will ensure the components that are being utilized as well as the testing procedures will comply with the Federal Hazardous Substances Act.
- The DL shall be subject to IP67 rating for Dust and Water resistance; [4]; Team 3 will perform extensive testing to ensure the module is IP67 rated and will make adjustments to ensure the module will be IP67 rated. 
- The DL shall conform to IEEE standards for thermal dissipation and handheld devices; [3];  Team 3 will ensure the module conforms to IEEE standards and implement passive thermal management designs into the module.
- The DL shall ensure the PCB and battery are properly grounded, avoiding electrical shorts or shock; [5]; Team 3 will follow IEEE, NEC, and NFPA to ensure the module adheres to these standards. 
- The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation; Due to the low power consumption of both module versions, low voltage batteries will be utilized as well as following the design constraint listed in the Electronics constraint section.


## Atomic Subsystem Specifications
There will be 5 major subsystems that will be considered for these two modules. Such subsystems are as follows:
1.	PCB System
2.	Power System
3.	Microcontroller System
4.	Data Processing and Storage System
5.	ARK Flight Controller module
While the ARK controller will share some features, the ARK Flight Controller based module is going to have enough differences that Team 3 is separating it into its own subsystem. Here are some specifics on each of these subsystems.


### PCB Subsystem
&emsp; &emsp; The PCB will act as the foundation for the module and will be populated with the necessary instrumentation components as well as a power management system that accommodates battery charging. The PCB will be utilizing all types of signals as it holds all of the components. 

The primary components located on the PCB are as follows: 		
- Microcontroller (MCU): Shall process and interpret data from sensors, then formats and write data to the microSD card.
- Inertial Measurement Unit: Shall measure linear acceleration and interface with MCU
- GPS: Shall record time stamps received from GPS satellite connection and interface with MCU.
- Temperature Sensor: Shall read ambient temperature and interface with MCU.
- Pressure Sensor: Shall read ambient pressure and interface with MCU.
- Magnetometer: Shall measure the strength, direction, or relative changes of a magnetic field and interface with MCU.
- SD Card Reader/Writer: Shall accept data transmission from MCU after data is formatted to specification and write that data to the SD card.
- USB-C connector: Acts as the primary connector for the charging cable. Shall supply power through standard USB-C protocol to both the battery and components when cable is connected. The USB-C charging system shall comply with the safety constraints listed in the High-Level Solution section.


### Power System
&emsp; &emsp; The power system will handle power management throughout the PCB as well as the battery charging system. The primary interfaces will be the USB-C connector and the battery's JST connector. The USB-C will act as an input that receives power via external USB-C cable. The JST connector will act as both an input and an output as the battery will charge and discharge through this connector. 

&emsp; &emsp; A handful of small components will be integrated into the power system to manage power regulation as well as battery charging. A battery charger IC will be the primary component of the battery charging circuit and is responsible for managing power that is received from the USB-C connector and regulating that power to the battery. If the battery is charging, a red LED will be illuminated. If the battery is fully charged, the charging IC will stop charging the battery and the red LED will turn off. A 3.3V regulator will be the primary component for voltage regulation throughout the PCB as most of the onboard components have an operating voltage range of 3.3V. Smoothing capacitors will be placed along the power traces to filter high frequencies. *Figure 5* shows the ideal battery charging flowchart.

*<div align="center">![Figure 5](https://hackmd.io/_uploads/BJqqditnzx.png)</div>*
*<div align="center">Figure 4 – Charging System</div>*


### Microcontroller
&emsp; &emsp; The microcontroller chosen for this project is the STM32G474RET6. This microcontroller will allow for the reading of all attached sensors as well as writing the data from these sensors out to the microSD through ULog format. The firmware needed for this subsystem will be written in C and designed using the STM32CubeMX software.

The firmware needed for this program will have 5 parts:
1. Setup
    - This section will initialize all the peripherals needed. It will also initialize each of the four tasks needed and the ring buffer required for the logger task. It will also handle mounting the microSD card.
2. Sensor Task
    - The sensor task will read the data coming from the sensors at regular intervals and push the data to the next task for analysis.
3. Analyzer Task
    - This task will take the data analysis curated by Nic through the Storage System and Data Analysis subsystem and implement it on the microcontroller before pushing the now processed data to the logger.
4. Logger Task
    - The logger task takes the processed data from the analyzer task and writes it out in ULog format to the microSD card. A ring buffer is used to keep the sensor and the logger from interrupting the other’s timing and throwing each other off balance.
5. Supervisor Task
    - This task determines when and if the logger should be actively writing out or not based on a few different factors. It checks if the microSD card has been inserted and has power, if so it tells the logger to write out, if not it flushes the buffer to keep it from getting full of old data. 


### Storage System and Data Analysis 
&emsp; &emsp; The MicroSD will take the data given to it in ULog format, which on the microSD card will be a single, continuous train of binary data directly from the microcontroller. This data will be in the exact same format that the microcontroller will see. All this data will be raw binary data and will need to be put into some kind of converter to be understood by humans. The benefit of the ULog format though is where it is binary, it does not take up much space. This helps give a heap of data in a small package. To make it able to be read by a human, it will have to be converted to CSV (Comma Separated Variables), by using python. Then this data can then be put into understandable graphs using MATLAB.

&emsp; &emsp; After getting graphs, this subsystem will also take the raw and unfiltered data and smooth it out to make it easily read by a consumer. This will be done with DSP (Digital System Processing). The DSP will include filtering out any high frequency noise and isolating the true system states.  By using PIDs and other Software filters, there shall be a Dynamic Transfer function that will then be flashed onto the MCU at the Analyzer Task.  This process may be repeated as many times as needed to get clean data from the DL.


### ARK FPV Module Subsystem
&emsp; &emsp; With this subsystem, this will be a system that is separate from the other subsystems when relating it to the Bare Bones Model. That said, all these elements will also be a less complicated version of each of their subsystems to allow the flight controller to achieve the same tasks without the data processing desired for the Bare Bones module. While it will contain many similar components, there are important changes that are required to get the ARK Flight Controller system to data log like the Bare Bones Model but stay within the scope that Valinor has established for their Data Logger. 

&emsp; &emsp; One of the major changes is that Team 3 will be developing a separate PCB board to work with the ARK controller to achieve the goal of being a data logger. This means that there will be a need to utilize traces to connect to JST-GH ports to connect the ARK controller to the PCB to provide power and transmit data from the GPS to the microcontroller. Specifically, there will be a JST-GH 3 Pin connection for power and a JST-GH 6 Pin connection for the GPS. The PCB will also need to house the battery providing power for the system. The GPS will need to have a voltage regulator like the Bare Bones Model to step down the 5 V that is going to come from the ARK controller to 3.3 V. Lastly, to mount the PCB to the ARK controller, Team 3 will be utilizing standoffs for this purpose.

&emsp; &emsp; Another major change is related to the power system. It will still utilize the same flow as indicated in Figure 4, but the battery that will be utilized for this system is going to be on the PCB separate from the charging ports that are on the ARK controller. It is also important to note that the battery for the ARK controller will need to be upgraded to 5 V instead of 3.3 V for the Bare Bones Module to accommodate the needs of the flight controller. With these differences, this module will still use the same battery charging and power regulation components as the Bare Bones' power system.

&emsp; &emsp; The last major change is that the ARK controller utilizes the STM32H743IIK6 microcontroller in comparison to the STM32G474RET6. This Microcontroller has significantly faster speeds, more memory, and more pins to utilize; however, these features are not important since the goal is the same if not simpler for this module in comparison to the Bare Bones Module. Also, since there are more pins on the ARK, but they are already assigned to specific ports on the controller, the custom drivers programed for the data logger will need to change to reflect the differences between the microcontrollers. With this, it is simpler since this module is not going to be doing the sensor fusion like the Bare Bones module.

&emsp; &emsp; With all these changes, Team 3 will be able to separately develop a module for Valinor that utilizes the ARK Flight Controller that they commonly use for the data logger they are looking for Team 3 to develop, while Team 3 can further develop a data logger to achieve the additional goals set by the team.


## Ethical, Professional, and Standards Considerations
&emsp; &emsp; Due to the rising issue of public trust with data collecting technology, a device such as this DL measuring environmental conditions and saving this data could pose global and societal implications. While the DL is only used to collect information about the environment and collects time stamps regarding the autonomous vehicle, the sensors the DL utilizes might lead to public distrust as the sensors can be implemented to collect unsolicited information. These implications are not as important since the DL will not be widely available for this to occur. 

&emsp; &emsp; A device such as this DL contains and implements various modules that can potentially be used for intrusive surveillance. This could further influence the modern and ongoing public trust issues that are present within the tech industry in terms of selling private information. With this DL, any extra "features" that could be added to the DL might bring ethical issues such as using GPS tracking for purposes outside the DL's scope as well as sensitive location data logged by the DL. Team 3 will heavily consider this in the way the DL will be programmed.

&emsp; &emsp; Environmental implications would cover the operations and carbon footprint of the manufacturing process for the DL. This DL uses special sensors and components that are manufactured using semiconductors and other materials. Accessibility to these components could pose an issue with few locations being able to manufacture and procure these semiconductors found in the DL. Team 3 will avoid this issue by using components that are readily available and manufactured from trusted and well-known companies to prevent addition difficulties from obtaining more obscure materials. Another potential issue would be the module detaching from the vehicle during operation, potentially disrupting terrestrial and aerial life as well as their environments. To prevent this, this DL will have the capability of using M4 screws via the screw mounts in this DL to keep the module from affecting wildlife and the environment.

&emsp; &emsp; In terms of economic implications, choosing and pricing components come into play. As engineers, Team 3 needs to come up with a good and economical price to return on investment value to deliver the best piece of hardware for the right cost. If the sensors and components are too cheap, there might be issues with reliability for the DL, causing complications for Valinor and the vehicles utilizing them. If the project is too expensive, Valinor Dispatch would lose their investment in the development of this module. This will be a major focus for Team 3 to keep the DL inexpensive while still utilizing trusted technology to meet the specifications.

&emsp; &emsp; With the development and planning of this module, there are important ethical considerations when it comes to the operation and implementation of the DL. The team of engineers responsible for the development of this project must consider the previously mentioned implications and adhere to the following ethical standards:
- Team members who are responsible for the software will program the modules to only capture data within the project scope.
- Team members who are responsible for hardware will construct and develop the DL to comply with basic safety standards as well as staying within project scope.

&emsp; &emsp; In summary, Team 3 will be developing this DL with success being measured based on these considerations, the specifications, and the measures of success listed in this document. When it meets all these standards, it will bring the promised benefits also listed and fulfill Valinor Dispatch's request for the DL, which will demonstrate innovation through Team 3's development of this project.


## Resources
The resources required for this project can be categorized in three ways: budget, labor, and timeline. Within these, the budget will specify what the expected costs are for each subsystem as well as the total expected cost for the project. The division of labor will clarify the team’s areas of expertise and how each member is going to contribute moving forward. The expected timeline will also be proposed, indicated using a Gantt Chart specifying the tasks needed to complete the project as well as when they are expected to be completed.


### Budget
PCB Design

&emsp; &emsp; This system contains the necessary PCB, along with its basic circuitry that will contain the capacitors, resistors, and other components necessary for its functionality. It also contains a pressure gauge, magnetometer, IMU, GPS, and digital temperature sensor. These parts were carefully chosen due to the specific needs and requirements of our DL and have been compared against our weight and area constraints.
- PCB: $50
- Pressure Gauge: $3
- Magnetometer: $3
- IMU: $4
- GPS: $12
- Digital Temperature Sensor: $6
Subsystem Total: $78


Power System

&emsp; &emsp; This system utilizes a Jauch Quartz LP705176JS 3.7V 3.15mAh battery. This battery was chosen as it satisfies the voltage needed for the STM32 microcontroller as well as the other power constraints needed for the PCB and it’s parts. The part itself will be utilized to supply power to the PCB, microcontroller and all other parts of the DL.
- Battery: $22
Subsystem Total: $22


Microcontroller 

&emsp; &emsp; This system utilizes a STM32G474RET6 microcontroller. This chip will be used to read data off of the various sensors that have been implemented on the PCB and will write out data to the MicroSD card at regular intervals. This specific chip was recommended by Valinor Dispatch to Team 3 and was chosen after careful consideration. Using the STM32 will also require the use of a programming cable and the one chosen for this project is the STLINK-V3MINIE. This chip was chosen at the recommendation of Valinor Dispatch and is commonly paired with the STM32 microcontroller. The connector cable required for the STLINK-V3MINIE is the TC2030-CTX-NL-STDC14 cable which will connect the PCB to the STLink for debugging purposes.
- STM32G474RET6: $10
- Programmer: $25
- Programming Cable: $50
Subsystem Total: $85


Storage System

&emsp; &emsp; This system contains the elements required to store data for the DL. It consists of the MicroSD card reader that will be located on the PCB as well as the MicroSD card itself. The MicroSD card reader chosen for this project is the Same Sky MSD-3-A. This part was chosen due to it’s size, weight, and cost as the most effective option. It features the ability to auto-eject out, allowing for easy removal of the MicroSD card.
- MicroSD Card Reader: $1
- 256GB MicroSD Card: $50
Subsystem Total: $51


ARK Flight Controller Variant 

&emsp; &emsp; This system will have its own separate GPS which will be contained on a PCB that will be connected and working in tandem with the ARK Flight controller. This system will also have its own battery separate from the rest of the project. The flight controller chosen for this project is the ARK FPV Flight Controller, this board was chosen as the recommendation of Valinor Dispatch as well as compared against similar models. This board was chosen over it’s competitors for its simplicity, reliability, and price point. The battery chosen for this project is the 1200mAh 7.4V 2S LiPo battery. This battery is commonly used to power drones and satisfies the ARKs needed 5.5V power consumption benchmark. The GPS chosen for this system is the same as was chosen for the Bare Bones Module, see above for the justification. This system will use the same debugger STLINK and cable as seen in the Microcontroller Subsystem above.
- ARK FPV Flight Controller: $200
- GPS: $12
- PCB: $50
- Battery: $26
Subsystem Total: $288


Total Budget

&emsp; &emsp; The total overall proposed budget for Team 3’s Data Logger is $524. As seen above these components have been chosen intentionally to work well together and result in a well rounded Data Logger that successfully reads and writes out data onto a MicroSD card using two separate board styles.


### Division of Labor
The members of Team 3 and their skill sets are as follows:
- Nicolas Campbell: 
    - Skills: CAD, Circuitry, Control Systems, LabVIEW, System Health Analysis
- Lucy Dunn:
    - Skills: Assembly, C/C++, LTSpice, Soldering, VHDL
- Sean Ottaway: 
    - Skills: C/C++, Circuitry, KiCad, Mechanical Systems, PCB Design
- Gabriel Simpkins: 
    - Skills: C/C++, Circuit Analysis, Microcontroller Processing, Soldering
- Andrew Singletary:
    - Skills: C/C++, Circuit Analysis, Microcontroller Processing, Signal Processing

Based on these skills the subsystems and their designated members have been divided as such:

&emsp; &emsp; Sean Ottoway will be in charge of the PCB design as he is well versed in KiCad and has experience in designing PCBs from scratch. All team members have joined him in researching components for this PCB and clearing them with Sean throughout the design process. His main responsibility will be designing the PCB from scratch as well as assembling it once received.

&emsp; &emsp; Nic Campbell will be taking care of the Storage System and Data Analysis as he has a specialty in control systems engineering. Through this subsystem he will be working mainly with the MicroSD as well as how the firmware filters and interprets the data it receives from the sensors.

&emsp; &emsp; Lucy Dunn will be over the microcontroller and therefore the firmware stored on it. She has been given this subsystem as she is the most versed in coding and has had experience in embedded systems as well as computer design. She will be writing the software and designing the firmware that will go on the STM32 microcontroller.

&emsp; &emsp; Gabe Simpkins will be in charge of the Power System he is skilled in circuitry and is able to look at the PCB design and components chosen and determine the power, voltage, and current necessary for the overall design of the Data Logger. He will be checking that the batteries chosen perform up to standard and expectation as well as ensuring that each component is getting the power it needs to perform properly.

&emsp; &emsp; Andrew Singletary will be working on the ARK Flight Controller as he has a very wide span of knowledge that allows him to see and understand this controller from many different angles including coding as well as signal processing. His main responsibility will be writing the code needed for the ARK to function as needed as well as any other issues that might arise with the flight controller.


### Timeline
![timeline](https://hackmd.io/_uploads/BJ5acoK3fl.png)


## References
[1] “ARK FPV | ARK Documentation,” Arkelectron.com, Oct. 21, 2026. https://docs.arkelectron.com/products/flight-controller/ark-fpv (accessed Oct. 23, 2026).

[2] “Federal Hazardous Substances Act (FHSA) Requirements,” CPSC.gov, Apr. 04, 2016. https://www.cpsc.gov/Business--Manufacturing/Business-Education/Business-Guidance/FHSA-Requirements (accessed Oct. 09, 2026).

[3] IEEE, “Handheld Devices,” IEEE Technology Navigator, 2026. https://technav.ieee.org/topic/handheld-devices/ (accessed Oct. 22, 2026).

[4] International Electrotechnical Commission, “IP Ratings | IEC,” www.iec.ch, 2024. https://www.iec.ch/ip-ratings (accessed Oct. 21, 2026).

[5] National Fire Protection Association and National Fire Protection Association. National Electrical Code Committee, "Article 250," NEC 2017: NFPA 70 National Electrical Code. Quincy, Ma: National Fire Protection Association, 2016.

## Statement of Contributions
Nicolas Campbell: Operational Flowchart, Comparative Analysis of Potential Solutions, Storage Systems and Data Analysis

Lucy Dunn: Resources, Microcontroller Subsystem

Sean Ottaway: High Level Solution, PCB Subsystem, Ethical Considerations

Gabriel Simpkins: Fully Formulating the Problem, Hardware Diagram

Andrew Singletary: Introduction, High Level Solution, & the ARK based Subsystem