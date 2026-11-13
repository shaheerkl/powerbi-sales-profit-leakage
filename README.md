# powerbi-sales-profit-leakage



## Data Model & Relationships

The project uses a hybrid data model consisting of sales and target fact tables, dimension tables, and an intermediate cleaned orders table.

### Main Tables

| Table | Purpose |
|---|---|
| Fact_Sales | Stores sales transactions, sales, profit, discount and related metrics. |
| Fact_Targets | Stores illustrative monthly sales targets by region. |
| Dim_Date | Provides date-based analysis. |
| Dim_Month | Supports monthly target comparisons. |
| Dim_Region | Supports regional analysis and RLS. |
| Dim_Product | Provides product-level attributes. |
| Dim_Customer | Provides customer-level attributes. |
| Dim_Geography | Provides geographical attributes such as state and city. |
| Clean_Orders | Intermediate cleaned orders table connecting customer, product and geography information with sales records. |

### Model Design

The model uses `Clean_Orders` as an intermediate table for customer, product and geography filtering. `Dim_Region` connects directly to both fact tables.

The model also includes inactive direct relationships between `Fact_Sales` and selected dimensions.

This is a hybrid model rather than a conventional pure star schema.

### Relationship Configuration

Relationships use one-to-many, many-to-one and one-to-one cardinalities, depending on the tables involved. Single-direction filtering is used in most relationships, with a bidirectional relationship between `Clean_Orders` and `Fact_Sales`.



## Row-Level Security (RLS)

Implemented Row-Level Security (RLS) in Power BI to restrict data access based on regional responsibilities.

### Security Roles

Created four region-based security roles:

| Role | Accessible Region |
|---|---|
| Region_West | West |
| Region_East | East |
| Region_Central | Central |
| Region_South | South |

### Implementation

Applied region-specific DAX filters to the following tables:

- `Dim_Region`
- `Clean_Orders`
- `Dim_Geography`

Each role uses matching regional filters to ensure that users can access only the data assigned to their respective region.

### Testing and Validation

- Tested all four roles using Power BI Desktop's **View as** functionality.
- Verified regional sales filtering.
- Verified that geography state-level data is restricted to the assigned region.
- Confirmed that all four roles returned the expected results.

### Deployment Note

The roles must also be configured with appropriate users in Power BI Service after publishing. Desktop testing alone does not confirm published user access.


### RLS Validation Evidence

**West Role**

![West RLS Validation](images/rls-west.png)

**East Role**

![East RLS Validation](images/rls-east.png)

**Central Role**

![Central RLS Validation](images/rls-central.png)

**South Role**

![South RLS Validation](images/rls-south.png)
