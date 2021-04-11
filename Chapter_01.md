## Chapter 1

#### Different worlds of data capture and analysis
1. Information is used for 2 purposes
		1. operationally for record keeping
			 1. Operations (OLTP) usually deals with 1 transaction at a time 
		2. analytical decision making
			 1.  Analytics (OLAP) deals generally with hundreds or thousands of transactions that need to be searched and compressed into an answer
3.  Need to separate these two systems for performance and usability reasons

#### Goals of DWH and BI (business intelligence)
1.  Information is easily accessible
2. Information should be consistent
	 1. clean data
	 2. common labels and definitions across sources
3.  DWH/BI systems must adapt to inevitable change
4.  Data delivered on time (seconds, minutes, days, etc)
5.  Data is kept secure
6. Serve as an authority on decision making

#### Publishing metaphors for DW/BI managers
If you were a publishing manager, you would ensure that...
1.  understand the reader
2.  ensure the magazine appeals to the reader
3.  sustain the publication
	4.  attract advertisers
	5.  publish magazine regularly

As a DWH manager, likewise you would
1. understand business users
2. deliver high quality data
3. Sustain the DWH environment


#### Dimensional Modeling Introduction
Widely accepted because it accomplishes two goals:
1. Deliver data that's understandable to the business users (keeps things simple!)
2. Deliver fast query performance

Dim models are not to be confused with third normal form (3NF) models.

Normalized models are great for:
- OLTP processing since update/insert happens in only one place

Bad for BI queries because:
-   users can't understand or navigate the tables
-  poor query performance due to more joins


#### Star schema vs OLAP cubes
[Star schema](https://docs.microsoft.com/en-us/power-bi/guidance/star-schema) is generally implemented in relational DB.
OLAP cubes are used in multi-dimensional DB's.

It is recommended that atomic information is loaded into star schema, and optionally, from there OLAP cubes are populated.

Kimball then goes to give around 10 different OLAP cube considerations, I will not cover these here.

#### Fact Tables for Measurements
- The fact table stores the performance measurements. Each row in a fact table corresponds to a measurement event.
- The data on each row is at a specific level of detail- known as the grain.
   - One core tenet of dimension modeling is that all measurement rows in a fact table must be at the same grain

- The most useful facts are numeric and additive
   - i.e dollars or sales amount
- Note that while addivity is the most common and preferred since you can sum up millions of rows at a time, sometimes facts are semi-additive or even non-additive
   - semi additive example: account balances
   - non-additive example: unit prices
- Fact tables usually make up 90% or more of total space from a dimension model.
- There are 3 categories of facts:
   1. transactions (Ch3: Retail Sales)
	 2. periodic snapshot (Ch4: Inventory)
	 3. accumulating snapshot (Ch4: Inventory)

Keys:
- All fact tables have 2 or more foreign keys (FK) that connect to dim tables primary keys.
- The fact table's primary key (PK) is generally composed of a subset/combination of its FK, this is called a `composite key`.

#### Dimension Tables for Descriptive Context
- Dim tables are the 'who, what, where, when , how and why' associated with an event.
- They tend to have many columns, but fewer rows- the inverse of a fact table.
- defined by a single primary key (PK)
- When naming dim fields, be clear and avoid abbreviations
- It is possible that a numeric field is a dim
	- if the value is constantly changing, it's probably a fact
	- if it's a discrete value drawn from a small list, it's probably a dim field
- Dim tables often represent hierarchal relationships
	- the example given is products -> brands -> categories
	- information is stored redundantly (denormalized) for ease of use and query performance
	- dim tables are generally highly denormalized, no need to normalize since the space benefits from normalization wouldn't matter considering it's fact tables that take up most space
- Dim table benefits
	- simplicity- easy to understand and navigate
	- performance benefit
		- “DB engine can make strong assumptions about first constraining the heavily indexed dimension tables, and then attacking the fact table all at once with the Cartesian product of the dimension table keys satisfying the user's constraints. ”
	- easily accommodates change (i.e new dimensions)
- Kimball gives a star schema example, and the ensuing SQL code to demonstrate how this structure is simple to read/follow

#### Kimball's DW/BI Architecture
There are 4 separate and distinct components in the DW/BI environment
1. operational source system
2. ETL system
3. data presentation area
4. business intelligence apps

![Architecture](images/Figure1.7-Core_DW_Architecture)

#### Operational Source Systems
- Think of these as outside the DWH
- main priority here is performance/availability
- Not expected to be queried upon

#### Extract, Transform, and Load
- Extracting means reading the source data and copying it the data over to the DWH
- Transformations- numerous options such as
	- cleaning the data
	- combining data from different sources
	- deduplicating data
- Loading the data into the presentation area is the final step
- Caveat: There is still debate on whether the data in the ETL system should  be repurposed into normalized structures prior to loading into presentation area.
	- Many times it is pointless to create a 3NF just to denormalize it for DWH usage in the BI presentation area
	- If normalized structures are used, these must be off limits to end users because it is 
		- less understandable
		- queries are less performant (need more joins)

#### Presentation Area to Support BI
- The presentation area is where data is organized, stored, and made available to end users and other BI apps
- Author has several strong opinions on this stage
	1. All data must be presented as a dim schema
	2. It must contain detailed, atomic data
		- the user may need data at the most granular level
		- if you provide granular data, the user can always roll the data up
	3. This data area should be structured around business process measurement events.
		- For example, you should construct a single fact table for atomic sales metrics, rather than slightly different tables for sales for each dept
	4. Dim structures must be built using common, conformed dims. This is the basis for DWH bus architecture

#### BI intelligence applications
- The term BI refers to the range of capabilities provided to end users. The data is served by the DW presentation area.
- Can be an ad-hoc query tool, or a data mining app

#### Restaurant metaphor

##### ETL = back room kitchen
The ETL system resembles the kitchen because
1. source data is magically transformed, just like raw ingredients are transformed into food.
2. The ETL system, like a kitchen, needs to be planned out long before data/food is extracted and designed to ensure max efficiency
3. ETL system, like a kitchen is concerned about data/food quality, integrity, consistency
4. ETL systems, like the kitchen, are off limits to the restaurant patron/business user

##### Data presentation and BI in the front dining room
- What are the key factors that a restaurant is rated on?
	1. food
	2. decor
	3. service
	4. cost

Similarly a DWH is rated on its data, is it consistent and high quality?
The presentation area should be organized in a way that is appealing to the end user.

#### Alternaties DW/BI architectures




