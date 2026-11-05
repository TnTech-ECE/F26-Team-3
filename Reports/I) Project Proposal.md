# <div align="center">Project Proposal - Team 3</div>
<div align="center">Nicolas Campbell, Lucy Dunn, Sean Ottaway, Gabriel Simpkins, & Andrew Singletary</div>


## Introduction
&emsp; &emsp; Unmanned vehicles can be found all over the world being used widely to understand the environment they are being used in without using human resources. Because the environment is a big factor in all parts of the industry, there is a strong drive to improve these vehicles to withstand any condition. Data loggers gain such information about these different environments, but often they can only function on one type of vehicle, measure individual elements of the environment, or format information poorly. This causes inefficiency and higher costs to obtain this critical information. 

&emsp; &emsp; To address these needs, Team 3 is conducting research and development to find a lower-cost, modular, and mass-producible data logger module able to obtain accurate time stamps and measure magnetic fields, temperature, pressure, and dynamic movement around these vehicles. Once this data logger obtains these measurements, it will be able to write this information in uLog formatting onto a microSD card to be easily understood and interpreted. This self-contained system will integrate five sensors, a microcontroller, and a power source while being mountable to unmanned vehicles and staying under $3,000 for the process of developing the module. This project is being developed for Valinor Dispatch to help with analysis of environments for various tasks of their unmanned vehicles and the health of these vehicles in these environments.   

&emsp; &emsp; This proposal outlines the background of Data Loggers and a thorough evaluation of existing solutions. It will address the difficulties involved with such an embedded system and further elaborate on the need for this project. This will distinguish the restrictions on the data logger along with definitions of the measurements of success for the data logger. It will present the details of the budget, proficiencies of the team and assisting experts, the timeline with milestones of the project, and more about the stakeholder of this project, Valinor Dispatch. Finally, the proposal will end by discussing the implications of success and ethics concerns related to this data logger. 


## Formulating the Problem
&emsp; &emsp; For data measurement, unmanned vehicles (UVs) typically only have an onboard IMU and do not have dedicated memory drives for data tracking. The Data Logger will be able to track IMU data, temperature, pressure, magnetic field strength, and log all of this data with absolute-time timestamps. Dedicated data logger units like this one exist only at high price points or high footprints. The Data Logger being designed in this project must be portable and easily transferable to any unmanned vehicles. A dedicated unit for data tracking will free up the UV to focus on navigation and achieve the task given to it while gaining more accurate data. This can help the user learn more about environments for future tasks of any UV with tasks in the same area. 


### Background
&emsp; &emsp; Recording data for environments is critical for consistent operations. Rough terrain and harsh environments make recording data from UVs difficult [6]. Recording environmental data can help the user learn more about potential hazards and environmental changes to impact the success of the UV in its task. Data like this can inform critical decision-making for the desired task to get done. These can also be important to track for simulation purposes. Tracking these data points (IMU data, temperature, pressure, magnetic field strength) can help to make simulations of the UV environments more accurate, leading to better maneuverability control and an improved UV model to be used in the future [1]. 

&emsp; &emsp; Designing a product that meets all the criteria provided for this project requires a knowledge of sensors, embedded systems, MCUs, and PCB design. Some specific topics related to these areas are sensor fusion, data denoising, and understanding of serial communication, which include Inter-Integrated Circuit (I2C) and Serial Peripheral Interface (SPI). Here are some specifics on these topics.

1. Sensor Fusion

&emsp; &emsp; With this data logger utilizing multiple types of sensors all at once, it is not as complicated to implement a data logger if the information from each sensor is processed separately. That said, Tam 3's DL will be using DSP in the way of Sensor Fusion by utilizing the information of all sensors together to imply the type of environment that the vehicle the DL is mounted to is in. This makes the project more complicated to be able to achieve this goal. [7]. This is going to be very important to make Team 3's DL unique and stand out from other data loggers on the market. 

2. Data Denoising

&emsp; &emsp; Data denoising is extremely important to be able to use data coming from any of the sensors on a data logger since there is noise in every signal whether it is desired or not. This means that Team 3 will need a method to handle the noise. Data denoising will make this DL more involved in the program to handle the noise without eliminating the signal entirely [12]. This will be an important consideration during the development of the DL. 

3. Serial Communication

&emsp; &emsp; Serial communication is one of the most important parts of a data logger since this project requires the use of multiple sensors all at once. This means that it gets more complicated for the team since it is required to program custom drivers to handle I2C from some of the sensors and SPI from others. Since SPI requires more lines connected to the MCU than the I2C, this means the connections made from the sensors to the MCU also cannot be done the same way. Lastly, I2C is inherently slower than SPI in communication since it has less lines to utilize for communication, but SPI is more difficult to scale with more lines required [10]. While I2C and SPI are not the only serial communication types, they are among the most used in the industry. These principles are important for Team 3 to know how to develop this DL. 

&emsp; &emsp; In addition to addressing all these topics, this product will have to meet several specifications and constraints set by Valinor Dispatch, governing bodies, or Team 3. While there are other comparable solutions, many fall short of the desired specifications of this project and achieve all these topics. These alternative solutions are taxing on the budget, don’t measure all the required data, don’t store the data to be observed in the future, or do not achieve all the important principles listed above. In addition, they are often too large to be portable and transferable to other types of UVs without modification. With this background, Team 3's Data Logger will aim to achieve these goals, but what are all the specifications for this project. 


### Specifications and Constraints
&emsp; &emsp; Team 3's Data Logger (DL) has many specifications and constraints given by Valinor Dispatch as well as electrical and communication governing bodies required for the project. These specifications are to help Valinor evaluate the environments their unmanned vehicles are working in and help improve their vehicles based on the performance of them inside these environments. Here are the specifics for this DL project: 


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
- The DL shall utilize Sensor Fusion to understand the environment around the vehicle the DL is mounted to
- The DL may follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers for this prototype


#### Constraints
1\.	General Operation Constraints
- The DL project budget shall not exceed $3,000
- The DL shall have a large operating temperature range (-20ºC ~ 60ºC)

2\.	Standards and Safety Constraints
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act [2]
- The DL shall be subject to IP67 rating for Dust and Water resistance [5] 
- The DL shall conform to IEEE standards for thermal disipation and handheld devices [3]
- The DL shall ensure the module and battery are properly grounded, avoiding electrical shorts or shock as laid out in Article 250 of NFPA 70 [9]
- The DL shall use a low voltage battery (<50V) to follow general low voltage electronics protocol and regulation



## Survey of Existing Solutions
&emsp; &emsp; When looking at Existing Solutions, the traditional data logger has a minimum of at least 3 of the 5 sensors that Team 3 will be using. This helps make it a standalone data logger and does not require use of any onboard sensors of the vehicle it is mounted to. This gives the user a second source of data that can help verify the sensor data on the Unmanned Vehicle. This Survey of Existing Solutions shall look at the separate data loggers for various types of Unmanned Vehicles.  

&emsp; &emsp; The first type of UV, UAV's, typically requires its data logger to have the capability to utilize all 5 sensors that are going to be used in this project. There are many solutions currently available, however none of the existing solutions that were found used all 5. Here are some of the solutions Team 3 has found while researching for existing solutions. 

1.	YOST LABS 3-Space Data Logger Nav with BLE & GPS [13]
    - Pros
        - Has 4 out of the 5 sensors that shall be used in Team 3’s DL.
        - Has a custom tracking engine that is able to pick up everywhere that GPS is not available to track.
        - Has the option for both MicroSD card data logging or can send its data via Bluetooth
    - Cons 
        - Does not come with the thermometer
        - Comes at a High Price Tag of $750 per unit

2.	Mapir DAQ-A [8]
    - Pros
      - Comes at a cheaper price of $400 per unit 
      - Has support for the companies Camera exposure logging
    - Cons
      - Does not come with an on-board battery
      - Does not come with a barometer, thermometer, or magnetometer

3.	Takeaways
    - The main takeaway with data loggers for this type of UV is that they are highly priced for the size of the units.  These vehicles must come with a baseline of an IMU and GPS to be operational. These takeaways will be considered for Team 3’s DL. <br><br>

&emsp; &emsp; The next type of vehicle, UGV's, typically utilizes all the same sensors as a typical data logger for UAVs. The main difference between them is the containment or mounting of the data logger used for UGV's since it should be more dust protectant and vibration proof. Here are some of the solutions currently available for UGV's. 

1.	SparkFun DataLogger IoT- 9DoF [11]
    - Pros
      - Comes at the cheapest price as any on this list at $79.95
      - Is built to be a full Plug-and-Play IoT ecosystem meaning that sensors on their supported list can be plugged directly into the board and work immediately without coding them in
    - Cons
      - Where it is a full Plug-and-Play IoT ecosystem, the $79.95 price tag only comes with the base sensors, and this includes the IMU and Magnetometer. Everything else has to be purchased after obtaining this particular data logger.
      - Does not come inside of a rigid box and is just the board by itself

2.	Gulf Coast Data Concepts IMU-GPS [4]
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


## Measures of Success
&emsp; &emsp; To ensure the accuracy and consistency of the DL, comparisons will be made with established units of various types to ensure the measurements are accurate. In addition, the efficiency of the DL will be verified so Team 3's DL will become the best solution. These will be checked using the following measurements of success: 
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

&emsp; &emsp; All these indications are important to the success of the DL, but it is not a complete success unless it meets the criteria listed previously in this document as well. <br><br>


## Resources
&emsp; &emsp; The necessary resources expected for Team 3's DL mostly correspond to the creation of a specifically designed PCB along with the components and sensors associated with the final design. This DL will collect information regarding GPS position, altitude, temperature, and pressure. It will be able to write to a microSD card for removable storage as well as house a battery. An important consideration is the personnel working on the project. Listed below are the resources and how they are expected to be utilized throughout the development of this DL.


### Timeline
![Capstone Gantt](https://hackmd.io/_uploads/HymNoo73Gl.png)


### Budget
The budget given by Valinor Dispatch for this project ranges from $2k - $3k, but the expected costs will fall below this threshold. For physical components including the PCB, it is expected that the total cost will be around $150, which includes the MCU and the programmer. Another $50 has been budgeted for any external casing that will be needed.  


### Personel
Team 3 
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

Other Personnel
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

[2] “Federal Hazardous Substances Act (FHSA) Requirements,” CPSC.gov, Apr. 04, 2016. https://www.cpsc.gov/Business--Manufacturing/Business-Education/Business-Guidance/FHSA-Requirements (accessed Oct. 09, 2026). 

[3] IEEE, “Handheld Devices,” IEEE Technology Navigator, 2026. https://technav.ieee.org/topic/handheld-devices/ (accessed Oct. 22, 2026).

[4] “IMU-GPS - Gulf Coast Data Concepts,” Gulf Coast Data Concepts - Simple yet versatile data acquisition, Sept. 06, 2024. https://gulfcoastdataconcepts.com/index.php/product/imu-gps/ (Accessed Oct. 08, 2026). 

[5] International Electrotechnical Commission, “IP Ratings | IEC,” www.iec.ch, 2024. https://www.iec.ch/ip-ratings (accessed Oct. 21, 2026). 

[6] J. Sanchez, “Ruggedized Storage for UAV/Drone Data Logging: Why Consumer-Grade Storage Falls Short,” Delkin Industrial, Jan. 28, 2026. https://www.delkin.com/blog/rugged-uav-data-logging-storage/ (accessed Oct. 09, 2026).  

[7] J. Z. Sasiadek, “Sensor Fusion,” IFAC Proceedings Volumes, vol. 33, no. 27, pp. 1–3, Sept. 2000, doi: 10.1016/s1474-6670(17)37896-5.

[8] MAPIR, “DAQ-A,” MAPIR, 2026. https://www.mapir.camera/products/daq-a (accessed Oct. 08, 2026).

[9] National Fire Protection Association and National Fire Protection Association. National Electrical Code Committee, "Article 250," NEC 2017: NFPA 70 National Electrical Code. Quincy, Ma: National Fire Protection Association, 2016.

[10] None V.Muneeswaran, K. N. Kumar, None P.Manikandan, M. N. Kumar, C.Vishnu Chaithanya, and M. Ganga Priyadarshini, “Performance Analysis of Communication Protocols (I2C, SPI) for Embedded Applications With IMU Sensor Using Verilog,” pp. 685–689, Apr. 2025, doi: 10.1109/ictmim65579.2025.10988065.

[11] “SparkFun DataLogger IoT - 9DoF,” Sparkfun.com, 2025. https://www.sparkfun.com/sparkfun-datalogger-iot-9dof.html (Accessed Oct. 08, 2026). 

[12] S. Yu, J. Ma, and W. Wang, “Deep Learning for Denoising,” Geophysics, vol. 84, no. 6, pp. V333-V350, July 2019, doi: 10.1190/geo2018-0668.1.

[13] Yost Labs, "3-Space™ Data Logger Nav with BLE & GPS,” Yost Labs, https://yostlabs.com/product/data-logger-nav-ble-gps/?srsltid=AU7gw4WEJ3qvT_4odsTwyClEaaVQxsDjtb8ClRZoBbiuZgtiw0GERoP8 (accessed Oct. 08, 2026) 

## Statement of Contributions
These are the contributions the team made to this document:<br><br>
Nicolas Campbell: Survey of Existing Solutions<br>
Lucy Dunn: Resources, Budget, Timeline, & Personnel<br>
Sean Ottaway: Specific Implications & Broader Implications<br>
Gabriel Simpkins: Background, Specifications, & Constraints<br>
Andrew Singletary: Introduction, Measures of Success, & Broader Implications
