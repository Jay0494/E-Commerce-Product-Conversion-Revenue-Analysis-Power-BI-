# E-Commerce Product Conversion & Revenue Analysis (Power BI)
[Click To View Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMmI0NzY1MDAtN2NhZC00YWE3LTgyNDQtNzgzZmJkZDgyY2E0IiwidCI6ImIyMTFiMjkwLWFkNzUtNGJlNC1iZDk3LWI5Y2MxZDlmMzdlZCJ9)

## Project Overview

Understanding how customers move from **product discovery to purchase** is critical for improving conversion and revenue in e-commerce businesses.

This project analyzes **customer interaction data** to understand behavioral patterns, conversion performance, and revenue drivers across an e-commerce platform.

Using **Power BI**, I built an interactive dashboard that evaluates:

* Customer conversion funnel
* Browsing behavior patterns
* Device performance
* Marketing channel effectiveness
* Revenue contribution by product category

**Analysis Period:** January 1 – March 14, 2026

---

# Business Problem

E-commerce companies generate large volumes of user interaction data, but without structured analysis it is difficult to understand:

* When customers are most active
* Which devices convert best
* Which marketing channels bring high-intent users
* Where users drop off in the purchase journey
* Which products generate the most revenue

The goal of this project was to transform **raw event data into actionable insights** that help improve conversion performance and marketing efficiency.

---

# Tools Used

* Power BI
* Power Query
* DAX
* Data Modeling
* Data Visualization

---

# Dataset Description

The dataset contains **event-level user interaction data** representing customer actions during website sessions.

Each row represents a **customer interaction event**.

### Key Fields

| Column              | Description                 |
| ------------------- | --------------------------- |
| user_id             | Unique user identifier      |
| session_id          | Session identifier          |
| event_type          | User action in the funnel   |
| event_time          | Timestamp of event          |
| device              | Device used by the customer |
| acquisition_channel | Marketing traffic source    |
| product_id          | Product identifier          |
| product_category    | Product category            |
| list_price          | Original product price      |
| discount_pct        | Discount percentage         |
| final_price         | Final purchase price        |
| payment_method      | Payment method used         |

---

# Data Cleaning & Preparation

Raw event data required several preprocessing steps before analysis.

## Initial Data Quality Assessment

The raw dataset was evaluated using **Power Query column profiling**.

Issues identified:

* Missing product values
* Inconsistent data types
* Null pricing values
* Event data stored across multiple tables

---

## Data Transformation Steps

Using **Power Query**, the following transformations were applied:

### 1. Data Type Standardization

Converted columns to appropriate types:

* event_time → DateTime
* list_price → Decimal
* discount_pct → Decimal
* final_price → Decimal

---

### 2. Event Timestamp Processing

Split timestamps into separate analytical fields:

* Date
* Hour of Day
* Time of Day category

This enabled analysis of **customer browsing patterns across the day**.

---

### 3. Handling Missing Product Data

Product attributes such as pricing and category were cleaned and standardized.

Example cleaned product data:

---

### 4. Session Integrity Check

Session IDs were validated to ensure no missing or duplicate session identifiers.

---

# Data Modeling

A **star schema data model** was implemented to improve query performance and analytical flexibility.

### Fact Table

**fact_engagement_table**

Contains transactional and event-level interaction data.

Key fields:

* event_id
* user_id
* device_id
* channel_id
* product_id
* event_date
* event_time
* final_price

---

### Dimension Tables

* dim_user_table
* dim_device_table
* dim_channel_table
* dim_product_table
* dim_event_table
* dim_payment_method
* date_table

This structure enables efficient filtering across multiple dimensions.

---

# Feature Engineering

Additional fields were created to analyze behavioral patterns.

### Hour of Day

Used to evaluate browsing activity during the day.

```DAX
Hour = HOUR(event_time)
```

---

### Time of Day Segmentation

Customers were grouped into time periods:

* Morning
* Afternoon
* Evening
* Night

This allowed identification of **peak browsing periods**.

---

### Weekday vs Weekend Classification

Customers were categorized based on order timing:

* Weekday
* Weekend

This enabled analysis of **weekly purchasing patterns**.

---

# Key Metrics (DAX)

### Visit → Purchase Conversion Rate

```DAX
Visit → Purchase Conversion =
DIVIDE([Purchases],[Visitors],0)
```

---

### Revenue

```DAX
Revenue =
CALCULATE(
SUM(fact_engagement_table[final_price]),
fact_engagement_table[event_type] = "purchase"
)
```

---

### Average Order Value

```DAX
AOV =
DIVIDE([Revenue],[Orders],0)
```

---

# Dashboard Design
The dashboard was designed to highlight key performance indicators across **conversion, engagement, and revenue**.

[Click To View Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMmI0NzY1MDAtN2NhZC00YWE3LTgyNDQtNzgzZmJkZDgyY2E0IiwidCI6ImIyMTFiMjkwLWFkNzUtNGJlNC1iZDk3LWI5Y2MxZDlmMzdlZCJ9)

---

# Dashboard Components

### KPI Summary

* Conversion Rate
* Cart Abandonment Rate
* Revenue Performance
* Total Orders

---

### Conversion Funnel

Visualizes the customer journey:

Visit → Product View → Add to Cart → Checkout → Purchase

This highlights where customers **drop off in the purchasing journey**.

---

### Conversion by Device

Compares conversion performance across:

* Desktop
* Tablet
* Mobile

---

### Conversion by Marketing Channel

Analyzes traffic sources including:

* Organic
* Social
* Referral
* Direct
* Paid Search
* Email

---

### Revenue by Product Category

Identifies which product categories generate the most revenue.

---

### Customer Activity by Time of Day

Examines when customers browse products during the day.

---

### Order Distribution

Compares **weekday vs weekend purchasing behavior**.

---

# Key Insights

Analysis of customer behavior revealed several important insights.

### Conversion Performance

The **Visit → Purchase Conversion Rate is 24.1%**, indicating strong purchase intent among visitors.

---

### Customer Engagement Patterns

Product browsing peaks during **evening hours**, suggesting customers engage with products after work.

Peak browsing times occurred at:

* 15:00 (4.6%)
* 22:00 (4.9%)

---

### Weekly Purchasing Behavior

**Weekday orders exceed weekend orders**, indicating higher purchasing activity during the workweek.

---

### Device Performance

**Desktop users have the highest conversion rate**, while **mobile users have the lowest**, suggesting potential friction in the mobile shopping experience.

---

### Marketing Channel Performance

**Organic traffic generates the highest conversion rate**, indicating strong purchase intent from search users.

**Email traffic shows the lowest conversion rate**, suggesting an opportunity to improve campaign targeting.

---

### Revenue Drivers

**Electronics generates the highest revenue**, making it the most profitable product category.

---

# Business Recommendations

Based on the analysis, several improvements are recommended.

### Improve Mobile Experience

Mobile users convert less than desktop users. Improving mobile UX and checkout flow may increase conversion rates.

---

### Align Marketing With Engagement Patterns

Schedule campaigns during **afternoon and evening browsing peaks**.

---

### Optimize Email Campaign Strategy

Improve segmentation and personalization to increase email conversion rates.

---

### Promote High-Revenue Categories

Increase marketing investment in **electronics products**.

---

# Business Impact

This analysis helps businesses:

* Understand customer purchase behavior
* Identify high-performing marketing channels
* Optimize conversion performance
* Improve product marketing strategy
* Support data-driven decision making

---

# Repository Structure

```
ecommerce-powerbi-analysis
│
├── dashboard
│   └── PowerBI_Dashboard.pbix
│
├── data
│   └── raw_dataset.csv
│
├── images
│   ├── dirty_data.png
│   ├── clean_data.png
│   ├── data_model.png
│   └── dashboard.png
│
└── README.md
```

---

# Author

Elijah Okpako
Data Analyst | Business Intelligence | Power BI

---

# Analytical Questions Answered

This analysis was designed to answer several key business questions related to **customer behavior, conversion performance, and revenue generation**.

---

## 1. What percentage of visitors convert into paying customers?

# Visit → Purchase Conversion Rate

This metric evaluates the overall effectiveness of the e-commerce funnel.

**Result**

The platform achieved a **24.1% conversion rate**, indicating strong purchase intent among visitors.

**Business Value**

Understanding conversion performance helps businesses evaluate **sales efficiency and customer acquisition effectiveness**.

---

## 2. Where do customers drop off in the purchase funnel?

**Funnel Stages Analyzed**

Visit → Product View → Add to Cart → Checkout → Purchase

The funnel analysis identifies **critical friction points in the customer journey**.

**Business Value**

Improving the weakest stage in the funnel can significantly increase revenue without increasing marketing spend.

---

## 3. When do customers browse products the most?

Customer browsing behavior was analyzed using **hourly activity data**.

**Key Finding**

Product browsing peaks during the **evening hours**, with the highest engagement recorded at:

* **15:00 (4.6%)**
* **22:00 (4.9%)**

**Business Value**

Understanding browsing patterns helps businesses optimize:

* marketing campaign timing
* promotional push notifications
* advertising schedules

---

## 4. Do customers purchase more during weekdays or weekends?

Orders were segmented into:

* Weekday orders
* Weekend orders

**Key Finding**

**Weekday purchases exceed weekend purchases**, suggesting that most transactions occur during the workweek.

**Business Value**

Businesses can allocate **marketing budget and promotional timing more effectively**.

---

## 5. Which devices generate the highest conversion rates?

Conversion performance was analyzed across devices:

* Desktop
* Tablet
* Mobile

**Key Finding**

* **Desktop users have the highest conversion rate**
* **Mobile users have the lowest conversion rate**

**Business Value**

This suggests potential **mobile user experience friction**, which may require improvements to:

* mobile navigation
* checkout flow
* payment processes

---

## 6. Which marketing channels bring the highest quality traffic?

Traffic sources were evaluated based on conversion performance.

Channels analyzed:

* Organic
* Social
* Referral
* Direct
* Paid Search
* Email

**Key Finding**

* **Organic traffic generated the highest conversion rate**
* **Email traffic generated the lowest conversion rate**

**Business Value**

This insight helps businesses:

* prioritize high-performing channels
* optimize marketing spend
* refine email campaign targeting

---

## 7. Which product categories generate the most revenue?

Revenue performance was analyzed across product categories.

**Key Finding**

**Electronics generates the highest revenue**, making it the top-performing category.

**Business Value**

Businesses can:

* prioritize high-performing products
* allocate inventory more efficiently
* target promotions more strategically
