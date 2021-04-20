### Chapter 3 - Retail Sales
Most of the remaining chapters in this book are devoted to going through tangible examples of different industries- retail for this chapter.

The following concepts will be discussed:
- Four-step process for designing dimensional models
- Fact table granularity
- Transaction fact tables
- Additive, non-additive, and derived facts
- Dimension attributes, including indicators, numeric descriptors, and multiple hierarchies
- Calendar date dimensions, plus time-of-day
- Causal dimensions, such as promotion
- Degenerate dimensions, such as the transaction receipt number
- Nulls in a dimensional model
- Extensibility of dimension models
- Factless fact tables
- Surrogate, natural, and durable keys
- Snowflaked dimension attributes
- Centipede fact tables with too many dimensions


#### Step 1: Select the business process
A business process (BP) is a low-level activity such as taking orders or invoicing.
These processes have these characteristics:
- BP are frequently expressed as action verbs
- BP are supported by an operational system
- BP either generate or capture key performance metrics

Rarely will a business tell you the BP, you figure out the BP events based on the performance measurements users want to analyze.


If a business talks about business initiative rather than processes, generally, it involves decomposing the initiative to a business process.

A BP is not based on a department, if you focus on depts this will lead to duplicates.

#### Step 2: Declare the Grain
Declaring the grain means specifying what a `fact` table row represents, i.e 'how do you describe a single row in the fact table?'

Example grain declarations:
- One row per line item on a bill from a doctor
- One row per bank account each month

You should first declare the grain in business terms, rather than declaring the fact table's PK, even if they end up equating to the same thing.

The biggest mistake in dim modeling is forgetting this step!

#### Step 3: Identify the Dimensions
To figure out the dimensions, ask yourself 'How do business people describe the data resulting from the business process measurement events'?

Once you're clear about the grain, the dimensions can be easily identified as the
- who, what, where, when, why, how


#### Step 4: Identify the facts
To figure out the facts, ask yourself 'What is the process measuring?'

#### Final Point
When doing this 4 step process, don't dive directly into the source data, it's important to talk to the business people that will be using this data!

### Retail Case Study
Scenario:
- You work at the HQ of a grocery store.
- The business has 100 grocery stores, across 5 states
- Each store has different depts such as grocery, frozen foods
- Each store has 60k products, identified by their SKU

The data systems:
- Cashier register (POS)
- When vendors make deliveries

#### Step 1: Select the business process
The business process to model is the POS retail sales transactions.
Note that choosing which process to model first should be based on:
- criticalness
- feasibility


#### Step 2: Declare the grain
Generally you want to identify the lowest atomic grain for the following reasons:
- The more detailed and atomic, the easier it is to translate into dimensions
- provides max analytical flexibility because it can be constrained or rolled up in all possible ways

In this scenario, the data should be at the level of a specific POS transaction. They won't necessarily need this data, but their requests may be to understand how shoppers took advantage of a .50 cents off promotion, and they need maximum flexibility for this.

#### Step 3: Identify the dimensions
Once we know that we are interested in the POS transaction,  it is easy to come up with the grain:
- date
- product
- store
- promotion
- cashier
- method of payment
- POS transaction ticket number (as a degenerate dimension for transaction numbers)

After coming up with a grain statement, and the ensuing primary dimensions, if you want to add more dimensions, you can, however, they need to meet the following criteria:
- The additional dims should not cause duplicate rows in the fact table

#### Step 4: Identify the facts
Use the grain statement as a way to frame this decision, we know the grain is based on the individual product line item on the POS transaction.

The facts include:
- sales quantity
- per unit regular/discount/ net paid prices
- extended discount
- sales dollar amounts
![Fact Table](images/Figure_3.3-fact_table_design.png)

### Derived Facts



