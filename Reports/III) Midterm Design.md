# <div align="center">Midterm Design Document - Team 3</div>
<div align="center">Nicolas Campbell, Lucy Dunn, Sean Ottaway, Gabriel Simpkins, & Andrew Singletary</div>


## Introduction
&emsp; &emsp; Unmanned vehicles can be found all over the world being used widely to understand the environment they are being used in without using human resources. Because the environment is a big factor in all parts of the industry, there is a strong drive to improve these vehicles to withstand any condition. Data loggers gain such information about these different environments, but often they can only function on one type of vehicle, measure individual elements of the environment, or format information poorly. This causes inefficiency and higher costs to obtain this critical information. 

&emsp; &emsp; To address these needs, Team 3 is conducting research and development to find a lower-cost, modular, and mass-producible data logger module able to obtain accurate time stamps and measure magnetic fields, temperature, pressure, and dynamic movement around these vehicles. Once this data logger obtains these measurements, it will be able to write this information in uLog formatting onto a microSD card to be easily understood and interpreted. This self-contained system will integrate five sensors, a microcontroller, and a power source while being mountable to unmanned vehicles and staying under $3,000 for the process of developing the module. This project is being developed for Valinor Dispatch to help with analysis of environments for various tasks of their unmanned vehicles and the health of these vehicles in these environments.  

&emsp; &emsp; This proposal outlines the background of Data Loggers and a thorough evaluation of existing solutions. It will address the difficulties involved with such an embedded system and further elaborate on the need for this project. This will distinguish the restrictions on the data logger along with definitions of the measurements of success for the data logger. It will present the details of the budget, proficiencies of the team and assisting experts, the timeline with milestones of the project, and more about the stakeholder of this project, Valinor Dispatch. Finally, the proposal will end by discussing the implications of success and ethics concerns related to this data logger. 


## Formulating the Problem
&emsp; &emsp; For data measurement, unmanned vehicles (UVs) typically only have an onboard IMU and do not have dedicated memory drives for data tracking. The Data Logger will be able to track IMU data, temperature, pressure, magnetic field strength, and log all of this data with absolute-time timestamps. Dedicated data logger units like this one exist only at high price points or high footprints. The Data Logger being designed in this project must be portable and easily transferable to any unmanned vehicles. A dedicated unit for data tracking will free up the UV to focus on navigation and achieve the task given to it while gaining more accurate data. This can help the user learn more about environments for future tasks of any UV with tasks in the same area. 


### Background
&emsp; &emsp; Recording data for environments is critical for consistent operations. Recorded environmental data can help businesses learn more about potential hazards and environmental changes to impact the success of any UV sent to do simple or difficult tasks in those environments. Data like this can inform critical decision-making for the desired task to get done. These can also be important to keep data points for simulation purposes to improve UV designs. These data points (IMU data, temperature, pressure, magnetic field strength) would specifically make simulations of any UV environments more accurate, which influence decisions of how to improve maneuverability control, task management in harsh environments, and other design choices like for UAVs [1].

&emsp; &emsp; So what happens if there is errors in the data stored related to these environments? If, for example, data related to rough terrain and harsh environments is not the same as the data being written on SD cards, then this information stored on the SD card could lead to ill-informed decisions related to military uses or any other business utilizing UVs [2]. This means the quality of the Data Logging system on any unmanned vehicles is important to prevent these issues. This is why decisions to use Consumer-Grade equipment for Data Logging because of monetary concerns sometimes lead to major errors that are not easy to fix without running another separate trip to confirm the data being recorded and check the functionality of the Data Logging system, which is highly inefficient [2].

&emsp; &emsp; Designing a product that meets all the criteria provided for this project requires a knowledge of sensors, embedded systems, MCUs, and PCB design. Some specific topics related to these areas are sensor fusion, data denoising, and understanding of serial communication, which include Inter-Integrated Circuit (I2C) and Serial Peripheral Interface (SPI). Here are some specifics on these topics. 

1. Sensor Fusion

&emsp; &emsp; With this data logger utilizing multiple types of sensors all at once, it is possible to implement a data logger with the information from each sensor is processed separately. That said, Sensor Fusion is another approach that can be utilized. The idea of Sensor Fusion is to process all the data from separate sensors to make one coherent picture. For example, autonomous vehicles utilize this technique to combine the information from a camera and a lidar to give the vehicle a more complete understanding of the environment around it [3]. The benefit of having a more complete picture rather than having individual data is that the vehicle can make better informed decisions like avoiding obstacles and interpreting green vs red on a traffic light.

&emsp; &emsp; Because of this big benefit, Team 3's DL will be utilizing Sensor Fusion as a form of Digital Signal Processing by combining the information of all sensors together to form a picture of the type of environment that the vehicle the DL is mounted to is in. This will make Team 3's DL distinguish itself from other data loggers on the market. 

2. Data Denoising

&emsp; &emsp; Data denoising is extremely important to be able to use data coming from any of the sensors on a data logger since there is always some noise present in every signal whether it is desired or not. This means that Team 3 will need a method to handle the noise.  

&emsp; &emsp; One method of Data Denoising is using Deep Learning to distinguish between noise and desired data by comparing the received data to predetermined sets of noise to separate noise from the actual data [4]. This method is often used to help further develop Artificial Intelligence among other applications. 

&emsp; &emsp; Another method is utilizing filters like a Low Pass Filter or Band Pass Filter to eliminate noise that is outside a specified region for signal. This technique would utilize hardware like RLC circuits to remove the undesired signal manually rather than using processing to remove the signal. While this is simpler to set up on a data logger, the con to utilizing this method is the range is set and cannot change without changing either the resistor, capacitor, or inductor used for the filter. This will be an important consideration during the development of the DL. 

&emsp; &emsp; One last method that can be utilized is setting up a model that represents what noise may look like based on previous knowledge of the sensor rather than using a specified data set to remove the noise element of the data. For example, Hyperspectral Image (HSI) denoising can use characteristics of the image to inform the model what the noise will look like [5]. 

3. Serial Communication

&emsp; &emsp; Serial communication is one of the most important parts of a data logger since it is required for a microcontroller to communicate with an individual sensor or especially with multiple sensors at the same time. There are many different protocols that can be used for serial communication, but here are some of the most commonly utilized. 

&emsp; &emsp; The first commonly used protocol is the Universal Asynchronous Receiver/Transmitter (UART) driven communication. This protocol uses two pins using one of them to transmit data (Tx) and the other pin the receive data (Rx). This protocol is often used for its simplicity to allow devices to communicate and notoriety. This protocol does struggle to do more complicated communication since it does not utilize a clock to sync data. [6] This would significantly limit the ability of a data logger to sync data from multiple sensors at once. This is why it is not very often used specifically for sensors. 

&emsp; &emsp; The next commonly used protocol is the Inter-Integrated Circuit (I2C) protocol. This protocol also utilizes two pins for communication, but instead of using them for transmitting and receiving over separate pins, I2C uses one pin as the clock to sync communication (SCL) and the other for transmitting data bidirectionally between devices (SDA). It also uses specific addresses to identify devices rather than just doing it automatically like UART does. This allows for Plug & Play capabilities while still being simple. That said, the speed of this protocol is limited since it is putting many functions on only two pins, which means less data can be transmitted at a time [7]. 

&emsp; &emsp; Another commonly used protocol is Universal Serial Bus (USB). This is the most widely used across all industries for its versatility. It can be used for power and for data transfer at the same time. It is extremely common for any handheld device in general. While it is like the UART protocol, it gets faster speeds for communication, but it requires a powerful driver to act as a master for the bus in comparison to I2C, which limits the Plug & Play functionality with smaller devices like sensors [8]. 

&emsp; &emsp; The last commonly used protocol is the Serial Peripheral Interface (SPI) protocol. This protocol differentiates itself the most since it uses four pins for communication: One for transmitting data as the slave and receiving data as the master (MISO), the second to do the opposite (MOSI), the third to act as the clock syncing the devices (SCK), and the fourth as the indicator of the device as slave or master (NSS). Being able to separate these functions through four pins makes the protocol faster than I2C since it can delegate all the tasks I2C does over more pins. That said, SPI does not have fixed standards, which can lead to some issues with systems developed separately not being able to communicate properly [9].

&emsp; &emsp; After looking at all these protocols, it is apparent that the data logger will need to utilize I2C, USB, & SPI to be able to achieve the final goal. This is possible since microcontrollers in the modern day have multiple pin sets that can be utilized for each protocol to operate at the same time. This allows Team 3 to have more options when looking for the desired sensors for the data logger that Team 3 is developing. 

&emsp; &emsp; With all this background information, Team 3 will be able to develop a data logger, but this project will have to meet several specifications and constraints set by Valinor Dispatch, governing bodies, and the team. While there are other comparable solutions, many fall short of the desired specifications of this project and achieve all these topics. These alternative solutions are taxing on the budget, don’t measure all the required data, don’t store the data to be observed in the future, or do not achieve all the important principles listed above. In addition, they are often not portable and transferable to other types of UVs without modification. With this background, Team 3's Data Logger will aim to achieve these goals, but what are all the specifications for this project. 


### Specifications and Constraints
&emsp; &emsp; Team 3's Data Logger (DL) has many specifications and constraints given by Valinor Dispatch as well as electrical and communication governing bodies required for the project. These specifications are to help Valinor evaluate the environments their unmanned vehicles are working in and help improve their vehicles based on the performance of them inside these environments. Here are the specifics for this DL project: 


##### Specifications
1\.	Physical Attributes
- The DL shall be less than 500g in mass
- The DL shall be entirely self-contained
- The DL shall be wallet sized (Approx. 1in x 3in x 4in.)
- The DL may be easily attached to the outside of a UAS, UGV, or USV

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
- The DL shall write timestamped data onto an SD (or microSD) card in uLog format
- Data shall be measured at a high enough resolution to be unimpeachable
- The DL shall utilize Sensor Fusion to understand the environment around the vehicle the DL is mounted to
- The DL shall follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers under Title 47 Part 15 Guidelines [10]

#### Constraints
1\.	General Operation Constraints
- The DL project budget shall not exceed $3,000
- The DL shall have a large operating temperature range (-20ºC ~ 60ºC)

2\.	Standards and Safety Constraints
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act [11] 
- The DL shall be subject to IP67 rating for Dust and Water resistance [12] 
- The DL shall conform to IEEE standards for thermal dissipation and handheld devices [13] 
- The DL shall ensure the module and battery are properly grounded, avoiding electrical shorts or shock as laid out in Article 250 of NFPA 70 [14] 
- The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation 

With all these specifications for the DL, there are many alternative solutions that try to achieve the same goal as Team 3's DL. What are these existing solutions? 

## Survey of Existing Solutions
&emsp; &emsp; When looking at Existing Solutions, the traditional data logger has a minimum of at least 3 of the 5 sensors that Team 3 will be using. This helps make it a standalone data logger and does not require use of any onboard sensors of the vehicle it is mounted to. This gives the user a second source of data that can help verify the sensor data on the Unmanned Vehicle. This Survey of Existing Solutions shall look at the separate data loggers for various types of Unmanned Vehicles. 

&emsp; &emsp; The first type of UV, UAV's, typically requires its data logger to have the capability to utilize all 5 sensors that are going to be used in this project. There are many solutions currently available, however none of the existing solutions that were found used all 5. Here are some of the solutions Team 3 has found while researching for existing solutions. 

1.	YOST LABS 3-Space Data Logger Nav with BLE & GPS [15]
    - Pros
        - Has 4 out of the 5 sensors that shall be used in Team 3’s DL.
        - Has a custom tracking engine that is able to pick up everywhere that GPS is not available to track.
        - Has the option for both MicroSD card data logging or can send its data via Bluetooth
    - Cons 
        - Does not come with the thermometer
        - Comes at a High Price Tag of $750 per unit

2.	Mapir DAQ-A [16]
    - Pros
      - Comes at a cheaper price of $400 per unit 
      - Has support for the companies Camera exposure logging
    - Cons
      - Does not come with an on-board battery
      - Does not come with a barometer, thermometer, or magnetometer

3.	Takeaways
    - The main takeaway with data loggers for this type of UV is that they are highly priced for the size of the units.  These vehicles must come with a baseline of an IMU and GPS to be operational. These takeaways will be considered for Team 3’s DL. <br><br>

&emsp; &emsp; The next type of vehicle, UGV's, typically utilizes all the same sensors as a typical data logger for UAVs. The main difference between them is the containment or mounting of the data logger used for UGV's since it should be more dust protectant and vibration proof. Here are some of the solutions currently available for UGV's. 

1.	SparkFun DataLogger IoT- 9DoF [17]
    - Pros
      - Comes at the cheapest price as any on this list at $79.95
      - Is built to be a full Plug-and-Play IoT ecosystem meaning that sensors on their supported list can be plugged directly into the board and work immediately without coding them in
    - Cons
      - Where it is a full Plug-and-Play IoT ecosystem, the $79.95 price tag only comes with the base sensors, and this includes the IMU and Magnetometer. Everything else has to be purchased after obtaining this particular data logger.
      - Does not come inside of a rigid box and is just the board by itself

2.	Gulf Coast Data Concepts IMU-GPS [18]
    - Pros
      - Comes with 4 of the 5 sensors that the Team 3 DL will be using
      - Does come inside of the dust proof box
    - Cons
      - Comes at the Higher Price of $360
      - Comes at a bigger size than Valinor Dispatch's would like for the project
3.	Takeaways
    - One Main Takeaway from the UGVs data loggers is that they come at a cheaper price than UAVs DLs because they are not limited by size.  
    - Another takeaway is that they are more universal in the quantity of chips that can be used to track whatever is needed in the business specs without paying extra for unnecessary sensors. <br><br>

&emsp; &emsp; From these findings, there are all kinds of different quality and prices of DL's that exist to accomplish the goals of Team 3's DL. If a company needs their data logger to be usable for both types of vehicles, they are looking at spending anywhere from $400 - $1,110 without the shipping costs included. With Team 3's DL, the costs will be less, and there is no process required to combine one of these solutions with add-ons to fulfill all the specifications and constraints listed in this document. This will lead to Team 3's DL becoming the best solution available after development. <br><br>

## Comparative Analysis of Potential Solutions

&emsp; &emsp; When looking at all the different ways to go about this project, there are ways that can be created from the bare bones, and there are some that can take an already existing solution and build it. This section shall hypothesize the possible solutions and present the benefits versus the disadvantages.

1. The Bare Bones Model

&emsp; &emsp; This model includes picking out an MCU, IMU, GPS, Magnetometer, Pressure, and temperature gauge. The group would have to create the PCB to be mountable and able to use all these sensors using traces on the PCB. The group would also have to mount and use an onboard battery to power the system as well as an onboard charging system for the battery. In addition, an SD card reader is required to store the data being measured on the board. After mounting everything, the group would then have to use a MCU flasher to flash the program onto the CPU to let the CPU be able to talk to each individual sensor. On top of this, addition digital signal processing would be added to interpret the environment it is in using sensor fusion. 

a. Benefits:

  - The benefit of this system is that it would play heavily upon the electrical circuitry of the PCB which multiple group members have stated to be included in their strong suits. It also has the benefit of complete customization in the fact that the group would get to pick every single sensor that would be wanted for the specific purpose.

b. Disadvantages:

  - The Disadvantage of this system is that if the company wanted to mass produce this product it would be increasingly difficult to have to source every single product to build the DL. Also, it would increase the amount of labor it would require the engineer to build the project.

2. The Controller Add-On Model

&emsp; &emsp; This model would include the group using an already made controller module and manipulating it to have the capabilities of being a data logger. Also, addition sensors would usually need to be added to make it achieve Valinor's specifications. Team 3 would still develop a custom PCB to add these additional sensors that module does not have. The specific module that has been suggested to Team 3 is the ARK FPV Flight Controller. This flight controller module includes an MCU, IMU, Temperature, Pressure, Magnetometer, and microSD card. The suggested flight controller can be seen in *Figure 1*. [19]

*<div align="center">![Figure 1](https://hackmd.io/_uploads/H1xZcQjK2zx.png)</div>*
*<div align="center">Figure 1: The ARK FPV Flight Controller</div>*

a. Benefits:

  - The benefit of The Controller Add-On Model is that it is a faster and easier alternative to the bare bones model. Much less is needed to do to get this model completely functional. All that would be required is to develop a custom "Hat" PCB to hold the GPS and create a battery pack system and wire it to the Flight Controller. After this, Team 3 would be required to do some addition coding to get the new GPS sensor to work with the on-board MCU. This would make it much cheaper and faster for Valinor Dispatch if they would like to create many copies of this design.  

b. Disadvantages:

  - The disadvantage of this system is that it removes many aspects that make this project so unique. This can also limit how custom the DL can be. This route is great for the purpose of quantity and not as good for quality. This is not to discredit the chips found on the ARK Flight Controller as bad chips, but it would significantly reduce the customization of the DL. This also would mean that the project is limited by budget or capabilities of the sensors already incorporated into the flight controller. With this route, this project would be more focused on coding than engineering.

&emsp; &emsp; Looking at all the Benefits and Disadvantages for both, Team 3 has decided it best to use the Bare Bones model to achieve Valinor's goals. This will allow Team 3 to customize all the elements to work and expand like Valinor's systems do. 

## High-Level Solution

&emsp; &emsp; The goal of this project for Valinor Dispatch is to develop a self-contained module that records data from integrated instrumentation and seamlessly implements the module onto their unmanned vehicles and utilize sensor fusion to interpret the data being collected to interpret the environment before storing the data.

&emsp; &emsp; The way Team 3 will maximize achieving these goals will be utilizing components, modules, and software that the company is already familiar with. This will reduce the amount of time and resources they will need to dedicate to making future adjustments to the module. In addition, the system will utilize widely available components paired with a commonly utilized MCU to help in the development process. 

&emsp; &emsp; This module will be based on the Bare Bones Model presented previously in the section comparing the possible different models and be subject to the requirements listed previously in this document. *Figure 2* shows the block diagram for the diagram based on the Bare Bones Model that Team 3 is using to design the data logger from the ground up. 

*<div align="center">![Figure 2](https://hackmd.io/_uploads/SysF4iY2Gl.png)</div>*
*<div align="center">Figure 2 – Data Logger Block Diagram</div>*

Here is how the model in *Figure 2* will be implemented to achieve Team 3's goals:

### Subsystems:
1. PCB
  - The PCB subsystem houses all sensors as well as the RGB LED. The physical PCB will also house the microSD and Microcontroller subsystems. This will draw power from the Power System and communicate with the Microcontroller via serial communication. The PCB subsystem shall be small enough to fit within housing smaller than 4 in x 3 in x 1 in. The PCB shall also isolate the sensors enough to where they will not interfere with each other’s operation. 

2. Storage System and Data Analysis 
  - The MicroSD will be housed on the physical PCB. The microcontroller will write data onto the microSD in ULog format. The microSD port shall be compliant with IP67 standards for dust and water resistance [12].  After writing onto the MicroSD card, the data will be analyzed, filtered, and smoothed to get clean data onto the microSD card. 

3. Microcontroller
  - The Microcontroller will be housed on the physical PCB and draw power from the Power System. The microcontroller will write data onto the microSD in ULog format and communicate with the PCB subsystem via serial communication. The microcontroller shall be isolated from the sensors to avoid increased noise.

4. Power System
  - The Power System will regulate input power from a USB-C port and the battery while supplying the other systems with power. The Power System shall comply with grounding, shock, and hazardous material standards.

5. Enclosure
  - The enclosure will be used to prevent dust and water from touching the electronics of the data logger to keep an IP67 rating [12]. This will have a tab that opens to the MicroSD card reader and the USB-C port to access them without removing the entirety of the enclosure.

&emsp; &emsp; With this model in mind, it will operate with the signal flow displayed in the operational flowchart shown in *Figure 3*. 

*<div align="center">![Figure 3](https://hackmd.io/_uploads/rkOA4jYnzl.png)</div>*
*<div align="center">Figure 3 – Operational Flowchart for Team 3's Data Logger</div>*

<br>&emsp; &emsp; While developing these systems, there have been constraints identified in the *Specifications and Constraints* section that will need to be followed in the development of these PCB systems. Team 3 plans to adhere to these constraints in the following ways:

### Physical Attributes
- The DL shall be less than 500g in mass; The module will utilize multiple components as well as a battery all which are collectively under the weight limit.  
- Entirely self-contained; The DL shall be isolated and not interfere with vehicle communications or existing onboard components. 
- Shall be approximately 4in x 3in x 1in; Due to the size of the components, this constraint will be achieved. 
- Easily attached to the outside of a UAS or UGV; The DL will remain securely attached when mounted and will be designed to resist vibrations and shock.

### Electronics
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

### Data
- The DL shall write timestamped data onto an SD (or microSD) card in ULog format; The team will research ULog formatting to confirm the data is being formatted and written correctly to the SD card as well as ensuring GPS timestamps are accurate. 
- Data shall be measured at a high enough resolution to be unimpeachable; Extensive tests will be performed to ensure the data is correct. 
- The DL shall follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers under Title 47 Part 15 Guidelines [10]; Since the DL will be utilizing an antenna for the GPS, it is very important for this antenna system to not interfere with any receivers or transmitters around the DL.

### General Operation Constraints
- The DL project budget shall not exceed $3,000; Components will be selected specifically to comply with the budget, also accounting for assembly and bench testing. 
- The DL shall have a large operating temperature and pressure range (-20ºC ~ 60ºC); Extensive bench testing will be performed, so the module operates within the specified temperature and pressure ranges. Additional temperature regulation techniques	may be implemented to obtain this objective.

### Standards and Safety Constraints
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act [11]; Team 3 will ensure the components that are being utilized as well as the testing procedures will comply with the Federal Hazardous Substances Act. 
- The DL shall be subject to IP67 rating for Dust and Water resistance [12]; Team 3 will perform extensive testing to ensure the module is IP67 rated and will make adjustments to ensure the module will be IP67 rated.  
- The DL shall conform to IEEE standards for thermal dissipation and handheld devices [13]; Team 3 will ensure the module conforms to IEEE standards and implement passive thermal management designs into the module. 
- The DL shall ensure the PCB and battery are properly grounded, avoiding electrical shorts or shock [14]; Team 3 will follow IEEE, NEC, and NFPA to ensure the module adheres to these standards.  
- The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation; Due to the low power consumption of both module versions, low voltage batteries will be utilized as well as following the design constraint listed in the Electronics constraint section.

## Atomic Subsystem Specifications

There will be 5 major subsystems that will be considered for these two modules. Such subsystems are as follows: 

  1. PCB System
  2. Power System
  3. Microcontroller System
  4. Data Processing & Storage System
  5. Enclosure

Here are some specifics on each of these subsystems.

### PCB Subsystem

&emsp; &emsp; The PCB will act as the foundation for the module and will be populated with the necessary instrumentation components as well as a power management system that accommodates battery charging. The PCB will be utilizing all types of signals as it holds all of the components. It will also be able to mount to unmanned vehicles utilizing the enclosure it will be contained in. 

&emsp; &emsp; The primary components located on the PCB are as follows: 

- Microcontroller (MCU): Shall process and interpret data from sensors, then formats and write data to the microSD card. 

- Inertial Measurement Unit: Shall measure linear acceleration and interface with MCU 

- GPS: Shall record time stamps received from GPS satellite connection and interface with MCU. 

- Temperature Sensor: Shall read ambient temperature and interface with MCU. 

- Pressure Sensor: Shall read ambient pressure and interface with MCU. 

- Magnetometer: Shall measure the strength, direction, or relative changes of a magnetic field and interface with MCU. 

- SD Card Reader/Writer: Shall accept data transmission from MCU after data is formatted to specification and write that data to the SD card. 

- USB-C connector: Acts as the primary connector for the charging cable. Shall supply power through *standard USB-C protocol* to both the battery and components when cable is connected. The USB-C charging system shall comply with the safety constraints listed in the *High-Level Solution* section.

### Power System

&emsp; &emsp; The power system will handle power management throughout the PCB as well as the battery charging system. The primary interfaces will be the USB-C connector and the battery's JST connector. The USB-C will act as an input that receives power via external USB-C cable. The JST connector will act as both an input and an output as the battery will charge and discharge through this connector.  

&emsp; &emsp; A handful of small components will be integrated into the power system to manage power regulation as well as battery charging. A battery charger IC will be the primary component of the battery charging circuit and is responsible for managing power that is received from the USB-C connector and regulating that power to the battery. If the battery is charging, a red LED will be illuminated. If the battery is fully charged, the charging IC will stop charging the battery and the red LED will turn off. A 3.3V regulator will be the primary component for voltage regulation throughout the PCB as most of the onboard components have an operating voltage range of 3.3V. Smoothing capacitors will be placed along the power traces to filter high frequencies. *Figure 4* shows the ideal battery charging flowchart.

*<div align="center">![Figure 4](https://hackmd.io/_uploads/BJqqditnzx.png)</div>*
*<div align="center">Figure 4 – Charging System</div>*

&emsp; &emsp; The battery chosen is a 3.7v 3000mAh rechargeable LiPo battery. With the DL needing to stay powered for 24 hours, the battery has a max current demand of 125mA. The max current demand per component is as follows: 

1. LED = 20 mA
2. STM = 56 mA
3. Pressure Sensor = 3.4 µA
4. Magnetometer = 450 µA
5. IMU = 790 µA
6. GPS = 4.5 mA
7. Temperature Sensor = 220 µA

&emsp; &emsp; With a total current demand of about 92mA, the data logger can run for about 36 hours without being recharged. This means the DL will be able to run for the required 24 hours from a 65% charged battery and above.

### Microcontroller

&emsp; &emsp; The microcontroller chosen for this project is the STM32G474RET6. This microcontroller will allow for the reading of all attached sensors as well as writing the data from these sensors out to the microSD through ULog format. The firmware needed for this subsystem will be written in C and designed using the STM32CubeMX software. 

&emsp; &emsp; The firmware needed for this program will have 5 parts: 

1. **Setup**
- This section will initialize all the peripherals needed. It will also initialize each of the four tasks needed and the ring buffer required for the logger task. It will also handle mounting the microSD card.

2. **Sensor Task**
- The sensor task will read the data coming from the sensors at regular intervals and push the data to the next task for analysis.

3. **Analyzer Task**
- This task will take the data analysis curated by Nic through the Storage System and Data Analysis subsystem and implement it on the microcontroller before pushing the now processed data to the logger.

4. **Logger Task**
- The logger task takes the processed data from the analyzer task and writes it out in ULog format to the microSD card. A ring buffer is used to keep the sensor and the logger from interrupting the other’s timing and throwing each other off balance.

5. **Supervisor Task**
- This task determines when and if the logger should be actively writing out or not based on a few different factors. It checks if the microSD card has been inserted and has power, if so it tells the logger to write out, if not it flushes the buffer to keep it from getting full of old data.

### Storage System and Data Analysis

&emsp; &emsp; The MicroSD will take the data given to it in ULog format, which on the microSD card will be a single, continuous train of binary data directly from the microcontroller. This data will be in the exact same format that the microcontroller will see. All this data will be raw binary data and will need to be put into some kind of converter to be understood by humans. The benefit of the ULog format though is where it is binary, it does not take up much space. This helps give a heap of data in a small package. To make it able to be read by a human, it will have to be converted to CSV (Comma Separated Variables), by using python. Then this data can then be put into understandable graphs using MATLAB.

&emsp; &emsp; After getting graphs, this subsystem will also take the raw and unfiltered data and smooth it out to make it easily read by a consumer. This will be done with DSP (Digital System Processing). The DSP will include filtering out any high frequency noise and isolating the true system states.  By using PIDs and other Software filters, there shall be a Dynamic Transfer function that will then be flashed onto the MCU at the Analyzer Task.  This process may be repeated as many times as needed to get clean data from the DL. 

### Enclosure

&emsp; &emsp; With this subsystem, the goal is to achieve the IP67 rating that is in the specifications for the project while allowing the Data Logger to function and not overheat [12]. This will be achieved by utilizing a casing that allows for an antenna to fit tightly through the enclosure for the GPS and potentially using cooling fans or systems to prevent damage inflicted on the Data Logger by itself. In addition, it will be the primary source of mounting the Data Logger to these unmanned vehicles utilizing this project.

&emsp; &emsp; To accomplish this, the enclosure will be utilizing M4 screws and mounting equipment to allow for the Data Logger to be easily added or removed from these vehicles. Also, some more screw will be used to allow for easy access to the microSD card without the requirement of dismounting the logger from the vehicles. 

## Measures of Success
&emsp; &emsp; To ensure the accuracy and consistency of the DL, comparisons will be made with established units of various types to ensure the measurements are accurate. In addition, the efficiency of the DL will be verified so Team 3's DL will become the best solution. These will be checked using the following measurements of success: 

1. Sensor Data Measurement
    - Each sensor will have readings taken for a set environment, and the data will be compared to sensors outside of the DL for accuracy.
      - For the accelerometer,
      - For the IMU,
      - For the thermometer, it will be put inside a temperature chamber with a set temperature to compare the readings on the thermometer to the set temperature.
      - For the pressure gauge,
      - For the GPS, 
    - Data measurement will be defined based on these error ranges in early testing:
      - Acceleration & Velocity: ± 5 %
      - Magnetic Field Strength: ± 5 %
      - Temperature: ± 2 °C
      - Pressure: ± 5 Pa
      - Absolute Time: ± 2 s
    - The final error ranges for success should be:
      - Acceleration & Velocity: ± 5 %
      - Magnetic Field Strength: ± 5 %
      - Temperature: ± 1 °C
      - Pressure: ± 1 Pa
      - Absolute Time: ± 1 s<br>
      
2. Power System Efficiency
    - The power system of the module shall be able to run all five sensors measuring data with readings within the previously listed tolerances at the same time for any continuous amount of time until the battery dies or the DL is turned off.  
    - The system shall run the MCU and SD card writing unit as well along with the sensors for any continuous amount of time without corrupted or missing data from the sensors. 
    - The system shall be rechargeable while onboard and last for more than one operation as specified previously in constraints without recharging being necessary during the trip.
    - Success is found when the DL can run all five sensors, the MCU, and the SD card writer without part failure from current and voltage draw.
    - Success is also reliant on the power system running for longer than 1 day without recharging.<br>

3. Data Processing and Transmission System
    - The MCU, whether it is an STM32, Raspberry Pi, or any other kind of controller, must be able to process data from all five sensors simultaneously. 
    - Once it has processed the data, it shall be organized and written in uLog format to the SD card so it can be recovered after a mission is complete. 
    - This system is deemed successful if the data can be read from the MCU using the STMCubeIDE to monitor these values. 
    - This system will utilize an RGB LED light to indicate red when the DL is turned on and ready for an SD card, green while the DL is processing data and writing data to the SD card, & Blue when the ulog file on the SD card has been closed and the SD card can be removed.
    - Success of these systems together will be when the SD card can be inserted into the SD card writer, have accurate data written to it from the MCU, and the ulog file created on the SD card is closed with the data organized in sets of data with timestamps from when it was taken.
    - Success will also be based on if there is an accurate guess of the environment the DL is in after Sensor Fusion is complete from the data collected.
    - These measures of success will be tested by mounting the DL onto one of Valinor Dispatch's unmanned vehicles for a 10-minute mission through different environments like outside vs inside to compare the readings of the DL to known temperatures, pressures, and timestamps.<br>
    
4. System Consistency in Different Environments 
    - This DL must be able to function properly in any environment. 
    - This measure will be met when the DL consistently gains accurate information on the SD card from the sensors in multiple different environments.<br><br>

&emsp; &emsp; All these indications are important to the success of the DL, but it is not a complete success unless it meets the criteria listed previously in this document as well. <br><br>


## Resources
&emsp; &emsp; The resources required for this project can be categorized in three ways: budget, labor, and timeline. Within these, the budget will specify what the expected costs are for each subsystem as well as the total expected cost for the project. The division of labor will clarify the team’s areas of expertise and how each member is going to contribute moving forward. The expected timeline will also be proposed, indicated using a Gantt Chart specifying the tasks needed to complete the project as well as when they are expected to be completed. 


### Timeline
![Team 3 Development Timeline](https://hackmd.io/_uploads/HymNoo73Gl.png)


### Budget

#### PCB Design
&emsp; &emsp; This system contains the necessary PCB, along with its basic circuitry that will contain the capacitors, resistors, and other components necessary for its functionality. It also contains a pressure gauge, magnetometer, IMU, GPS, and digital temperature sensor. These parts were carefully chosen due to the specific needs and requirements of our DL and have been compared against our weight and area constraints. The costs for this subsystem can be seen below. 

- PCB: $50
- Pressure Gauge: $3
- Magnetometer: $3
- IMU: $4
- GPS: $12
- Digital Temperature Sensor: $6

Subsystem Total: $78

#### Power System

&emsp; &emsp; This system utilizes a Jauch Quartz LP705176JS 3.7V 3.15Ah battery. This battery was chosen as it satisfies the voltage needed for the STM32 microcontroller as well as the other power constraints needed for the PCB and it’s parts. The part itself will be utilized to supply power to the PCB, microcontroller and all other parts of the DL. The costs for this subsystem can be seen below. 

- Battery: $22

Subsystem Total: $22

#### Microcontroller

&emsp; &emsp; This system utilizes a STM32G474RET6 microcontroller. This chip will be used to read data off of the various sensors that have been implemented on the PCB and will write out data to the MicroSD card at regular intervals. This specific chip was recommended by Valinor Dispatch to Team 3 and was chosen after careful consideration. Using the STM32 will also require the use of a programming cable and the one chosen for this project is the STLINK-V3MINIE. This chip was chosen at the recommendation of Valinor Dispatch and is commonly paired with the STM32 microcontroller. The connector cable required for the STLINK-V3MINIE is the TC2030-CTX-NL-STDC14 cable which will connect the PCB to the STLink for debugging purposes. The costs for this subsystem can be seen below. 

- STM32G474RET6: $10
- Programmer: $25
- Programming Cable: $50

Subsystem Total: $85

#### Data Processing & Storage System

&emsp; &emsp; This system contains the elements required to store data for the DL. It consists of the MicroSD card reader that will be located on the PCB as well as the MicroSD card itself. The MicroSD card reader chosen for this project is the Same Sky MSD-3-A. This part was chosen due to it’s size, weight, and cost as the most effective option. It features the ability to auto-eject out, allowing for easy removal of the MicroSD card. The costs for this subsystem can be seen below.

- MicroSD Card Reader: $1
- 256GB MicroSD Card: $50

Subsystem Total: $51

#### Enclosure

This system contains the casing outside the PCB to allow for easy removal utilizing M4 screws and an environmently robust casing to keep the Data Logger functioning. The costs for this system can be seen below. 

**TBD**

#### Total Budget

&emsp; &emsp; The total overall proposed budget for Team 3’s Data Logger is $236. As seen above these components have been chosen intentionally to work well together and result in a well rounded Data Logger that successfully reads and writes out data onto a MicroSD card using two separate board styles. 

### Division of Labor 

The personnel of Team 3 and their skill sets are as follows: 
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
 
Based on these skills, the subsystems and their designated members have been divided as such:

- Nic Campbell will be taking care of the Storage System and Data Analysis as he has a specialty in control systems engineering. Through this subsystem he will be working mainly with the MicroSD as well as how the firmware filters and interprets the data it receives from the sensors.

- Lucy Dunn will be over the microcontroller and therefore the firmware stored on it. She has been given this subsystem as she is the most versed in coding and has experience in embedded systems as well as computer design. She will be writing the software and designing the firmware that will go on to the STM32 microcontroller.

- Sean Ottoway will be in charge of the PCB design as he is well versed in KiCad and has experience in designing PCBs from scratch. All team members have joined him in researching components for this PCB and clearing them with Sean throughout the design process. His main responsibility will be designing the PCB from scratch as well as assembling it once received.

- Gabe Simpkins will be in charge of the Power System. He is skilled in circuitry and can look at the PCB design and components chosen and determine the power, voltage, and current necessary for the overall design of the Data Logger. He will be checking that the batteries chosen to perform up to standard and expectation as well as ensuring that each component is getting the power it needs to perform properly.

- Andrew Singletary will be working on the enclosure for the Data Logger to make sure that it does not impede on the functionality of the project while keeping the proper rating. This suits him well with his understanding of microcontrollers and sensor functionality with limitations. He will also be helping Nic with the details of the data processing system once the enclosure subsystem has been complete.

#### Other Personnel
- Planned Supervisor: Dr. Tarek Elfouly
  - Dr. Elfouly has a multitude of experience working with embedded systems, communicating with sensors using various languages, and programming microcontrollers. This makes him a great choice to help advise the development of this project. 
- Valinor Dispatch Contact: John Cain
  - John Cain along with Valinor Dispatch is the customer of this project, and they are looking to utilize this project once it is fully developed to influence future improvements of their unmanned vehicles. They are also looking to obtain information related to any environment they may be sending unmanned vehicles to for many purposes like navigation of these vehicles. 
- Instructor: Dr. Christopher Storm Johnson
  - Dr. Johnson is the main supervisor over the project progress and documentation for this project. All documentation will be put through him to be approved before moving on in the development of this DL. Lastly, if any interpersonal matters escalate to negatively affect the development process, he will act as oversight and mediator if necessary to help progress this project. 


## Specific Implications

&emsp; &emsp; There are many benefits to the DL Team 3 is developing. The solution for onboard data measurement and storage for autonomous vehicles with this DL can be viewed through four major sets of implications: 


#### *Technical Implications*

&emsp; &emsp; Developing a data logging module is an in-depth hands-on project. There is quite a bit of component research and testing that needs to be conducted. While there are readily available and universal off the shelf units, this DL is designed specifically for the company's autonomous vehicles and is much more cost effective than the competitors. This DL collects data from onboard sensors that measure GPS time stamps, pressure, temperature, electromagnetic fields, and writes the data to a micro-SD card. This unit is self-contained and features its own battery power source with support for USB-C charging. With these inclusions, it will stand out against other data loggers used for Unmanned Vehicles. 


#### *Manufacturing Implications*  

&emsp; &emsp; This DL is designed to use readily manufactured and widely available components. The module will feature its own PCB that can be easily manufactured by most PCB manufacturing companies without going through a custom manufacturer. The cost to develop and manufacture the DL will be well under the $3,000.00 budget allocated for the project.  


#### *Operational Implications*  

&emsp; &emsp; This DL will be developed to be a self-contained unit that utilizes the shelf components that do not require maintenance intervals. If one of the DLs malfunctions or needs to be replaced, a new one can be easily swapped in without requiring the knowledge of an engineer. This will allow for sustainability of the DL without being replaced frequently. 


#### *Strategic Implications*  

&emsp; &emsp; This DL is designed specifically to integrate with the company's already existing autonomous vehicles and will be mountable to any vehicle Valinor Dispatch would like and does not need any extra connections, excluding the battery charging cable. This makes the DL unique from competing data loggers and easily used for any task Valinor Dispatch desires to utilize Unmanned Vehicles on. <br><br>

&emsp; &emsp; With all these implications, the DL will benefit Valinor Dispatch's needs for autonomous vehicle data logging in many ways to help with further development of their autonomous charging stations and other technology; however, there are some considerations that are required in the process of this DL. <br><br>

## Broader Implications, Ethics, and Responsibility as Engineers

&emsp; &emsp; Due to the rising issue of public trust with data collecting technology, a device such as this DL measuring environmental conditions and saving this data could pose global and societal implications. While the DL is only used to collect information about the environment and collects time stamps regarding the autonomous vehicle, the sensors the DL utilizes might lead to public distrust as the sensors can be implemented to collect unsolicited information. These implications are not as important since the DL will not be widely available for this to occur.  

&emsp; &emsp; A device such as this DL contains and implements various modules that can potentially be used for intrusive surveillance. This could further influence the modern and ongoing public trust issues that are present within the tech industry in terms of selling private information. With this DL, any extra "features" that could be added to the DL might bring ethical issues such as using GPS tracking for purposes outside the DL's scope as well as sensitive location data logged by the DL. Team 3 will heavily consider this in the way the DL will be programmed. 

&emsp; &emsp; Environmental implications would cover the operations and carbon footprint of the manufacturing process for the DL. This DL uses special sensors and components that are manufactured using semiconductors and other materials. Accessibility to these components could pose an issue with few locations being able to manufacture and procure these semiconductors found in the DL. Team 3 will avoid this issue by using components that are readily available and manufactured from trusted and well-known companies to prevent addition difficulties from obtaining more obscure materials. Another potential issue would be the module detaching from the vehicle during operation, potentially disrupting terrestrial and aerial life as well as their environments. To prevent this, this DL will have the capability of using M4 screws via the screw mounts in this DL to keep the module from affecting wildlife and the environment.

&emsp; &emsp; In terms of economic implications, choosing and pricing components come into play. As engineers, Team 3 needs to come up with a good and economical price to return on investment value to deliver the best piece of hardware for the right cost. If the sensors and components are too cheap, there might be issues with reliability for the DL, causing complications for Valinor and the vehicles utilizing them. If the project is too expensive, Valinor Dispatch would lose their investment in the development of this module. This will be a major focus for Team 3 to keep the DL inexpensive while still utilizing trusted technology to meet the specifications. 

&emsp; &emsp; With the development and planning of this module, there are important ethical considerations when it comes to the operation and implementation of the DL. The team of engineers responsible for the development of this project must consider the previously mentioned implications and adhere to the following ethical standards: 
- Team members who are responsible for the software will program the modules to only capture data within the project scope.
- Team members who are responsible for hardware will construct and develop the DL to comply with basic safety standards as well as staying within project scope.<br><br>

&emsp; &emsp; In summary, Team 3 will be developing this DL with success being measured based on these considerations, the specifications, and the measures of success listed in this document. When it meets all these standards, it will bring the promised benefits also listed and fulfill Valinor Dispatch's request for the DL, which will demonstrate innovation through Team 3's development of this project. 

## References

[1] “Drone Simulation,” www.mathworks.com. https://www.mathworks.com/discovery/drone-simulation.html (accessed Oct. 09, 2026).  

[2] J. Sanchez, “Ruggedized Storage for UAV/Drone Data Logging: Why Consumer-Grade Storage Falls Short,” Delkin Industrial, Jan. 28, 2026. https://www.delkin.com/blog/rugged-uav-data-logging-storage/ (accessed Oct. 09, 2026).  

[3] J. Kocić, N. Jovičić and V. Drndarević, "Sensors and Sensor Fusion in Autonomous Vehicles," 2018 26th Telecommunications Forum (TELFOR), Belgrade, Serbia, 2018, pp. 420-425, doi: 10.1109/TELFOR.2018.8612054.  

[4] S. Yu, J. Ma, and W. Wang, “Deep Learning for Denoising,” Geophysics, vol. 84, no. 6, pp. V333-V350, July 2019, doi: 10.1190/geo2018-0668.1. 

[5] Q. Zhang, Y. Zheng, Q. Yuan, M. Song, H. Yu and Y. Xiao, "Hyperspectral Image Denoising: From Model-Driven, Data-Driven, to Model-Data-Driven," in IEEE Transactions on Neural Networks and Learning Systems, vol. 35, no. 10, pp. 13143-13163, Oct. 2024, doi: 10.1109/TNNLS.2023.3278866. 

[6] E. Peña and M. Legaspi, “UART: A Hardware Communication Protocol Understanding Universal Asynchronous Receiver/Transmitter,” VISIT ANALOG.COM, vol. 54, no. 4, 2020, Accessed: Nov. 06, 2026. [Online]. Available: https://fgcoca.github.io/Autocaravana-inteligente/datasheet/uart-a-hardware-communication-protocol.pdf 

[7] Dr. T. Elfouly, “Serial Communication - I2C,” ECE 4140 Lecture, Tennessee Technological University, Cookeville, TN, Oct. 12, 2026. Accessed: Nov. 06, 2026. [Online]. Available: https://drive.google.com/file/d/12pZjCredY6Ln2uffFPUiT_TnEynQqUeO/view?usp=sharing 

[8] Dawoud Shenouda Dawoud, SERIAL COMMUNICATION PROTOCOLS and STANDARDS: Rs232/485, Uart/Usart, Spi, Usb, Insteon, Wi-Fi and Wimax. Aalborg: River Publishers, 2020. 

[9] Dr. T. Elfouly, “Serial Communication - SPI,” ECE 4140 Lecture, Tennessee Technological University, Cookeville, TN, Oct. 26, 2026. Accessed: Nov. 06, 2026. [Online]. Available: https://drive.google.com/file/d/1nXYp2KQZq13p0-WOEwmBI7-R9dWzmG6O/view?usp=sharing 

[10] Federal Communications Commission, Telecommunication, 47 C.F.R. pts. 40–69 (2026). 

[11] “Federal Hazardous Substances Act (FHSA) Requirements,” CPSC.gov, Apr. 04, 2016. https://www.cpsc.gov/Business--Manufacturing/Business-Education/Business-Guidance/FHSA-Requirements (accessed Oct. 09, 2026).  

[12] International Electrotechnical Commission, “IP Ratings | IEC,” www.iec.ch, 2024. https://www.iec.ch/ip-ratings (accessed Oct. 21, 2026).  

[13] IEEE, “Handheld Devices,” IEEE Technology Navigator, 2026. https://technav.ieee.org/topic/handheld-devices/ (accessed Oct. 22, 2026).  

[14] National Fire Protection Association and National Fire Protection Association. National Electrical Code Committee, "Article 250," NEC 2017: NFPA 70 National Electrical Code. Quincy, Ma: National Fire Protection Association, 2016.  

[15] Yost Labs, "3-Space™ Data Logger Nav with BLE & GPS,” Yost Labs, https://yostlabs.com/product/data-logger-nav-ble-gps/?srsltid=AU7gw4WEJ3qvT_4odsTwyClEaaVQxsDjtb8ClRZoBbiuZgtiw0GERoP8 (accessed Oct. 08, 2026)  

[16] MAPIR, “DAQ-A,” MAPIR, 2026. https://www.mapir.camera/products/daq-a (accessed Oct. 08, 2026).  

[17] “SparkFun DataLogger IoT - 9DoF,” Sparkfun.com, 2025. https://www.sparkfun.com/sparkfun-datalogger-iot-9dof.html (Accessed Oct. 08, 2026).  

[18] “IMU-GPS - Gulf Coast Data Concepts,” Gulf Coast Data Concepts - Simple yet versatile data acquisition, Sept. 06, 2024. https://gulfcoastdataconcepts.com/index.php/product/imu-gps/ (Accessed Oct. 08, 2026).  

[19] “ARK FPV | ARK Documentation,” Arkelectron.com, Oct. 21, 2026. https://docs.arkelectron.com/products/flight-controller/ark-fpv (accessed Oct. 23, 2026). 

## Statement of Contributions
These are the contributions the team made to this document:<br><br>
Nicolas Campbell: Survey of Existing Solutions, Operational Flowchart, Comparative Analysis of Potential Solutions, Storage Systems and Data Analysis<br><br>
Lucy Dunn: Resources, Budget, Timeline, Division of Labor, Microcontroller Subsystem<br><br>
Sean Ottaway: Broader Implications, Specific Implications, High Level Solution, PCB Subsystem, Power Subsystem<br><br>
Gabriel Simpkins: Background, Specifications, & Constraints, Fully Formulating the Problem, Hardware Diagram<br><br>
Andrew Singletary: Introduction, Measures of Success, & Broader Implications, High Level Solution, the ARK Flight Controller-Based Subsystem
