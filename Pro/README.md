# Telco Customer Churn Analysis

I built this to figure out why telecom customers leave, and how much it's costing. It's a two-part project: a Python notebook that cleans the raw data, and a Power BI dashboard that turns it into something you can actually click through and explore.

## Project Files

| File | What it is |
|---|---|
| `WA_Fn-UseC_-Telco-Customer-Churn.csv` | The raw dataset, straight from source |
| `port1.ipynb` | Notebook that cleans the raw data |
| `Cleaned_data.csv` | Output of the cleaning step (7,043 rows, 21 columns) |
| `Port_1.pbix` | The Power BI dashboard |
| `images/` | PNG exports of each dashboard view |

## The Dataset

Standard Telco Customer Churn data. Each row is one customer:

- **Who they are**: gender, senior citizen status, partner, dependents
- **Their account**: tenure, contract type, paperless billing, payment method
- **What they've signed up for**: phone service, multiple lines, internet type, online security, backup, device protection, tech support, streaming TV and movies
- **What they pay**: monthly charges, total charges
- **Whether they left**: `Churn` (Yes/No)

1,869 of the 7,043 customers churned. That's about 26.5%, which is high for telecom.

## Cleaning the Data (`port1.ipynb`)

Nothing fancy here, just `pandas` and `numpy`:

1. Load the raw CSV
2. Fix `TotalCharges`, which comes in as text and needs to be numeric
3. Check what broke in that conversion (a handful of blank strings turn into nulls)
4. Fill those nulls with 0
5. Write out `Cleaned data.csv`

### Requirements
```bash
pip install pandas numpy jupyter
```

### Run it
```bash
jupyter notebook port1.ipynb
```

## The Dashboard (`Port_1.pbix`)

I wireframed this in Figma first, then built it in Power BI. It's technically one page, but there's a nav pane with three views you flip between, plus a "Clear all slicers" button to reset everything.

**Overview** is where I put the numbers that matter most at a glance:
- Churn Rate: 26.54%
- Avg C.L.V: 2,279.73
- Total Customers: 7,043
- Monthly Revenue at Risk: $139,130.85

Below that, a line chart tracks churn against tenure buckets, and it drops off a cliff: nearly 48% in the first year, down under 10% by year five or six. There's also a bar chart on churn by payment method (electronic check is the worst offender at 45.29%), one on churn by contract type (month-to-month is 42.71%, two-year contracts are practically loyal at 2.83%), and a column chart comparing average monthly charges between people who left and people who stayed. A payment method slicer filters the whole page.

![Overview page](images/overview.png)

**Churn by Services** breaks things down by what customers subscribed to: tech support, internet service type (fiber optic churns way more than DSL, 41.89% vs 18.96%), device protection, online security, online backup, and phone service.

![Churn by Services page](images/churn-by-services.png)

**Churn by Family** looks at household and demographic factors: partner status, senior citizens (who churn almost twice as often as everyone else, 41.68% vs 23.61%), dependents, streaming TV, streaming movies, and multiple lines.

![Churn by Family page](images/churn-by-family.png)

Most of the charts are bar or clustered bar charts. The tenure trend is the one line chart, and the monthly charges comparison is a column chart.

### Opening it
1. Grab [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows only, unfortunately)
2. Open `Port_1.pbix`
3. Click around. That's really the point of it.

## What Questions Does It Answer?

**On the Overview page:**
- What's the overall churn rate, and how much revenue does that put at risk?
- What's the average customer lifetime value?
- How does churn change as customers stick around longer?
- Which payment method and contract type see the most churn?
- Do people who churn pay more per month than people who don't?

**On Churn by Services:**
- Does tech support, device protection, or online security actually reduce churn?
- Does the type of internet service matter?
- Does having phone service change anything?

**On Churn by Family:**
- Do senior citizens churn more?
- Does having a partner or dependents make someone more likely to stay?
- Do streaming subscriptions or multiple phone lines correlate with churn?

You can also filter the whole Overview page by payment method using the slicer, so it's not just static numbers, you can dig into specific segments.

## Skills This Project Shows Off

**Python / data cleaning**: reading and inspecting CSVs with pandas, fixing bad data types, handling nulls, exporting a clean dataset.

**Analysis**: comparing churn across categorical variables, spotting which segments actually move the needle versus which don't.

**Design**: wireframed the whole layout in Figma before touching Power BI, so the dashboard had a plan instead of getting built ad hoc.

**Power BI**: DAX measures behind the KPI cards, several chart types (line, column, bar, clustered bar), interactive slicers, and general report layout and styling.

**Domain knowledge**: churn analysis and what actually drives retention in a subscription/telecom business.

### Tools
- Python (pandas, numpy)
- Jupyter Notebook
- Power BI Desktop (DAX, report design)
- Figma (wireframing)
- Git/GitHub
