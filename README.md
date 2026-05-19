# Fashion Marketing & Sale Analysis | Power BI

Author: Anh Tuan Nguyen  
Date: Jan 2026  
Tools Used: Power BI, Power Query, DAX, Data Modeling

## Table of Contents

1. [Background & Overview](#background--overview)
2. [Dataset Description & Data Structure](#dataset-description--data-structure)
3. [Design Thinking Process](#design-thinking-process)
4. [Key Insights & Visualizations](#key-insights--visualizations)
5. [Final Conclusion & Recommendations](#final-conclusion--recommendations)

---

## 1. Background & Overview

### Objective

This project builds an interactive Power BI dashboard for a fashion retail business that runs multi-channel marketing campaigns. The goal is to connect marketing spend with sales performance, evaluate campaign efficiency, and identify tactical actions to improve budget allocation.

The dashboard helps stakeholders understand:

- How much revenue is generated from overall sales and ads-driven sales
- How efficiently the marketing budget is spent
- Which campaigns perform best or worst
- Which products and categories contribute most to ads revenue
- Where the business should scale, optimise, or reduce marketing spend

### Business Users

This dashboard is designed for:

- Marketing managers tracking campaign performance
- Sales and commercial teams monitoring revenue contribution
- Business analysts evaluating marketing efficiency
- Management teams making budget allocation decisions

### Business Questions

- What is the overall sales and marketing performance?
- How much revenue is attributed to marketing campaigns?
- Which campaigns generate the highest ROAS?
- Which campaigns have high spend but weak results?
- Which products perform best within marketing campaigns?
- Which categories deserve more investment?
- Are there products with strong demand but potential budget or stock risks?

### Project Outcome

The final report provides an end-to-end view of fashion marketing and sales performance through three main dashboards:

- **Overview**: executive summary of revenue, ads revenue, spend, budget, impressions, profit, and ROAS
- **Campaign Performance**: campaign-level efficiency analysis using ROAS, CPC, CPM, CTR, CPA, and campaign ranking
- **Product Analysis**: product and category-level analysis to identify strong products, weak products, and optimisation opportunities

---

## 2. Dataset Description & Data Structure

### Data Source

The dataset contains sales orders, marketing campaign costs, SKU-level campaign allocation, and product master data.

Main source file:

```text
[DAC] Project 3 - Dataset.xlsx
```

Power BI file:

```text
Fashion.pbix
```

### Tables Used

| Table | Type | Description |
|---|---|---|
| `fact_order` | Fact table | Sales order data including price, quantity, discount, cost, customer level, and product category |
| `fact_mkt_by_sku_cost` | Fact table | Marketing campaign performance allocated by SKU, including spend, ads revenue, comments, inbox, impressions, and campaign ID |
| `fact_product_sold` | Fact table | Product sold quantity by product code and date |
| `dim_date` | Dimension table | Date, day, and week fields for time-based analysis |
| `dim_ds san pham` | Dimension table | Product master data including product code, category, brand, material, price, and cost |
| `dim_mkt_camp_cost` | Dimension/campaign table | Campaign-level cost, budget, impressions, clicks, CPC, CPM, and campaign ID |

### Data Model

The report uses a star-schema style model. Dimension tables are connected to fact tables to support filtering by date, product, campaign, and category.

Key relationships:

| From Table | To Table | Join Key | Relationship |
|---|---|---|---|
| `dim_date` | `fact_order` | Date | One-to-many |
| `dim_date` | `fact_mkt_by_sku_cost` | Date | One-to-many |
| `dim_date` | `dim_mkt_camp_cost` | Date | One-to-many |
| `dim_ds san pham` | `fact_order` | Product code | One-to-many |
| `dim_ds san pham` | `fact_mkt_by_sku_cost` | Product code | One-to-many |
| `dim_ds san pham` | `fact_product_sold` | Product code | One-to-many |
| `dim_mkt_camp_cost` | `fact_mkt_by_sku_cost` | Campaign ID | One-to-many |

### Data Preparation

Power Query was used to:

- Clean and standardise column names
- Convert date, numeric, and percentage fields to correct data types
- Create product, campaign, and date dimensions
- Build campaign IDs for relationship mapping
- Prepare week-level fields for trend analysis
- Remove or handle missing and invalid values

---

## 3. Design Thinking Process

### Empathize

Stakeholders need a dashboard that does more than report sales. They need to know how marketing budget is performing and what tactical actions should be taken.

Main stakeholder needs:

- Management wants a high-level view of total revenue and marketing efficiency
- Marketing teams want to identify campaigns to scale or pause
- Product teams want to know which products and categories perform well
- Analysts need drill-down capability to explain performance drivers

### Define

The main problem is that marketing spend, sales revenue, and product performance are stored in separate tables. Without a connected model, it is difficult to understand which campaigns and products actually drive revenue.

Defined analytical goals:

- Connect sales data with marketing spend
- Measure efficiency using ROAS, CPC, CPM, CTR, CPA, and cost per result
- Compare performance by week, campaign, product, and category
- Provide actionable recommendations for budget optimisation

### Ideate

The dashboard was designed around three analytical layers:

1. **Executive layer**: overall sales and marketing performance
2. **Campaign layer**: campaign efficiency and budget effectiveness
3. **Product layer**: SKU/category performance and product-level marketing return

### Prototype & Review

The report was built in Power BI with:

- Dark-themed visual design
- KPI cards with weekly comparison
- Dynamic slicers for week/day, campaign, and category
- Switch buttons for metric views
- Scatter plot for campaign performance
- Matrix with conditional formatting for product analysis
- Drillthrough support for deeper campaign review

---

## 4. Key Insights & Visualizations

### Dashboard Preview

The Power BI report contains three main pages:

1. Overview
2. Campaign Performance
3. Product Analysis

### I. Overview

The Overview dashboard provides a business-level summary of revenue and marketing efficiency.

Main KPIs:

- Total Revenue: `$4.77bn`
- Ads Revenue: `$3.02bn`
- Total Spend: `$394.13M`
- Total Impression: `5.11M`
- ROAS: `7.67`

Key findings:

1. **Ads revenue contributes strongly to total revenue**
   - Ads Revenue reached approximately `$3.02bn`, showing that marketing campaigns are a major revenue driver.

2. **Marketing spend is highly connected to weekly revenue movement**
   - Weekly charts show changes in total revenue, ads revenue, and spend, helping stakeholders monitor growth and budget usage.

3. **ROAS remains positive overall**
   - Overall ROAS is `7.67`, meaning each unit of marketing spend generated about `7.67` units of ads-attributed revenue.

4. **Budget utilisation varies by category**
   - Some categories use most of their assigned budget, while others still have remaining budget, creating opportunities for reallocation.

### II. Campaign Performance

The Campaign Performance dashboard evaluates marketing efficiency at the campaign level.

Main KPIs:

- ROAS: `7.67`
- Total Impression: `5.11M`
- CPC: `$9.5K`
- CPM: `$77.1K`
- CTR: `0.82%`

Key findings:

1. **Campaign performance is uneven**
   - The scatter plot shows that campaigns differ significantly in spend and ads revenue. Some campaigns generate strong revenue at efficient cost, while others require review.

2. **Top campaigns should be considered for scaling**
   - Campaigns with high ads revenue and strong ROAS are candidates for additional budget.

3. **High CPC or CPA campaigns need optimisation**
   - Campaigns with high cost but weak conversion should be reviewed for audience targeting, creative quality, or product fit.

4. **Drillthrough supports deeper analysis**
   - Users can right-click a campaign to drill through and investigate product-level performance behind the campaign.

Suggested dashboard subtitle:

```text
Right-click a campaign to drill through for more details.
```

### III. Product Analysis

The Product Analysis dashboard identifies which products and categories perform best in terms of marketing investment.

Main visuals:

- Ads Revenue and ROAS by Category
- CPC / CPM / CPA / CTR by Category
- Product performance matrix
- Conditional formatting for revenue, ROAS, impressions, CPC, CPM, CTR, and cost per result

Key findings:

1. **Several products drive large ads revenue**
   - Products such as Audrey Shirt and Lisa Dress appear among the strongest contributors to ads revenue.

2. **High revenue does not always mean best efficiency**
   - Some products generate high ads revenue but may have weaker ROAS or higher cost metrics.

3. **Category-level ROAS reveals budget opportunities**
   - Categories with strong ROAS and lower spend can be considered for increased investment.

4. **Conditional formatting helps identify risks quickly**
   - Red, green, and yellow formatting highlights strong products, inefficient cost areas, and metrics requiring attention.

---

## 5. Final Conclusion & Recommendations

### Campaign Budget Optimization

Insight:

- Some campaigns generate strong ads revenue and ROAS, while others consume budget with lower efficiency.

Recommendation:

- Scale campaigns with high ROAS and controlled CPC/CPA.
- Pause or redesign campaigns with low ROAS and high cost per result.
- Use drillthrough to identify which products are driving or weakening each campaign.

### Product Portfolio Strategy

Insight:

- Product-level performance varies across ads revenue, ROAS, impressions, CPC, CPM, and CTR.

Recommendation:

- Prioritize products with strong ads revenue and high ROAS.
- Review products with high spend but weak conversion.
- Use product matrix conditional formatting to identify products needing pricing, creative, or targeting adjustments.

### Category Investment Strategy

Insight:

- Some categories show stronger ROAS and better cost efficiency than others.

Recommendation:

- Increase budget for categories with strong ROAS and scalable demand.
- Monitor categories with high spend but low efficiency.
- Compare spend, budget used, and ads revenue before reallocating budget.

### Marketing Efficiency Monitoring

Insight:

- ROAS, CPC, CPM, CTR, and CPA together provide a more complete view than revenue alone.

Recommendation:

- Track ROAS for profitability.
- Track CTR for creative and audience relevance.
- Track CPC/CPM for traffic cost.
- Track CPA and cost per comment/inbox for conversion efficiency.

---





