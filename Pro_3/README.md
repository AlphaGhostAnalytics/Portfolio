# Online Retail II: Sales & Customer Analysis

## Overview

I picked up the Online Retail II dataset, about 1.07 million transaction rows from a UK-based online gift retailer running December 2009 through December 2011, and set out to answer the kind of questions a stakeholder would actually ask: where's the revenue coming from, who are the best customers, what's selling and what isn't anymore.

Same pipeline I've used on the other projects: clean in Python, wireframe in Figma, build the dashboard in Power BI.

## Dataset

- **Source:** Online Retail II (UCI Machine Learning Repository)
- **Size:** ~1.07M raw rows across two sheets (`Year 2009-2010`, `Year 2010-2011`)
- **Fields:** Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country

## Data Cleaning (Python)

The raw file comes as two separate sheets, one per year, so step one was just stacking them together. After that, `clean_data.py` handles the rest:

- Dropped bad-debt adjustment invoices (Invoice prefix `A`): these are internal write-offs, not real customer orders
- Threw out rows with no description and no price, since there's nothing usable in them
- Tagged non-product rows (postage, discounts, manual entries, bank charges) with an `IsProduct` flag so they don't pollute product-level rankings
- Tagged cancellations (Invoice prefix `C`) with `IsCancelled`, keeping them as negative revenue so the totals reflect what actually landed net, not just gross sales
- Added a few calculated columns: `Revenue`, `Year`, `Month`, `YearMonth`, `DayOfWeek`
- About 23% of rows have no Customer ID. I kept those for revenue and product analysis (the sale still happened) but excluded them anywhere I was slicing by customer

## Tools Used

- **Python** (pandas): data cleaning and exploratory analysis
- **Figma**: dashboard wireframing
- **Power BI**: DAX measures, visuals, and interactive dashboard
- **GitHub**: portfolio hosting

## Business Questions & Answers

Here's what I set out to answer, and what the data actually said.

**1. What is the total revenue?**
£19.29M net. That's gross sales of about £20.96M minus roughly £1.53M that came back as cancellations or returns.

**2. How does revenue change over time?**
It climbs hard through 2010, levels off in 2011, and spikes every October–November before the holidays. Right after December, it drops off a cliff.

**3. Which products generate the most revenue?**
The Regency Cakestand 3 Tier, at around £330K. The White Hanging Heart T-Light Holder is a close second at roughly £260K.

**4. Which products sell the highest quantities?**
World War 2 Gliders Asstd Designs top the list at about 109K units, ahead of the T-Light Holder at 93K. These are cheap items though, which is exactly why they don't show up in the revenue ranking above.

**5. Which countries generate the most revenue?**
The UK, by a mile: roughly 85% of total revenue, about £16.4M. Ireland (EIRE), the Netherlands, and Germany are the next tier, but nowhere close.

**6. Who are the highest-value customers?**
Customer #18102 tops the list at £598,215. A customer based in the Netherlands isn't far behind at £523,342. Both of these look like wholesale buyers, not individual shoppers picking up gifts.

**7. What are the monthly and yearly sales trends?**
November is the peak, every year. 2010 and 2011 land in a similar range, though it's worth noting 2009 and 2011 are both partial years in this dataset (it starts in December 2009 and cuts off in December 2011), so a straight year-over-year comparison isn't quite fair.

**8. Which products have declining sales?**
I split the dataset into first-half and second-half by date and compared revenue for each product. A handful of seasonal and novelty items basically fell off a cliff, dropping to near-zero in the second half. That reads more like discontinued stock than a slow fade.

**9. What days or months generate the highest sales?**
Thursday wins for revenue. Saturday is nearly flat, but that's not weak demand. The business barely took any orders on Saturdays at all across the whole two-year window. November crushes every other month.

**10. What percentage of orders are cancelled or returned?**
About 16% of orders. At the line-item level it drops to roughly 2%, which tells you cancelled orders usually involve several items at once, not just one.

**11. What is the average order value?**
£462.99. The median is noticeably lower, which makes sense once you know a small number of large wholesale-style orders are dragging the average up.

**12. How does customer purchasing behavior differ across countries?**
UK customers buy often, in smaller amounts. Customers in Ireland and the Netherlands order far less frequently but spend a lot more each time. Again, that's a wholesale/reseller pattern, not typical retail behavior.

## Dashboard Pages

- **Overview**: headline KPIs (Total Revenue, Total Orders, Average Order Value, Cancellation Rate, Unique Customers), monthly revenue trend, and revenue by country
- **Products**: top products by revenue and quantity, declining products table, revenue by country map
- **Sales Pattern**: revenue by day of week and month, top 20 customers by revenue, cancellation rate breakdown

## Key Insights

- This is really a UK-domestic retailer with a thin international tail, not a globally balanced business
- A small handful of high-volume buyers, mostly outside the UK, punch way above their weight on revenue. Looks like wholesale/reseller activity rather than retail
- Seasonality drives almost everything here. The whole business seems built around the run-up to Christmas
- Cancellations eat about 7% of gross revenue. Noticeable, but not the story

## How to Run

1. Run `clean_data.py` on the raw `online_retail_II.xlsx` file. It outputs a cleaned CSV
2. Import that CSV into Power BI
3. Load the measures and relationships from this repo
4. Click through the three dashboard pages
