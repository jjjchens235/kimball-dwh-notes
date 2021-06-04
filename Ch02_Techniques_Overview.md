## Chapter 2 Kimball Dimensional Modeling Techniques Overview
- This chapter is intended to be an official list of Kimball Dimension techniques- meant to be used as a reference guide.
### Fundamental Concepts
1. Gather business requirements and data realities
	- Chapter 1 DW/BI and Dimensional Modeling Primers
	- Chapter 3 Retail Sales
	- Chapter 11 Telecommunications
	- Chapter 17 Lifecycle Overview
	- Chapter 18 Dimensional Modeling Process and Tasks
	- Chapter 19 ETL Subsystems and Techniques

### Collaborative Dimensional Modeling Workshops
Dimension models should be designed with other business representatives such as subject matter experts
- Chapters:
	- Chapter 3 Retail Sales
	- Chapter 4 Inventory
	- Chapter 18 Dimensional Modeling Process and Tasks”

### Four-Step Dimensional Design Process
The four steps are
1. Select business process
2. declare the grain
3. identify the dimensions
4. identify the facts

From there the design team determines:
1. table and column names
2. sample domain values
3. business rules

- Chapters:
	- Chapter 3 Retail Sales
	- Chapter 11 Telecommunications
	- Chapter 18 Dimensional Modeling Process and Tasks

#### Business Process
Business processes are the operational activities, such as processing an insurance claim.
These business process events generate or capture performance metrics that translate into facts into a fact table.


#### Grain
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

#### Dimensions for Descriptive Context
Dimensions provide the “who, what, where, when, why, and how” context surrounding a business process event

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 11 Telecommunications
- Chapter 18 Dimensional Modeling Process and Tasks
- Chapter 19 ETL Subsystems and Techniques

#### Facts for measurements
Facts are the measurements that result from a business process event and are almost always numeric.
A single fact table row has a one to one relationship to measurements as described by the fact table's grain

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 18 Dimensional Modeling Process and Tasks

#### Star Schemas and OLAP Cubes
- skipped

### Basic Fact Table Techniques
##### Fact Table Structure
- Fact table contains numeric measures produced by operational measurable events
- The fact table design should be based on physical events and not on the eventual reports that may be produced
- In addition to numerical values, a fact table will contain FK for each dim

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 5 Procurement
- Chapter 6 Order Management

##### Additive, Semi-Additive, Non-Additive Facts
Three categories of numerical facts
- full additive: these measures can be summed across any dimension
- semi additive:  can be summed across some dimensions, i.e balance amounts can't be summed across time
- non-additive: i.e. ratios

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 7 Accounting

##### Nulls
- Null values in numerical fields are fine- aggregate functions handle these perfectly
- However nulls are to be avoided as FK, the dim table should have a default row representing null values

- Chapter 3 Retail Sales
- Chapter 20 ETL System Process and Tasks

##### Conformed Facts
- If the same measurement appears in separate fact tables, consistent, but separate fact table definitions are known as `conformed facts`
	- if conformed fact, make sure to name identically in each table
	- if inconsistently measured, be sure to name differently so that this alerts end business users

- Chapter 4 Inventory
- Chapter 16 Insurance

##### Transaction Fact tables
A row in a `transaction fact table` corresponds to a measurement event at a point in place and time.

- Chapter 3 Retail Sales
- Chapter 4 Inventory
- Chapter 5 Procurement
- Chapter 6 Order Management
- Chapter 7 Accounting
- Chapter 11 Telecommunications
- Chapter 12 Transportation
- Chapter 14 Healthcare
- Chapter 15 Electronic Commerce
- Chapter 16 Insurance
- Chapter 19 ETL Subsystems and Techniques

##### Periodic Snapshot Fact tables
- A row in a periodic snapshot fact table summarizes many measurement events occurring over a standard period, such as a day, a week, or a month.
- The grain is the period, not the individual transaction.

- Chapter 4 Inventory
- Chapter 7 Accounting
- Chapter 9 Human Resources Management
- Chapter 10 Financial Services
- Chapter 13 Education
- Chapter 14 Healthcare
- Chapter 16 Insurance
- Chapter 19 ETL Subsystems and Techniques

##### Accumulating Snapshot Fact Tables
- A row in an accumulating snapshot fact table summarizes the measurement events occurring at predictable steps between the beginning and the end of a process.

- Chapter 4 Inventory
- Chapter 5 Procurement
- Chapter 6 Order Management
- Chapter 13 Education
- Chapter 14 Healthcare
- Chapter 16 Insurance
- Chapter 19 ETL Subsystems and Techniques

##### Factless fact tables
- Fact tables that do not have any numerical facts associated with it
- Example would be a fact table tracking student attending class

- Chapter 3 Retail Sales
- Chapter 6 Order Management
- Chapter 13 Education
- Chapter 16 Insurance

##### Aggregate fact tables or OLAP cubes
- aggregate fact tables roll up atomic fact tables for the purpose of query performance

- Chapter 15 Electronic Commerce
- Chapter 19 ETL Subsystems and Techniques
- Chapter 20 ETL System Process and Tasks

##### Consolidated fact tables
- It can be convenient to combine facts from multiple processes together into a consolidated fact table, assuming these facts can be expressed in the same grain
- This makes things harder for the ETL processing, and easier for BI analytical apps

- Chapter 15 Electronic Commerce
- Chapter 19 ETL Subsystems and Techniques
- Chapter 20 ETL System Process and Tasks

### Basic Dimension Table Techniques
#### Dimension Table Structure

- Every dimension table has a single PK column, these PK are embedded as FK in associated fact table

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales
- Chapter 11 Telecommunications

#### Dimension Surrogate Keys
- the dim table is designed to have 1 column serving as its primary key
- The PK should not be the natural key (i.e SSN)
- The PK should instead be surrogate keys (SERIAL type in Postgres)
- The only exception to this rule are date dim tables, you can use the date itself

- Chapter 3 Retail Sales
- Chapter 19 ETL Subsystems and Techniques
- Chapter 20 ETL System Process and Tasks

#### Natural, Durable, and Supernatural keys
- Natural keys are created by OLTP source systems and are subject to business rules outside of the system
- Let's take the example of an employee quitting and then being re-hired, their employee ID may have changed so using natural key isn't a good idea
- A `durable` key is one that is persistent and wouldn't change in this situation.
	- This key is sometimes referred to as a durable supernatural key.
	- The best durable keys have a format that is independent of the original business process and thus should be simple integers assigned in sequence beginning with 1.
	- Note that in Ch 3, it is stated that the supernatural key is handled as a dimension attribute and is not a replacement for the surrogate (serial) primary key

- Chapter 3 Retail Sales
- Chapter 20 ETL System Process and Tasks
- Chapter 21 Big Data Analytics

#### Drilling down
- Drilling down means adding a row header to an existing query, i.e GROUP BY

- Chapter 3 Retail Sales

#### Degenerate Dimensions
- Sometimes a dimension is defined that has no content except for its primary key. 

- Chapter 3 Retail Sales
- Chapter 6 Order Management
- Chapter 11 Telecommunications
- Chapter 16 Insurance

#### Denormalized Flattened Dimensions
- In general, dimensional designers must resist the normalization urges caused by years of operational database designs and instead denormalize the many-to-one fixed depth hierarchies into separate attributes on a flattened dimension row

- Chapter 1 DW/BI and Dimensional Modeling Primer
- Chapter 3 Retail Sales

#### Multiple Hierarchies in Dimensions
Many dimensions contain more than one natural hierarchy. For example, calendar date dimensions may have a day to week to fiscal period hierarchy, as well as a day to month to year hierarchy. Location intensive dimensions may have multiple geographic hierarchies. In all of these cases, the separate hierarchies can gracefully coexist in the same dimension table.

- Chapter 3 Retail Sales
- Chapter 19 ETL Subsystems and Techniques

#### Flags and Indicators as Textual Attributes
Cryptic abbreviations, true/false flags, and operational indicators should be supplemented in dimension tables with full text words that have meaning when independently viewed

- Chapter 3 Retail Sales
- Chapter 11 Telecommunications
- Chapter 16 Insurance

#### Null attributes in dimensions
- In dim tables null-value attributes should be replaced by a descriptive string such as 'Unknown'
- This is because different DB's handle groupings and null constraints differently

- Chapter 3 Retail Sales

#### Calendar date time dimensions
- Almost all fact tables will contain a FK to a date time dim table
- You would never compute a date in a fact table, you would always join with a date dim table.
- Surrogate key is not needed for date dim tables, can use natural key of YYYY-mm-dd

- Chapter 3 Retail Sales
- Chapter 7 Accounting
- Chapter 8 Customer Relationship Management
- Chapter 12 Transportation
- Chapter 19 ETL Subsystems and Techniques

#### Role-Playing Dimensions
- A single physical dimension can be referenced multiple times in a fact table, with each reference linking to a logically distinct role for the dimension.
- For instance, a fact table can have several dates, each of which is represented by a foreign key to the date dimension. 

- Chapter 6 Order Management
- Chapter 12 Transportation
- Chapter 14 Healthcare
- Chapter 16 Insurance

#### Junk Dimensions
- Transactional business processes typically produce a number of miscellaneous, low-cardinality flags and indicators.
- Rather than making separate dimensions for each flag and attribute, you can create a single junk dimension combining them together.
- This dimension, frequently labeled as a transaction profile dimension in a schema, does not need to be the Cartesian product of all the attributes' possible values, but should only contain the combination of values that actually occur in the source data.

- Chapter 6 Order Management
- Chapter 12 Transportation
- Chapter 16 Insurance
- Chapter 19 ETL Subsystems and Techniques

#### Snowflaked Dimensions
- [Snowflake_schema.jpg](https://www.softwaretestinghelp.com/wp-content/qa/uploads/2019/09/Snowflake-Schema.jpg)
- When a hierarchical relationship in a dimension table is normalized, low-cardinality attributes appear as secondary tables connected to the base dimension table by an attribute key.  
- Although the snowflake represents hierarchical data accurately, you should avoid snowflakes because it is difficult for business users to understand and navigate snowflakes.

- Chapter 3 Retail Sales
- Chapter 11 Telecommunications
- Chapter 20 ETL System Process and Tasks

#### Outrigger Dims
- A dimension can contain a reference to another dimension table.
- For instance, a bank account dimension can reference a separate dimension representing the date the account was opened.
- These secondary dimension references are called outrigger dimensions. Outrigger dimensions are permissible, but should be used sparingly. 

- Chapter 3 Retail Sales
- Chapter 5 Procurement
- Chapter 8 Customer Relationship Management
- Chapter 12 Transportation

### Integrated via Conformed Dimensions
Conformed Dims are simple, but is a powerful method to integrate data from different processes.

#### Conformed Dimensions
- Dim tables conform when attributes in separate tables have the same column names

- Chapter 4 Inventory
- Chapter 8 Customer Relationship Management
- Chapter 11 Telecommunications
- Chapter 16 Insurance
- Chapter 18 Dimensional Modeling Process and Tasks
- Chapter 19 ETL Subsystems and Techniques

### Enterprise Data Warehouse Bus Arch
- This architecture decomposes the DW/BI planning process into manageable pieces by focusing on business processes, while delivering integration via standardized conformed dimensions that are reused across processes.

### Enterprise Data Warehouse Bus Matrix
- The enterprise data warehouse bus matrix is the essential tool for designing and communicating the enterprise data warehouse bus architecture. 
- The rows are the matrix are business processes, and the columns are the dimensions

### Dealing with slowly changing dim attributes
There are different approaches with slowly changing dimensions (SCD)
1. Type 0 Retain Original
	- The dimension attribute value never changes, i.e any attribute labeled 'original' such as a customer's original credit card
	- Chapter 5 Procurement
1. type 1: Overwrite
	- The old attribute value in a dimension row is over-written with the new value
	- type 1 assignments always reflects the most recent assignment
	- Chapters:
		- Chapter 5 Procurement
		- Chapter 16 Insurance
		- Chapter 19 ETL Subsystems and Techniques
2. Type 2: Add new row
	- Type 2 changes add a new row in the dim with the updated attribute values
	- This requires creating a primary key that goes beyond just a natural key since there can be multiple rows describing each member
	- A minimum of 3 new rows needed to be added to the dim table for Type 2 changes
		1. row effective date
		2. row expiration date
		3. current row indicator
	- Chapters:
		- Chapter 5 Procurement
		- Chapter 8 Customer Relationship Management
		- Chapter 9 Human Resources Management
		- Chapter 16 Insurance
		- Chapter 19 ETL Subsystems and Techniques
		- Chapter 20 ETL System Process and Tasks
3. Type 3: Add New Attribute
	- A new attribute/field is added rather than overwriting as in type 1
	- This change is aptly referred to as `alternative reality`
	- Chapters:
		- Chapter 5 Procurement
		- Chapter 16 Insurance
		- Chapter 19 ETL Subsystems and Techniques
4. Type 4: Add mini dimension
	- The type 4 technique is used when a group of attributes in a dimension rapidly changes and is split off to a mini-dimension
5. Add Mini-Dimension and Type 1 Outrigger
	- The type 5 technique is used to accurately preserve historical attribute values, plus report historical facts according to current attribute values. Type 5 builds on the type 4 mini-dimension by also embedding a current type 1 reference to the mini-dimension in the base dimension
6. Type 6: Add Type 1 Attributes to Type 2 Dimension
Like type 5, type 6 also delivers both historical and current dimension attribute values.
	- Type 6 builds on the type 2 technique by also embedding current type 1 versions of the same attributes in the dimension row so that fact rows can be filtered or grouped by either the type 2 attribute value in effect when the measurement occurred or the attribute's current value
7. Dual Type 1 and Type 2 Dimensions
	- Type 7 is the final hybrid technique used to support both as-was and as-is reporting.
	- A fact table can be accessed through a dimension modeled both as a type 1 dimension showing only the most current attribute values, or as a type 2 dimension showing correct contemporary historical profiles.
	- The same dimension table enables both perspectives. Both the durable key and primary surrogate key of the dimension are placed in the fact table.

### Dealing with Dimension Hierarchies
#### Fixed Depth Positional Hierarchies
- A fixed depth hierarchy is a series of many-to-one relationships, such as product to brand to category to department. 
- A fixed depth hierarchy is easy to understand and navigate as long as:
	- The hierarchy is defined
	- Hierarchy levels have agreed upon names
	- Hierarchy should appear as separate positional attributes in a dimension table
- Chapters:
	- Chapter 3 Retail Sales
	- Chapter 7 Accounting
	- Chapter 19 ETL Subsystems and Techniques
	- Chapter 20 ETL System Process and Tasks

#### Slightly Ragged/Variable Depth Hierarchies
- Slightly ragged hierarchies don't have a fixed number of levels, but the range in depth is small.
- Geographic hierarchies often range in depth from perhaps three levels to six levels. 
- Chapter 7 Accounting

#### Ragged/Variable Depth Hierarchies with Hierarchy Bridge Tables
- Ragged hierarchies of indeterminate depth are difficult to model and query in a relational database.
- Solution is to use `bridge table`
- Chapters:
	- Chapter 7 Accounting
	- Chapter 9 Human Resources Management

#### Ragged/Variable Depth Hierarchies with Pathstring Attributes
- The use of a bridge table for ragged variable depth hierarchies can be avoided by implementing a pathstring attribute in the dimension.
- For each row in the dimension, the pathstring attribute contains a specially encoded text string containing the complete path description from the supreme node of a hierarchy down to the node described by the particular dimension row.
- Chapter 7 Accounting

### Advanced Fact Table Techniques
#### Fact Table Surrogate Keys
- Surrogate keys are used to implement the primary keys of almost all dimension tables.
- In addition, single column surrogate fact keys can be useful, albeit not required, for the following reasons:
	1. Used a single column PK of fact table
	2. serve as immediate identifier of fact table without navigating multiple dimensions
	3. Allow for interrupted load process to back out / resume
	4. allow fact table update operations to be decomposed into less risky inserts/deletes
- Chapters:
	- Chapter 3 Retail Sales
	- Chapter 19 ETL Subsystems and Techniques
	- Chapter 20 ETL System Process and Tasks

#### Centipede Fact Tables
- Some designers create separate normalized dimensions for each level of a many-to-one hierarchy, such as a date dimension, month dimension, quarter dimension, and year dimension, and then include all these foreign keys in a fact table.
- This results in a centipede fact table with dozens of hierarchically related dimensions.
- `Centipede fact tables should be avoided.`
- Chapter 3 Retail Sales

#### Numeric Values as Attributes or Facts
- Designers sometimes encounter numeric values that don't clearly fall into either the fact or dimension attribute categories.
- A classic example is a product's standard list price.
- If the numeric value is used primarily for calculation purposes, it likely belongs in the fact table.
- If a stable numeric value is used predominantly for filtering and grouping, it should be treated as a dimension attribute
- Chapters:
	- Chapter 3 Retail Sales
	- Chapter 6 Order Management
	- Chapter 8 Customer Relationship Management
	- Chapter 16 Insurance

#### Lag/Duration Facts
TODO

#### Header/Line Fact Tables
#### Allocated Facts
#### Profit and Loss Fact Tables Using Allocations
#### Multiple Currency Facts
- Fact tables that record financial transactions in multiple currencies should contain a pair of columns for every financial fact in the row.
- One column contains the fact expressed in the true currency of the transaction 
- And the other column contains the same fact expressed in a single standard currency that is used throughout the fact table.

#### Multiple Units of measure Facts
#### Year-to-Date Facts
#### Multipass SQL to Avoid Fact-to-Fact Table Joins
#### Timespan Tracking in Fact Tables
- It can be useful to add a row effective date, row expiration date, and current row indicator to the fact table, much like you do with type 2 slowly changing dimensions, to capture a timespan when the fact row was effective. 
#### Late Arriving Facts
- If a fact row arrives late, the relevant dimensions must be searched to find the dimension keys that were effective when the measurement event actually occurred.

### Advanced Dimension Techniques
#### Dimension-to-Dimension Table Joins
- Dimensions can contain references to other dimensions.
- these relationships can be modeled with outrigger dimensions
- in some cases, the existence of a foreign key to the outrigger dimension in the base dimension can result in explosive growth of the base dimension because type 2 changes in the outrigger force corresponding type 2 processing in the base dimension.
- Chapter 6 Order Management

#### Multivalued Dimensions and Bridge Tables
- In a classic dimensional schema, each dimension attached to a fact table has a single value consistent with the fact table's grain.
- But there are a number of situations in which a dimension is legitimately multivalued.
- For example, a patient receiving a healthcare treatment may have multiple simultaneous diagnoses

- Chapter:
	- Chapter 8 Customer Relationship Management
	- Chapter 9 Human Resources Management
	- Chapter 10 Financial Services
	- Chapter 13 Education
	- Chapter 14 Healthcare
	- Chapter 16 Insurance
	- Chapter 19 ETL Subsystems and Techniques

#### Time Varying Multivalued Bridge Tables
	- Chapter 7 Accounting
	- Chapter 10 Financial Services
#### Behavior Tag Time Series
	- Chapter 8 Customer Relationship Management 
#### Behavior Study Groups
	- Chapter 8 Customer Relationship Management
#### Aggregated Facts as Dimension Attributes
	- Chapter 8 Customer Relationship Management
#### Dynamic Value Bands
#### Text Comments Dimension
#### Multiple Time Zones
#### Measure Type Dimensions
#### Step Dimensions
#### Hot Swappable Dimensions
#### Abstract Generic Dimensions
#### Audit Dimensions
- A simple audit dimension row could contain basic indicators of data quality, perhaps deriving from error event schema
- Furthermore Kimball in his white-paper specifies the following requirements, sourced from [holistics blog](https://www.holistics.io/blog/data-quality-first-principles/):
	1. enable early diagnosis and triage of data quality issues
	2. Store specific descriptions of data errors
	3. Captures all data quality errors
	4. Generate time series data so that stored data quality scores can be measured over time
	5. Quality confidence metrics are always displayed alongside actual data
#### Late Arriving Dimensions
- Some times facts arrives before the associated dim context.
- In these cases, special dim rows are created with unresolved natural keys as attributes
- When the actual dim context is eventually supplied, the placeholder dime rows are updated with type 1 overwrites

### Special Purpose Schemas
- Error Event schemas: When a data quality screen detects an error, this event is recorded in a special dimensional schema.
#### Supertype and Subtype Schemas for Heterogeneous Products
#### Real-Time Fact Tables
#### Error Event Schemas
