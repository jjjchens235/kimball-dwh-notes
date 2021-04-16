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
- skipped

#### Basic Fact Table Techniques
##### Fact Table Structure
- Fact table contains numeric measures produced by operational measurable events
- The fact table design should be based on physical events and not on the eventual reports that may be produced
- In addition to numerical values, a fact table will contain FK for each dim
##### Additive, Semi-Additive, Non-Additive Facts
Three categories of numerical facts
- full additive: these measures can be summed across any dimension
- semi additive:  can be summed across some dimensions, i.e balance amounts can't be summed across time
- non-additive: i.e. ratios

##### Nulls
- Null values in numerical fields are fine- aggregate functions handle these perfectly
- However nulls are to be avoided as FK, the dim table should have a default row representing null values

##### Conformed Facts
- If the same measurement appears in separate fact tables, consistent, but separate fact table definitions are known as `conformed facts`
	- if conformed fact, make sure to name identically in each table
	- if inconsistently measured, be sure to name differently so that this alerts end business users

##### Transaction Fact tables
A row in a `transaction fact table` corresponds to a measurement event at a point in place and time.

##### Periodic Snapshot Fact tables
- A row in a periodic snapshot fact table summarizes many measurement events occurring over a standard period, such as a day, a week, or a month.
- The grain is the period, not the individual transaction.

##### Accumulating Snapshot Fact Tables
- A row in an accumulating snapshot fact table summarizes the measurement events occurring at predictable steps between the beginning and the end of a process.

##### Factless fact tables
- Fact tables that do not have any numerical facts associated with it
- Example would be a fact table tracking student attending class

##### Aggregate fact tables or OLAP cubes
- aggregate fact tables roll up atomic fact tables for the purpose of query performance

##### Consolidated fact tables
- It can be convenient to combine facts from multiple processes together into a consolidated fact table, assuming these facts can be expressed in the same grain
- This makes things harder for the ETL processing, and easier for BI analytical apps

### Basic Dimension Table Techniques
#### Dimension Table Structure
