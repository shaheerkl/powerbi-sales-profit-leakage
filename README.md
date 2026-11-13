# powerbi-sales-profit-leakage


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
