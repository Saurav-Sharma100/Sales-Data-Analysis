# Sales Data Analysis Dashboard

## Project Summary

An interactive Power BI dashboard developed to analyze sales performance across products, customers, promotions, and time. The report enables users to monitor key business metrics, compare performance across different reporting periods, identify top and bottom-performing products, and review detailed transactional records to support data-driven business decisions.

---

# Dashboard Preview

> *<img width="1330" height="748" alt="Image" src="https://github.com/user-attachments/assets/ca2ad3b9-e4f6-489e-bb99-e3bdb8698ad6" />*

---

# Project Snapshot

| Category | Details |
|----------|---------|
| **Project Type** | Business Intelligence Dashboard |
| **Tool** | Microsoft Power BI |
| **Domain** | Retail Sales Analytics |
| **Dataset** | Sales Transaction Data |
| **Data Source** | Excel Workbook |
| **Data Preparation** | Power Query |
| **Data Modelling** | Star Schema |
| **Language** | DAX |
| **Dashboard Pages** | 4 |
| **Primary KPIs** | Net Sales, Net Profit, Units Sold |

---

# Project Overview

Sales data often contains thousands of transactional records spread across multiple dimensions such as products, customers, promotions, and dates. Without a centralized reporting solution, identifying business trends, monitoring performance, and evaluating product effectiveness becomes both time-consuming and inefficient.

This Power BI solution consolidates sales information into an interactive reporting environment that enables users to analyze business performance from multiple perspectives. The dashboard combines summarized KPIs with detailed transaction-level reporting, allowing decision-makers to move seamlessly from high-level performance monitoring to detailed operational analysis.

---

# Business Problem

Business users needed a reporting solution capable of answering questions such as:

- How much revenue and profit has the business generated?
- Which products are performing the best and the worst?
- How does current performance compare with another reporting period?
- Which customers and promotions contribute to overall sales?
- How can users quickly access detailed sales transactions for further investigation?

Answering these questions manually through spreadsheets would require significant effort and would make recurring business analysis difficult.

---

# Project Objectives

- Build a centralized sales performance dashboard.
- Monitor core business KPIs using interactive visuals.
- Compare business performance across different reporting periods.
- Identify top and bottom-performing products.
- Provide transaction-level visibility for detailed analysis.
- Deliver an interactive reporting experience using Power BI.

---

# Tools & Technologies

| Tool | Purpose |
|------|----------|
| **Power BI Desktop** | Dashboard Development |
| **Power Query** | Data Cleaning and Transformation |
| **DAX** | Business Calculations |
| **Excel** | Data Source |
| **Star Schema Data Model** | Relationship Management |

---

# Dataset Overview

The report is built using sales transaction data stored in an Excel workbook.

The dataset includes information related to:

- Sales transactions
- Products
- Customers
- Promotions
- Sales dates
- Net Sales
- Profit
- Units Sold

The data model separates transactional information from descriptive dimensions, making the report easier to maintain and improving query performance.

---

# Data Preparation (Power Query)

Power Query was used to prepare the dataset before loading it into the Power BI model.

The preparation process included:

- Importing data from Excel.
- Validating data types.
- Preparing dimension tables for modelling.
- Organizing the dataset into a structure suitable for analytical reporting.

Performing these transformations before loading the data helps keep the reporting model efficient while reducing the need for additional processing during report interaction.

---

# Data Model

> *<img width="1475" height="719" alt="Image" src="https://github.com/user-attachments/assets/8f482ec3-15e0-4df7-8653-87ebc3f96c0f" />*

The report follows a star schema design where the central **Fact Table** stores transactional sales records and is connected to supporting dimension tables.

### Fact Table

- Sales Transactions
- Net Sales
- Profit
- Units Sold

### Dimension Tables

- Product Dimension
- Customer Dimension
- Promotion Dimension
- Date Table 1
- Date Table 2

A notable feature of the model is the use of two date tables. While one relationship remains active, an inactive relationship is activated within DAX measures using `USERELATIONSHIP()`. This approach provides greater flexibility when calculating metrics using a specific reporting date without changing the overall model relationships.

---

# DAX Implementation

The report uses DAX measures to calculate core business metrics while leveraging an inactive relationship between the fact table and the reporting date table. By using `USERELATIONSHIP()`, the model evaluates metrics against the desired reporting date without modifying the active relationship in the data model. Additionally, `ALL('Date Table 1')` removes filters from the primary date table to ensure calculations are based solely on the selected reporting date.

### Net Profit

```DAX
Net Profit =
CALCULATE(
    SUM('Fact Table'[Profit]),
    ALL('Date Table 1'),
    USERELATIONSHIP(
        'Date Table 2'[Date],
        'Fact Table'[Date (dd/mm/yyyy)]
    )
)
```

Calculates the total profit using the reporting date relationship, ensuring consistent profit analysis across the dashboard.

---

### Sum of Net Sales

```DAX
Sum of Net Sales =
CALCULATE(
    SUM('Fact Table'[Net Sales]),
    ALL('Date Table 1'),
    USERELATIONSHIP(
        'Date Table 2'[Date],
        'Fact Table'[Date (dd/mm/yyyy)]
    )
)
```

Returns total net sales while evaluating the data against the reporting date instead of the default active date relationship.

---

### Total Quantity

```DAX
Total Quantity =
CALCULATE(
    SUM('Fact Table'[Units Sold]),
    ALL('Date Table 1'),
    USERELATIONSHIP(
        'Date Table 2'[Date],
        'Fact Table'[Date (dd/mm/yyyy)]
    )
)
```

Calculates the total quantity of units sold using the reporting date context for accurate period-based analysis.

---

### React Dim

```DAX
React dim =
SUM('Fact Table'[Net Sales])
```

A simple aggregation of Net Sales used within report visuals where no alternate date context is required.

---

# Dashboard Walkthrough

## 1. Overview
> *<img width="1330" height="748" alt="Image" src="https://github.com/user-attachments/assets/ca2ad3b9-e4f6-489e-bb99-e3bdb8698ad6" />*


The **Overview** page serves as the primary landing page of the report, providing a consolidated view of overall sales performance. It allows decision-makers to quickly evaluate business health by monitoring key performance indicators alongside supporting visualizations.

The page combines high-level KPIs with interactive charts that summarize sales performance across products, customers, promotions, and time. Slicers enable users to filter the report dynamically, making it easy to focus on specific business segments without navigating away from the dashboard.

### Business Value

- Provides an immediate snapshot of overall business performance.
- Enables rapid identification of sales trends and profitability.
- Supports interactive filtering for deeper business exploration.
- Serves as the central navigation point for further analysis.

---

## 2. Top/Bottom 5 Analysis

> *<img width="1327" height="751" alt="Image" src="https://github.com/user-attachments/assets/81bd9617-6f15-4efb-a922-9c3b2e929bb9" />*

The **Top/Bottom 5 Analysis** page focuses on product performance by highlighting the highest and lowest performing products based on selected business metrics.

This page allows users to compare product performance side by side, making it easier to identify products driving revenue as well as products that may require further investigation. The interactive nature of the visuals enables users to explore different reporting perspectives by applying available filters.

### Business Value

- Identifies best-performing products contributing to overall sales.
- Highlights underperforming products that may require business attention.
- Supports product performance evaluation for inventory and sales planning.
- Helps management prioritize improvement opportunities.

---

## 3. Period Comparison

> *<img width="1322" height="747" alt="Image" src="https://github.com/user-attachments/assets/cecb5bbc-b70f-4289-8cf5-4db6b2febed4" />*

The **Period Comparison** page enables users to compare business performance across different reporting periods using the dedicated reporting date logic implemented in the data model.

By utilizing DAX measures that activate the inactive relationship with the reporting date table, the dashboard provides consistent comparisons without changing the model's primary relationships. This approach allows users to evaluate changes in sales, profit, and quantity across selected periods.

### Business Value

- Simplifies comparison between different reporting periods.
- Supports trend analysis using consistent business metrics.
- Helps evaluate changes in sales performance over time.
- Enables more informed business decision-making through period-based analysis.

---

## 4. Order Details

> *<img width="1315" height="740" alt="Image" src="https://github.com/user-attachments/assets/df704a37-7d97-4f2e-849e-e22e055c0e6a" />*

The **Order Details** page provides detailed transactional information that complements the summarized dashboards. Users can review individual sales records, allowing them to investigate specific transactions whenever additional detail is required.

This detailed view supports operational reporting by enabling users to validate aggregated results and perform record-level analysis directly within the report.

### Business Value

- Provides complete transaction-level visibility.
- Supports operational reporting and data validation.
- Enables users to investigate individual sales records.
- Complements the summary dashboards with detailed business data.

---

# Key Business Insights

The dashboard provides a comprehensive view of sales performance by consolidating key business metrics into a single reporting solution. Users can quickly monitor revenue, profitability, and sales volume while exploring product performance and detailed transaction records.

Some of the primary analytical capabilities offered by the dashboard include:

- Monitoring overall Net Sales, Net Profit, and Units Sold through centralized KPI reporting.
- Comparing business performance across different reporting periods using a dedicated reporting date table.
- Identifying the highest and lowest performing products through comparative analysis.
- Exploring sales data interactively using report filters and slicers.
- Investigating individual transactions through the detailed Order Details page to support operational analysis and data validation.

Rather than relying on multiple spreadsheets or manual reporting, the dashboard enables faster access to business information and supports more efficient decision-making.

---

# Business Recommendations

Based on the analytical capabilities provided by this dashboard, organizations can use the report to support several business decisions.

- Monitor sales performance regularly to identify changes in business trends.
- Review top-performing products to understand successful sales patterns and replicate them across similar products.
- Investigate consistently low-performing products to determine whether pricing, promotions, or inventory strategies require adjustment.
- Use period comparisons to evaluate the impact of business initiatives over time.
- Leverage transaction-level reporting to validate aggregated metrics and investigate unusual sales activity whenever required.

These recommendations help transform the dashboard from a reporting solution into a practical decision-support tool.

---

# Technical Highlights

This project demonstrates several important Power BI development practices that improve both report usability and model performance.

- Designed using a **star schema** with a centralized Fact Table and supporting dimension tables.
- Utilized **Power Query** for data preparation before loading data into the model.
- Implemented reusable DAX measures for Net Sales, Net Profit, and Units Sold.
- Used **USERELATIONSHIP()** to activate an inactive relationship between the reporting date table and the fact table when required.
- Applied **ALL()** within DAX measures to remove filters from the primary date table and ensure calculations were evaluated against the intended reporting date.
- Developed an interactive multi-page reporting experience combining executive summaries with detailed transactional analysis.
- Structured the report to support both high-level business monitoring and detailed operational reporting.

---

# Skills Demonstrated

This project demonstrates practical Business Intelligence and Power BI development skills, including:

### Data Preparation

- Data import from Excel
- Data transformation using Power Query
- Data type validation
- Analytical dataset preparation

### Data Modelling

- Star Schema design
- Fact and Dimension modelling
- Relationship management
- Multiple date table implementation

### DAX

- CALCULATE()
- SUM()
- ALL()
- USERELATIONSHIP()

### Dashboard Development

- KPI reporting
- Interactive filtering
- Comparative analysis
- Product performance reporting
- Transaction-level reporting
- Multi-page dashboard design

### Business Analysis

- Sales performance analysis
- Product performance evaluation
- Period comparison
- Executive reporting
- Operational reporting
- Business decision support

---

# Conclusion

This Power BI project demonstrates the complete development of an interactive sales analytics solution, from data preparation and modelling to DAX calculations and dashboard design. By combining summarized KPIs with detailed transaction reporting, the solution enables users to monitor sales performance, compare reporting periods, evaluate product performance, and explore underlying business data within a single reporting environment.

The implementation of a well-structured data model, Power Query transformations, and DAX measures using `USERELATIONSHIP()` and `ALL()` highlights an understanding of analytical modelling techniques that extend beyond basic report creation. Overall, the project showcases practical Power BI development skills while delivering meaningful business insights that support informed decision-making.
