# Data Analytics Portfolio

A collection of end-to-end analytics projects. Each one starts with a messy real-world dataset and ends with a working Power BI dashboard, documented well enough that someone else could pick up where I left off.

## How each project gets built

Every project in this repo follows the same pipeline, mostly because I got tired of reinventing my workflow every time I started something new:

1. **Python** – clean the raw data, handle missing values, run EDA to figure out what questions the data can actually answer
2. **Figma** – wireframe the dashboard before touching Power BI, so I'm not rearranging visuals after the fact
3. **Power BI** – build the real dashboard: DAX measures, calculated columns, the whole thing
4. **README** – write up what the project does, what decisions I made and why, so it's not just a folder of files with no context

I treat the business questions as the starting point, not an afterthought. Each project defines its questions early, and that list drives the cleaning decisions, the DAX, and which visuals actually make the cut.

## Projects

| # | Project | Dataset | Status |
|---|---------|---------|--------|
| telco-churn-analysis | Telco Customer Churn | Telco customer records | Complete |
| Hotel_Bookings | Hotel Bookings | Hotel booking records | Complete |
| online_retail_Store | Online Retail II | Online retail transactions | Complete |
| Loan | Loan Applications | 614 loan application records | Complete |
| HR-Employee-Attrition | HR Employee Attrition | HR employee data | Complete |

Each project folder has its own README with the specifics: the business questions it answers, the cleaning decisions, and any quirks I ran into building the dashboard.

## A few things I've learned doing this repeatedly

- Derived columns and flags belong in Power BI as DAX, not in the Python cleaning script. Keeping them out of Python means the raw-to-clean step stays simple and the analysis logic lives in one place.
- Wireframing in Figma before opening Power BI saves a surprising amount of rework. It's tempting to skip straight to the dashboard, but sketching it out first means fewer "wait, where does this KPI even go" moments.
- Sort-order circular dependencies in Power BI usually mean the sort key is referencing the wrong column. Point it at the same upstream source as the column being sorted, not the column itself, and the loop goes away.
- Business questions first, visuals second. Deciding what I want to be able to answer before I open Power BI keeps the dashboard from turning into a pile of charts nobody asked for.

## Tools

Python (pandas), Power BI (DAX, Power Query), Figma, Git.

More projects will get added here as I finish them. If you're looking at one in particular, check its own README for the full breakdown.
