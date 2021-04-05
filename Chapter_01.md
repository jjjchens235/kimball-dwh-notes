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


	
