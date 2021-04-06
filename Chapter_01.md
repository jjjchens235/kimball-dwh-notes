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


#### Dimensional Modeling
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
- There are 3 caregories of facts:
   1. transactions (Ch3: Retail Sales)
	 2. periodic snapshot (Ch4: Inventory)
	 3. accumulating snapshot (Ch4: Inventory)

Keys:
- All fact tables have 2 or more foreign keys (FK) that connect to dim tables primary keys.
- The fact table's primary key (PK) is generally composed of a subset/combination of its FK, this is called a `composite key`.

#### Dimension Tables for Descriptive Context
	
