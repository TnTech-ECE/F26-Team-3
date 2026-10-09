# <div align="center">Project Proposal - Team 3</div>
<div align="center">Nicolas Campbell, Lucy Dunn, Sean Ottaway, Gabriel Simpkins, & Andrew Singletary</div>

## Introduction
&emsp; &emsp; Unmanned vehicles can be found all over the world being used by the military to scout in harsh environments without using human resources. Because the environment is a big factor in warfare and defense, there is a strong drive to improve these vehicles to withstand such harsh environments. Data loggers gain such information about these different environments, but often they can only function on one type of vehicle, measure individual elements of the environment, or format information poorly. This causes inefficiency and higher costs to obtain this mission-critical information. 

&emsp; &emsp; To address these needs, Team 3 is conducting research and development to find a lower-cost, modular, and mass-producible module able to obtain accurate time stamps and measure magnetic fields, temperature, pressure, and dynamic movement around these vehicles. Once this data logger obtains these measurements, it needs to write this information in uLog formatting onto a microSD card for military personnel to plan around. This self-contained system will integrate five sensors, a microcontroller, and a power source in a mountable PCB while staying under $3,000 for the process of developing it.  

&emsp; &emsp; This proposal outlines the background of Data Loggers and a thorough evaluation of existing solutions. It will address the difficulties involved with such an embedded system and further elaborate on the need for this project. This will distinguish the restrictions on the project along with definitions of what success looks like for the project. It will present the details of the budget, proficiencies of the team and associated experts, and a timeline with milestones of the project. Finally, the proposal will end by discussing the implications of success and ethics concerns related to this project. 

## Formulating the Problem
&emsp; &emsp; For data measurement, unmanned vehicles (UVs) typically only have an onboard IMU and do not have dedicated memory drives for data tracking. The Data Logger will be able to track IMU data, temperature, pressure, magnetic field strength, and log all of this data with absolute timestamps. A dedicated unit for data tracking will free up the UV to focus on navigation and will give more accurate data that can help the user learn more about mission environments.

### Background
&emsp; &emsp; Rough terrain and harsh environments make recording data from UVs difficult [1]. Recording environmental data can help the user learn more about potential hazards, environmental changes, and the impact of this data on the UV. Data like this can inform mission critical decision-making. These can also be important to track for simulation purposes. Tracking these data points (IMU data, temperature, pressure, magnetic field strength) can help to make simulations of the UV environments more accurate, leading to better flight control and an improved drone model [2].

&emsp; &emsp; While there are other comparable solutions, many fall short of the desired specifications. These alternative solutions are out of this project stakeholders' budget, don’t measure all the required data, or don’t save the data to an SD card. These are also often too large to be portable and transferable to other types of drones without modification. Designing a product that meets all these criteria requires a knowledge of sensors, embedded systems, MCUs, and PCB design.

### Specifications and Constraints
&emsp; &emsp;The Data Logger (DL) has several specifications and constraints given by this project's stakeholders as well as electrical and communication governing bodies required for the project:

#### Specifications
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
- The DL may follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers for this prototype

#### Constraints
1\.	General Operation Constraints
- The DL project budget shall not exceed $3,000
- The DL shall have a large operating temperature and pressure range (-20ºC ~ 60ºC)

2\.	Safety and Compliance Constraints
- The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act [3]
- The DL shall ensure the PCB and battery are properly grounded, avoiding electrical shorts or shock
- The DL may be resistant to water or may be contained in a water-resistant case

## Survey of Existing Solutions
&emsp; &emsp; From what has been found, there are not any companies that make a version of the DL that is useable for all three UAV, UGV, and USV. They do however make a version of a DL for each individual UV. This section shall be broken into 3 different sections, each section correlating to the existing solutions to each UV.

&emsp; &emsp; The first type of vehicle, UAV's, should utilize all 5 sensors that should be used in this project. There are many solutions currently available, but here are some of these solutions currently available.
1.	YOST LABS 3-Space Data Logger Nav with BLE & GPS [3]
    - Pros
        - Has 4 out of the 5 sensors that shall be used in Team 3’s DL.
        - Has a custom tracking engine that is able to pick up everywhere that GPS is not available to track.
        - Had the option for both MicroSD card data logging or can send its data via Bluetooth.
    - Cons 
        - Does not come with the thermometer.
        - Comes at a High Price Tag of $750 per unit

2.	Mapir DAQ-A [4]
    - Pros
      - Comes at a cheaper price of $400 per unit 
      - Has support for the companies Camera exposure logging
    - Cons
      - Does not come with an on-board battery.
      - Does not come with a barometer, thermometer, or magnetometer.

3.	Takeaways
    - The main takeaway with this type of DL is that they are highly priced for the size of the units.  These vehicles must come with a baseline of an IMU and GPS to be operational. These takeaways will be considered for Team 3’s DL.<br><br>

&emsp; &emsp; The next type of vehicle, UGV's, use all the same sensors that UAV's use. The main difference between them is the box containing the DL for UGV's should be more dust protectant and vibration proof. Here are some of the solutions currently available for UGV's.  

1.	SparkFun DataLogger IoT- 9DoF [5]
    - Pros
      - Comes at the cheapest price as any on this list at $79.95
      - Is built to be a full Plug-and-Play IoT ecosystem meaning that sensors on their supported list can be plugged directly into the board and work immediately without coding them in.
    - Cons
      - Where it is a full Plug-and-Play IoT ecosystem, the $79.95 price tag only comes with the base sensors, and this includes the IMU and Magnetometer. Everything else has to be purchased after obtaining this particular data logger.
      - Does not come inside of a rigid box and is just the board by itself.

2.	Gulf Coast Data Concepts IMU-GPS [6]
    - Pros
      - Comes with 4 of the 5 sensors that the Team 3 DL will be using.
      - Does come inside of the dust proof box
    - Cons
      - Comes at the Higher Price of $360.
      - Comes at a bigger size than Team 3’s stakeholder's desire.

3.	Takeaways
    - One takeaway from the UGVs DLs is that they come at a cheaper price than UAVs DLs because they are not limited by size.
    - Another takeaway is that they are more universal in the quantity of chips that can be used to track whatever is needed in the business specs without having to pay extra for unnecessary sensors.<br><br>

&emsp; &emsp; The last type of vehicle is USVs. From current findings, this is the most expensive type since they must be completely waterproof. This big difference is observed in the solutions presented that are currently available.
1.	Lowell Instruments Orientation Acceleration Temperature DL [7]
    - Pros
      - It includes 3 of the 5 sensors that Team 3 DLs will have.
      - Has a battery that runs for months to year.
      - Can be used on land and sea.
    - Cons
      - Comes at a higher price of $950.00
      - Battery is not rechargeable and must be replaced.


2.	DST Magnetic Field Strength Data Recorder [8]
    - Pros
      - It includes 4 of the 5 sensors that the Team 3 DL will have.
      - Weighs 12 grams in the water.
    - Cons
      - Comes in at the highest price out of all the DLs at a price of $1350.00 per unit.
      - The software that is required to run it is sold adds an additional cost separate from the unit price.

3.	Takeaways
    - The biggest take away is that the GPS signal is unable to function the second that the DL hits the water. This makes one of the stakeholder’s desired sensors rendered useless.
    - Another takeaway is that with waterproofing the system the price goes up significantly to accommodate.<br><br>

&emsp; &emsp; From these findings, there are all kinds of different quality and prices of DL's that exist to accomplish the goals of Team 3's DL. If a company needs their DL to be usable for all 3 types of vehicles, they are looking at spending anywhere from $1430 - $2460 not including the shipping cost. With Team 3's DL, the costs will be significantly less, and there is no process required to combine one of these solutions with add-ons to fulfill all the specifications and constraints listed in this document. This will lead to Team 3's DL becoming the best solution available after development.<br><br>

## Measures of Success
&emsp; &emsp; To ensure the accuracy and consistency of the DL, comparisons will be made to equipment of each type. In addition, the efficiency of the DL will be observed. These will be checked using the following: 
1. Sensor Data Measurement
    - Each sensor will have readings taken for a set environment, and the data will be compared to sensors outside of the DL for accuracy.
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
    - The power system of the module shall be able to run all five sensors measuring data at the same time. 
    - The system shall run the MCU and SD card writing unit as well along with the sensors.
    - The system shall be rechargeable while onboard and last for more than one operation.
    - Success is found when the DL can run all five sensors, the MCU, and the SD card writer without part failure from current and voltage draw.
    - Success is also reliant on the power system running for longer than 1 day without recharging.<br> 
3. Data Processing and Transmission System
    - The power system of the module shall be able to run all five sensors measuring data at the same time. 
    - The system shall run the MCU and SD card writing unit as well along with the sensors.
    - The system shall be rechargeable while onboard and last for more than one operation.
    - Success is found when the DL can run all five sensors, the MCU, and the SD card writer without part failure from current and voltage draw. <br>
4. Data Storage System
    - With the data now in uLog format, it must be transmitted to the SD Card writer to write the data onto an SD card to be observed after operation. 
    - Success can be observed when an SD card put into the writer can be taken out and read off the SD card with timestamps indicated for each set of data. <br>
5. System Consistency in Different Environments 
    - This DL must be able to function properly in any environment. 
    - This measure will be met when the DL consistently gains accurate information on the SD card from the sensors in multiple different environments.<br><br>

&emsp; &emsp; All these indications are important to the success of the DL, but it is not a complete success unless it meets the criteria listed earlier in this document as well.<br><br>


## Resources
&emsp; &emsp; The necessary resources expected for our data logger drone attachment mostly correspond to the creation of a specifically designed PCB, and the components and sensors associated with the final design. This data logger will collect information regarding GPS position, altitude, temperature, and pressure. This logger will be able to write to a microSD card for removable storage as well as house a battery. 


Timeline
*Gantt Chart in progress*


### Budget
The budget given by Valinor Dispatch for this project ranges from $2k - $3k, but the expected costs fall below this threshold. For physical components including the PCB we are expecting a total cost around $150, this includes the MCU and the programmer. Another $50 has been budgeted for any external casing that will be needed. 

### Personel
Team 3 
- Nicolas Campbell: System Health Analysis, Circuitry, KiCad, Labview, Control Systems
- Lucy Dunn: C/C++, VHDL, Assembly, LTSpice, Soldering, Embedded Systems
- Sean Ottaway: PCB Design, Circuitry, Mechanical Systems KiCad, C/C++ Programming
- Gabriel Simpkins: Microcontrollers, C/C++, Soldering, Circuit Analysis
- Andrew Singletary
  - Current Skills: Signal Processing, Circuit Analysis, C/C++
  - Skills to Learn: Embedded Systems, Microcontroller Processing, PCB Assembly

Other Personnel
•	Planned Supervisor: Dr. Tarek Elfouly
•	Valinor Dispatch Contact: John Cain
•	Instructor: Dr. Christopher Storm Johnson

### Timeline
** Gantt Chart in Progress ** <br><br>

## Specific Implications

&emsp; &emsp; There are many benefits to the DL that Team 3 is developing. The solution for onboard data measurement and storage for autonomous vehicles with this DL can be viewed in four major sets of implications: 

#### *Technical Implications*

&emsp; &emsp; Developing a data logging module is an in-depth hands-on project. There is quite a bit of component research and testing that needs to be conducted. While there are readily available and universal off the shelf units, this DL is designed specifically for the company's autonomous vehicles and is much more cost effective than the competitors. This DL collects data from onboard sensors that measure GPS time stamps, pressure, temperature, electromagnetic fields, and writes the data to a micro-SD card. This unit is self-contained and features its own battery power source with support for USB-C charging.  

#### *Manufacturing Implications*  

&emsp; &emsp; This DL is designed to use readily manufactured and widely available components. The module features its own PCB that can be easily manufactured by most PCB manufacturing companies without going through a custom manufacturer. The cost to develop and manufacture the DL will be well under the $3,000.00 budget allocated for the project.  

#### *Operational Implications*  

&emsp; &emsp; This DL is developed to be a self-contained unit that utilizes the shelf components that do not require maintenance intervals. If one of the DLs malfunctions or needs to be replaced, a new one can be easily swapped in without requiring the knowledge of an engineer.  

#### *Strategic Implications*  

&emsp; &emsp; This DL is designed specifically to integrate with the company's already existing autonomous vehicles and can be mounted or affixed anywhere the company would like and does not need any extra connections, excluding the battery charging cable.<br><br>

&emsp; &emsp; With all these implications, the DL will benefit the stakeholder's needs for autonomous vehicle data logging in many ways to help with further development of their autonomous charging stations and other technology.<br><br>

## Broader Implications, Ethics, and Responsibility as Engineers
&emsp; &emsp; Due to the rising issue of public trust with data collecting technology, a device such as this DL measuring environmental conditions and saving this data could pose global and societal implications. While the DL is only used to collect information about the environment and collects time stamps regarding the autonomous vehicle, the sensors the DL utilizes might lead to public distrust as the sensors can be implemented to collect unsolicited information. These implications are not as important since the DL will not be widely available for this to occur.  

&emsp; &emsp; A device such as this DL contains and implements various modules that can potentially be used for intrusive surveillance. This could further influence the modern and ongoing public trust issues that are present within the tech industry in terms of selling private information. With this DL, any extra "features" that could be added to the DL might bring ethical issues such as using GPS tracking for purposes outside the DL's scope as well as sensitive location data logged by the DL.  

&emsp; &emsp; Environmental implications would cover the operations and carbon footprint of the manufacturing process for the DL. This DL uses special sensors and components that are manufactured using semiconductors and other materials. Accessibility to these components could pose an issue with few locations being able to manufacture and procure these semiconductors found in the DL. A way to avoid this issue would be to use components that are readily available and manufactured from trusted and well-known companies to prevent addition difficulties from obtaining more obscure materials. Another potential issue would be the module detaching from the vehicle during operation, potentially disrupting aquatic and terrestrial life as well as their environments. To prevent this, the DL will have support for rugged mounting hardware to keep the module from affecting wildlife and the environment. 

&emsp; &emsp; In terms of economic implications, choosing and pricing components come into play. As engineers, we need to come up with a good and economical price to return on investment value to deliver the best piece of hardware for the right cost. If the sensors and components are too cheap, we might face issues with reliability, causing complications for the company and the vehicles utilizing them. If the project is too expensive, the company would lose their investment in the development of the module. This will be a major focus of the DL to be not very expensive while still utilizing trusted technology to get the job done. 

&emsp; &emsp; With the development and planning of this module, there are important ethical considerations when it comes to the operation and implementation of the DL. The team of engineers responsible for the development of this project must consider the previously mentioned implications and adhere to the following ethical standards:
- Team members who are responsible for the software will program the modules to only capture data within the project scope.
- Team members who are responsible for hardware will construct and develop the DL to comply with basic safety standards as well as staying within project scope.<br><br>

## References

[1] J. Sanchez, “Ruggedized Storage for UAV/Drone Data Logging: Why Consumer-Grade Storage Falls Short,” Delkin Industrial, Jan. 28, 2026. https://www.delkin.com/blog/rugged-uav-data-logging-storage/ (accessed Oct. 09, 2026).  

[2] “Drone Simulation,” www.mathworks.com. https://www.mathworks.com/discovery/drone-simulation.html (accessed Oct. 09, 2026).  

[3] “Federal Hazardous Substances Act (FHSA) Requirements,” CPSC.gov, Apr. 04, 2016. https://www.cpsc.gov/Business--Manufacturing/Business-Education/Business-Guidance/FHSA-Requirements (accessed Oct. 09, 2026). 

[4] Yost Labs, "3-Space™ Data Logger Nav with BLE & GPS,” Yost Labs, https://yostlabs.com/product/data-logger-nav-ble-gps/?srsltid=AU7gw4WEJ3qvT_4odsTwyClEaaVQxsDjtb8ClRZoBbiuZgtiw0GERoP8 (accessed Oct. 08, 2026) 

[5] MAPIR, “DAQ-A,” MAPIR, 2026. https://www.mapir.camera/products/daq-a (accessed Oct. 08, 2026). 

[6] “SparkFun DataLogger IoT - 9DoF,” Sparkfun.com, 2025. https://www.sparkfun.com/sparkfun-datalogger-iot-9dof.html (Accessed Oct. 08, 2026). 

[7] “IMU-GPS - Gulf Coast Data Concepts,” Gulf Coast Data Concepts - Simple yet versatile data acquisition, Sept. 06, 2024. https://gulfcoastdataconcepts.com/index.php/product/imu-gps/ (Accessed Oct. 08, 2026). 

[8] Lowell Instruments, LLC, “Universal User Guide for TCM-x Current Meters, MAT-1 Data Logger, and Domino Software.” Lowell Instruments, LLC, East Falmouth, MA 02536, Feb. 2022. Accessed: Oct. 08, 2026. [Online]. Available: https://www.onsetcomp.com/sites/default/files/2025-07/Universal_User_Guide_Lowell_CurrentMeters_Loggers.pdf 

[9] “DST Magnetic Field Strength Data Recorder,” MicroDAQ, LLC, 2026. https://microdaq.com/star-oddi-dst-magnetic-field-strength-data-recorder.php (accessed Oct. 08, 2026). 

## Statement of Contributions
These are the contributions the team made to this document:<br><br>
Nicolas Campbell: Survey of Existing Solutions<br>
Lucy Dunn: Resources, Budget, Timeline, & Personnel<br>
Sean Ottaway: Specific Implications & Broader Implications<br>
Gabriel Simpkins: Background, Specifications, & Constraints<br>
Andrew Singletary: Introduction, Measures of Success, & Broader Implications

