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
The Data Logger (DL) has several specifications and constraints given by this project's stakeholders as well as electrical and communication governing bodies required for the project:

#### Specifications
1.	Physical Attributes
- The DL shall be less than 500g in mass
- The DL shall be entirely self-contained
- The DL shall be wallet sized (Approx. 1in x 3in x 4in.)
- The DL may be easily attached to the outside of a UAS, UGV, or USV

2.	Electronics
- The DL shall have an onboard battery with enough charge to run multiple missions without being recharged
- The DL shall record the following types of data
  - Acceleration and velocity
  - Magnetic field strength
  - Temperature
  - Pressure
  - Absolute time
- The DL shall have an embedded LED active when data is being logged
- The DL may use recommended MCU (STM32G474RET6) and JST connections for software updates and changes

3.	Data
- The DL shall write timestamped data onto an SD (or microSD) card in uLog format
- Data shall be measured at a high enough resolution to be unimpeachable
- The DL may follow Federal Communications Commission (FCC) regulations on radio transmitters and receivers for this prototype

#### Constraints
1.	General Operation Constraints
- The DL project budget shall not exceed $3,000
- The DL shall have a large operating temperature and pressure range (-20ºC ~ 60ºC)

2.	Safety and Compliance Constraints
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
- The main takeaway with this type of DL is that they are highly priced for the size of the units.  These vehicles must come with a baseline of an IMU and GPS to be operational. These takeaways will be considered for Team 3’s DL.

&emsp; &emsp; The next type of vehicle, UGV's, use all the same sensors that UAV's use. The main difference between them is the box containing the DL for UGV's should be more dust protectant and vibration proof. Here are some of the solutions currently available for UGV's.
1.	SparkFun DataLogger IoT- 9DoF [5]
- Pros
  - Comes at the cheapest price as any on this list at $79.95
  - Is built to be a full Plug-and-Play IoT ecosystem meaning that sensors on their supported list can be plugged directly into the board and work immediately without coding them in.
- Cons
  - Where it is a full Plug-and-Play IoT ecosystem, the $79.95 price tag only comes with the base sensors, and this includes the IMU and Magnetometer. Everything else has to be purchased after hand.
  - Does not come inside of a rigid box and is just the board by itself.

2.	Gulf Coast Data Concepts IMU-GPS [6]
- Pros
  - Comes with 4 of the 5 sensors that the Team 3 DL will be using.
  - Does come inside of the dust proof box
- Cons
  - Comes at the Higher Price of $360.
  - Comes at a bigger size than Team 3’s stakeholder's desire.

3.	Takeaways
- One Main Takeaway from the UGVs DLs is that they come at a cheaper price than UAVs DLs because they are not limited by size. In addition, they are more universal in the quantity of chips that can be used to track whatever is needed in the business specs without having to pay extra for unnecessary sensors.	

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
- The biggest take away is that the GPS signal is unable to function the second that the DL hits the water. This makes one of the stakeholder’s desired sensors rendered useless. Another takeaway is that with waterproofing the system the price goes up significantly to accommodate.

&emsp; &emsp; From these findings, there are all kinds of different quality and prices of DL's that exist to accomplish the goals of Team 3's DL. If a company needs their DL to be usable for all 3 types of vehicles, they are looking at spending anywhere from $1430 - $2460 not including the shipping cost. With Team 3's DL, the costs will be significantly less, and there is no process required to combine one of these solutions with add-ons to fulfill all the specifications and constraints listed in this document. This will lead to Team 3's DL becoming the best solution available after development.

## Measures of Success
- Andrew

## Resources
- Lucy

### Budget

### Personel

### Timeline

## Specific Implications

## Broader Implications, Ethics, and Responsibility as Engineers

## References

## Statement of Contributions
