# Retail Transaction Analysis Using Python & Pandas

## 1. Executive Summary

This project analyses a large retail dataset containing more than **2.1 million transaction records** using Python and Pandas. The analysis focuses on understanding sales performance over time, customer purchasing behaviour across demographic groups, and differences in product purchasing patterns.

Three datasets were incorporated into the analysis which are transaction data, household demographic data, and product information.

The project demonstrates an end-to-end exploratory data analysis workflow including data preparation, datatype optimisation, datetime manipulation, aggregation, dataset merging, pivot-table analysis, and data visualisation.

---

## 2. Project Objectives

The analysis was conducted to answer several key questions:

1. How do retail sales change over time?
2. How does monthly sales performance compare across years?
3. Are there noticeable differences in sales across days of the week?
4. How does household spending vary across age groups?
5. How does spending differ across household income levels?
6. Does household composition influence average spending?
7. Which product departments generate sales among different age groups?

---

## 3. Dataset

### Transaction Data

The primary dataset contains **2,146,311 transaction-level records**.

The main variables used were:

| Variable | Description |
|---|---|
| `household_key` | Identifier for each household |
| `BASKET_ID` | Identifier for each shopping basket |
| `DAY` | Transaction day |
| `PRODUCT_ID` | Identifier for the purchased product |
| `QUANTITY` | Quantity purchased |
| `SALES_VALUE` | Transaction sales value |

### Household Demographics

Household information was incorporated using:

- `AGE_DESC`
- `INCOME_DESC`
- `HH_COMP_DESC`
- `household_key`

These variables allowed transaction behaviour to be analysed across different customer segments.

### Product Data

Product information was incorporated using:

- `PRODUCT_ID`
- `DEPARTMENT`

This enabled sales to be analysed according to product department and customer age group.

---

# 4. Data Preparation

## 4.1 Column Selection

Only columns relevant to the analysis were imported from the transaction dataset. This reduced unnecessary data processing and kept the analysis focused on the required business questions.

The transaction dataset was reduced to six primary columns:

`household_key`, `BASKET_ID`, `DAY`, `PRODUCT_ID`, `QUANTITY`, and `SALES_VALUE`.

---

## 4.2 Datatype Optimisation

Several numerical columns were converted to smaller integer datatypes where appropriate.

For example:

- `DAY` → `Int16`
- `PRODUCT_ID` → `Int32`
- `QUANTITY` → `Int32`

After optimisation, the transaction DataFrame containing more than 2.1 million records used approximately **75.7 MB of memory**.

Categorical demographic and product variables were also stored using Pandas' `category` datatype where appropriate.

This demonstrates how datatype selection can improve memory efficiency when working with large datasets.

---

## 4.3 Date Creation

The original dataset represented time using a numerical `DAY` variable.

A proper datetime variable was therefore created using Pandas datetime and timedelta functionality.

Creating a datetime field enabled the dataset to be analysed using time-series operations such as:

- monthly resampling,
- year-over-year comparisons,
- date filtering,
- day-of-week extraction.

---

# 5. Exploratory Analysis

## 5.1 Monthly Sales Trend

Transaction data was indexed by date and resampled at a monthly level.

Monthly `SALES_VALUE` was aggregated to examine how overall retail sales changed throughout the observation period.

This analysis provides a high-level view of sales movement and makes it easier to identify periods of stronger or weaker sales activity than would be possible from individual transaction records.

---

## 5.2 Focused Time-Period Analysis

The time series was subsequently filtered to focus on transactions between **April 2016 and October 2017**.

This demonstrates the use of Pandas datetime indexing to investigate specific periods within a larger transaction history.

Filtering the dataset by date allows analysts to investigate particular periods without altering the original transaction data.

---

## 5.3 Year-over-Year Monthly Sales

Monthly sales were compared between **2016 and 2017**.

A 12-month lag was created using `shift(12)`, allowing each month's sales to be compared with the corresponding month from the previous year.

This technique is useful for identifying year-over-year patterns while accounting for recurring monthly behaviour.

---

## 5.4 Sales by Day of Week

Transactions were grouped using the day-of-week component of the transaction date.

Total `SALES_VALUE` was then calculated for each day.

This analysis provides insight into how customer purchasing activity varies throughout the week and demonstrates how datetime attributes can be used for behavioural analysis.

---

# 6. Customer Demographic Analysis

The next stage examined whether household characteristics were associated with differences in purchasing behaviour.

Transaction-level sales were first aggregated by `household_key`.

The aggregated sales table was then joined with the household demographic dataset using an **inner join**, ensuring that the analysis only included households for which demographic information was available.

The resulting demographic dataset contained **668 matched household records**.

---

## 6.1 Sales by Age Group

Total household sales were grouped according to `AGE_DESC`.

This analysis was used to examine the contribution of different age segments to overall spending.

Rather than analysing individual transactions alone, aggregating spending at household level provides a clearer representation of customer-level purchasing behaviour.

---

## 6.2 Sales by Income Group

Household sales were also analysed according to `INCOME_DESC`.

This allows spending patterns to be compared across different household income ranges.

The analysis demonstrates how demographic segmentation can be combined with transaction data to identify differences in customer purchasing behaviour.

---

## 6.3 Age and Household Composition

A pivot table was created using:

- `AGE_DESC`
- `HH_COMP_DESC`
- Mean household `SALES_VALUE`

This enabled average household spending to be compared across combinations of age group and household composition.

Using average household sales rather than only total sales is particularly useful here because total sales can be influenced by the number of households belonging to each demographic category.

The pivot-table approach therefore provides another perspective on the relative purchasing behaviour of customer segments.

---

# 7. Product Demographic Analysis

The final stage incorporated product information into the analysis.

The product dataset was reduced to:

- `PRODUCT_ID`
- `DEPARTMENT`

`PRODUCT_ID` was stored using an appropriate integer datatype, while `DEPARTMENT` was converted to a categorical datatype.

---

## 7.1 Combining the Datasets

Product information was joined with the transaction and demographic data.

The resulting dataset brought together three important dimensions:

**Transaction information**

→ What was purchased and how much was spent

**Customer information**

→ Age, income and household composition

**Product information**

→ The department associated with the purchased product

This transformed the analysis from simple sales aggregation into customer and product segmentation.

---

## 7.2 Department Performance by Age Group

A pivot table was created using:

- `AGE_DESC`
- `DEPARTMENT`
- Sum of `SALES_VALUE`

This allows sales performance across product departments to be compared between customer age groups.

The analysis can help identify departments that are particularly important to specific demographic segments.

From a business perspective, this type of segmentation could support more targeted merchandising, marketing and customer engagement strategies.

---

# 8. Techniques Demonstrated

The project demonstrates practical use of several core Pandas techniques:

### Data Manipulation

- Selecting relevant columns
- Datatype conversion
- Memory optimisation
- Creating calculated columns
- Filtering data

### Aggregation

- `groupby()`
- `agg()`
- `sum()`
- `mean()`
- Pivot tables

### Time-Series Analysis

- `pd.to_datetime()`
- `pd.to_timedelta()`
- Datetime indexing
- `resample()`
- `.dt` accessor
- `shift()`

### Combining Data

- DataFrame joins and merges
- Inner joins
- Combining transaction, demographic and product datasets

### Data Visualisation

- Line charts
- Bar charts
- Time-series comparisons

---

# 9. Key Takeaways

This project demonstrates how a large transactional dataset can be transformed into a structured analysis using Python and Pandas.

Several analytical perspectives were explored:

**Time-based analysis** helped examine how sales changed across months, years and days of the week.

**Customer segmentation** connected household spending with age, income and household composition.

**Product segmentation** extended the analysis by examining product department performance across customer age groups.

Most importantly, the project demonstrates the process of moving from raw transactional records to more meaningful analytical views through aggregation, data integration and visualisation.

---

# 10. Potential Improvements

The project could be extended further by:

- Calculating year-over-year sales growth percentages
- Identifying the highest-value customer segments
- Analysing average basket value
- Measuring purchase frequency by household
- Identifying top-performing product departments
- Investigating seasonality in purchasing behaviour
- Creating an interactive dashboard using Power BI or Tableau
- Developing customer segmentation using clustering techniques

These extensions could transform the exploratory analysis into a more comprehensive business intelligence project.

---

# 11. Tools & Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Jupyter Notebook**

---

# 12. Acknowledgements

This project was completed as part of my learning through **Maven Analytics**.

The project dataset and guided exercises were provided through Maven Analytics' learning materials. The Python implementation and analysis presented in this repository were completed by me as hands-on practice in data analysis using Python and Pandas.

---

## Author

**Nur Fatin Aina**