### Chapter 2 Kimball Dimensional Modeling Techniques Overview
- This chapter is intended to be an official list of Kimball Dim techniques and will serve as a reference to each technique. 
#### Fundamental Concepts
1. Gather business requirements and data realities
	- Chapter 1 DW/BI and Dimensional Modeling Primers
	- Chapter 3 Retail Sales
	- Chapter 11 Telecommunications
	- Chapter 17 Lifecycle Overview
	- Chapter 18 Dimensional Modeling Process and Tasks
	- Chapter 19 ETL Subsystems and Techniques

#### Collaborative Dimensional Modeling Workshops
Dimension models should be designed with other business representatives such as subject matter experts
- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 18 Dimensional Modeling Process and Tasks”

#### “Four-Step Dimensional Design Process
The four steps are
1. Select business process
2. declare the grain
3. identify the dimensions
4. identify the facts

From there the design team determines:
1. table and column names
2. sample domain values
3. business rules

Appears in:
- Chapter 3 Retail Sales
- Chapter 11 Telecommunications
- Chapter 18 Dimensional Modeling Process and Tasks

##### Business Process
Business processes are the operational activities, such as processing an insurance claim.
These business process events generate or capture performance metrics that translate into facts into a fact table.


##### Grain
Declaring the grain establishes what a single fact table row represents. Every dimension or fact table henceforth must be consistent with this declared grain.
`Atomic grain` refers to the lowest level in which data is captured by a given project. 
It is strongly encouraged to start with atomic-grained data since you can always roll-up the data, but you can't roll down the data.

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 6 Order Management
- Chapter 11 Telecommunications
- Chapter 12 Transportation
- Chapter 18 Dimensional Modeling Process and Tasks

##### Dimensions for Descriptive Context
Dimensions provide the “who, what, where, when, why, and how” context surrounding a business process event

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 11 Telecommunications
- Chapter 18 Dimensional Modeling Process and Tasks
- Chapter 19 ETL Subsystems and Techniques

##### Facts for measurements
Facts are the measurements that result from a business process event and are almost always numeric.
A single fact table row has a one to one relationship to measurements as described by the fact table's grain

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 18 Dimensional Modeling Process and Tasks

##### Star Schemas and OLAP Cubes


