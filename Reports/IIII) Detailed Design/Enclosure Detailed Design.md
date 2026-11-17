# Detailed Design

This document delineates the objectives of a comprehensive system design. Upon reviewing this design, the reader should have a clear understanding of:
- How the specific subsystem integrates within the broader solution
- The constraints and specifications relevant to the subsystem
- The rationale behind each crucial design decision
- The procedure for constructing the solution

## General Requirements for the Document

The document should include:
- Explanation of the subsystem’s integration within the overall solution
- Detailed specifications and constraints specific to the subsystem
- Synopsis of the suggested solution
- Interfaces to other subsystems
- 3D models of customized mechanical elements
- A comprehensive Bill of Materials (BOM)
- Analysis of crucial design decisions

## Function of the Subsystem

*This segment should elucidate the role of the subsystem within the entire system, detailing its intended function, aligned with the conceptual design.*

## Specifications and Constraints

*This section should provide a list of constraints applicable to the subsystem, along with the rationale behind these limitations.
Every subsystem must incorporate at least one constraint stemming from standards, ethics, or socio-economic factors.*

1\.	Physical Attributes
- The DL shall be less than 500g in mass
- The DL shall be entirely self-contained
- The DL shall be wallet sized (Approx. 1in x 3in x 4in.)
- The DL may be easily attached to the outside of a UAS, UGV, or USV

2\.	Electronics
- The DL shall have an onboard battery with enough charge to run for 24 hours without being recharged
- The DL shall have an embedded LED active when data is being logged

#### Constraints
1\.	General Operation Constraints
- This subsystem shall not exceed a cost of $200
- The DL shall have a large operating temperature range (-20ºC ~ 60ºC)

2\.	Standards and Safety Constraints
- The DL shall avoid hazardous materials in accordance with the Federal Hazardous Substances Act [1] 
- The DL shall be subject to IP67 rating for Dust and Water resistance [2]
- The DL shall conform to IEEE standards for thermal dissipation and handheld devices [3]
- The DL shall ensure the module and battery are properly grounded, avoiding electrical shorts or shock as laid out in Article 250 of NFPA 70 [4] 

## Overview of Proposed Solution

*Describe the solution and how it will fulfill the specifications and constraints of this subsystem.*

## Interface with Other Subsystems

*Provide detailed information about the inputs, outputs, and data transferred to other subsystems. Ensure specificity and thoroughness, clarifying the method of communication and the nature of the data transmitted.*

## 3D Model of Custom Mechanical Components

*Should there be mechanical elements, display diverse views of the necessary 3D models within the document. Ensure the image's readability and appropriate scaling. Offer explanations as required.*

## BOM

*Provide a comprehensive list of all necessary components along with their prices and the total cost of the subsystem. This information should be presented in a tabular format, complete with the manufacturer, part number, distributor, distributor part number, quantity, price, and purchasing website URL.*

## Analysis

*Deliver a full and relevant analysis of the design demonstrating that it should meet the constraints and accomplish the intended function. This analysis should be comprehensive and well articulated for persuasiveness.*

## References
