# E-Commerce User Behavior Analysis: Engagement, Cart Abandonment & User Personas

An end-to-end analytics project using PowerQuery and PowerBI to analyze 27M+ shopping events from a multi-category online store (October 2019).

## Table of Contents
- Business Problem
- Key Findings
- Dataset
- Tools & Technologies
- Methodology
  - Data Cleaning
  - Data Modeling
  - DAX Measures
  - Dashboards
- User Personas
- Recommendations
- Limitations
  

## Business Problem
The store attracts a very large audience, but mist visitors never buy. This project aims to answer to questions:
1. **Who are the store's users?** What do their engagement patterns, session frequency, spending, and cart abandonment look like, and *what distinct personas emerge*?
2. **How can the store grow?** Which actions would improve engagement, cart conversion, and sales?


## Key Findings

| Metric | Value |
| --- | ---: |
| Total views | 27, 542, 941 |
| Total cart additions | 820, 790 |
| Total purchases | 569, 424 |
| Cart abandonment rate | 30.62% |
| Unique users | 2, 408, 159 |
| Avg. sessions per user | < 3 |
| Avg. session duration | 6.77 min |
| Avg. events per session | 4 |
| Users with no spending | 88.93% |
| Share of purchases in Electronics | 74.29% |


### Highlights
- Customer retention is a core issue. While the store attracts many visitors, it is poor at keeping them as most users have very few sessions and the large majority never made purchases.
- Electronics drives the business. Samsung and Apple each generated over 4M engagements, and electronics account for roughly three quarters of total purchases.
- Timing patterns in activity emerged. Cart additions and purchases peak from Tuesday through Friday, while overall engagement is highest between 2 and 5 PM (UTC), gradually declining through 11 PM.
- Low-activity users abandon carts the most. Users with fewer than 5 sessions have the highest per-user cart abandonment rate (47.99%), and 81.77% of them never purchase.
- Heavy browsers rarely buy. Most high-activity users (>15 sessions) make no purchases.


## Dataset
The data used for this analysis was obtained from a Kaggle dataset posted by Michael Kechinov. The file contains behavior data of a large multi-category online store’s users for October 2019. Each row represents an event classified as view, cart, and purchase.  

Source: [eCommerce behavior data from multi-category store](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store) 

| Column | Description |
| --- | --- |
| `event_time` | Time of the event (in UTC) |
| `event_type` | view, cart, or purchase |
| `product_id` | Unique product ID |
| `category_id` | Unique category ID |
| `category_code` | Category code name, can be null |
| `brand` | Lowercased brand name, can be null |
| `price` | Product price (float) |
| `user_id` | Permanent unique user ID |
| `user_session` | Temporary session ID (changes when user comes back after a long pause) |

> **How to Read:** User `user_id` during session `user_session` added to shopping cart (property `event_type` is equal `cart`) product `product_id` of brand `brand` of category `category_code` (`category_code`) with price `price` at `event_time`.

## Tools & Technologies
- Power Query: data cleaning and transformation
- PowerBI: data modeling, DAX, and dashboards
- DAX: calculated columns and measures


## Methodology
### 1. Data Cleaning 
- Split `event_time` into separate date and time columns and set the correct data types.
- Split `category_code` into three levels and kept the top level for simplicity (e.g. appliances.kitchen.microwave and appliances.environment.water_heater both become appliances).
- Removed the original `category_id` and generated new unique IDs for the simplified categories.
