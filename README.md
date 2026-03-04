# Victoria Accident Executive Dashboard

## Executive Summary

### Business Problem

Victoria's Department of Transport and Planning oversees road safety across 7 regions, covering 66,173 crashes, 1,471 fatalities, and 32,419 serious injuries recorded over 5 years. Despite the volume of data collected through Victoria Police reports and hospital injury records, there was no single consolidated view that allowed executives to track performance trends, compare regions, and identify where road safety resources were most urgently needed.

<img width="979" height="959" alt="Screenshot 2026-03-04 at 3 54 14 PM" src="https://github.com/user-attachments/assets/18a1ffc6-92ad-4492-a60f-596cf1999abb" />

### The Failing Decision

Without visibility across all regions and severity types, road safety funding decisions risk being directed to the wrong areas. A high-crash-volume zone and a high-fatality zone tell very different stories and demand very different responses. Treating them the same way misallocates resources and leaves the most serious risks unaddressed.

### Scale of Impact

This dashboard covers 5 years of Victorian road crash data across 7 regions, capturing 66,173 total crashes with 1,471 fatalities and 32,419 serious injuries. Alcohol-related crashes account for 3.32% of all incidents, and police attended 78.97% of crashes over the period. These figures represent real lives and real costs to the state, making accurate, accessible reporting a genuine public safety priority.

### The Outcome

Executives at the Department of Transport and Planning can now track whether road safety is genuinely improving over 5 years, not just reacting to a single year of figures. The dashboard surfaces which regions carry the highest fatality burden, which speed zones generate the most crashes, and whether key interventions like alcohol enforcement are working over time. This shifts decision making from reactive to evidence-based, and from fragmented to consolidated.

---

## Business Problem

Victoria collects detailed road crash data through Victoria Police and hospital injury reporting, but this data alone does not support executive decision making. The raw dataset spans multiple tables, contains inconsistencies and unknowns, and requires significant preparation before it can be meaningfully interpreted.

The core problem is not a lack of data. It is a lack of usable data at the right level for the right audience. An executive responsible for regional road safety funding needs to see trends, comparisons, and patterns clearly and quickly. Without a purpose-built dashboard, that visibility simply did not exist, and decisions on where to direct road safety programs and resources were made without a complete picture.

---

## Results and Business Recommendations

**1. Fatalities are rising even as total crashes fall**

Fatalities increased 18.6% over 5 years while total crashes fell 6.2%, suggesting road safety resources should shift toward severity reduction programs rather than crash volume reduction. Fewer crashes does not mean safer roads if the crashes that do occur are more deadly.

**2. Urban 60 km/h zones carry the highest crash burden**

With 22,324 crashes recorded in 60 km/h zones, urban roads account for the largest share of incidents by a significant margin. Investment in urban road safety infrastructure, intersection design, and speed enforcement in these zones is likely to produce the greatest reduction in total crash numbers.

**3. Geelong is the highest priority region for intervention**

Among the top regions, Geelong recorded the highest fatality count (48) and the second highest serious injury count (1,576). Targeted regional programs and infrastructure audits in Geelong should be prioritised in the next funding cycle.

**4. Alcohol enforcement programs are working**

Alcohol-related crashes dropped 11.4% over 5 years, the strongest sustained improvement across all key metrics. This suggests existing enforcement and awareness programs are effective and should be maintained and expanded rather than defunded or deprioritised.

**5. Single-year figures can be deeply misleading**

Police attendance appeared to drop 50.3% year on year, which would normally trigger concern. Over 5 years, the decline was just 1.8%. This finding alone demonstrates the risk of making resource decisions based on one year of data and validates the need for a dashboard that presents both perspectives together.

---

## Methodology

### Data Cleaning in Power Query

The raw dataset required targeted cleaning before analysis could begin. Columns with null values were addressed, and rows with unknown values below 1% of total records were removed as they were statistically insignificant and would not affect the integrity of the analysis. Where unknown values exceeded a meaningful threshold, such as road geometry at 9%, the data was retained to avoid introducing bias into regional and location-based analysis. Columns that risked duplicating or confusing existing fields were dropped to keep the dataset clean and unambiguous. Date and time fields were transformed into consistent formats to support time-based filtering and trend analysis.

Every cleaning decision was made with the end audience in mind. An executive dashboard requires data that is reliable and consistent, and each transformation step was designed to support that standard.

### DAX Measures and Calculations

The analytical layer of this project was built entirely in DAX within Power BI. Key measure categories include:

**Year-on-Year (YoY) calculations:** Dynamic YoY percentage change measures for total crashes, fatalities, serious injuries, alcohol-related crashes, and police attendance. These compare the most recent year against the prior year and respond to region filters applied by the user.

**5-year trend comparisons:** To address the risk of single-year figures being misleading, a parallel set of measures compares the first and last calendar years in the dataset dynamically using `FIRSTDATE` and `LASTDATE` with `REMOVEFILTERS` to anchor the comparison to the full dataset regardless of user selections.

**Dynamic context labels:** Text measures that display the exact comparison period on each card, for example (2019 vs 2018) and (2014 vs 2019), so executives always know what time frame they are looking at.

**Conditional color logic:** Supporting color measures return 1 or 0 to drive green and red conditional formatting on each KPI card, with the color logic correctly inverted for metrics where an increase is a positive outcome, such as police attendance.

**Supporting measures:** LGA fatality ranking using `RANKX` with `ALLSELECTED` to produce a dynamic top 10 table that responds to region filters, and averaged latitude and longitude measures to correctly plot one bubble per LGA on the map visual.

### Use of AI

Claude (Anthropic) was used throughout this project as a practical productivity and quality tool. Specific applications included generating dashboard mockups to clarify visual requirements before building in Power BI, refining business requirements and audience definitions during the planning phase, troubleshooting and iterating on DAX formula logic, and supporting the writing of this documentation. The use of AI in this project reflects a deliberate approach to working efficiently and at a higher standard, not a shortcut around the analytical work.

---

## Demonstration of Skills and Capabilities

| Skill | Evidence in this Project |
|---|---|
| **Power BI** | Single-page executive dashboard with 5 KPI cards, interactive region filter, bubble map, trend line chart, speed zone bar chart, severity distribution chart, and top regions table |
| **DAX** | 20+ measures across YoY, 5-year trend, dynamic context labels, conditional color logic, and RANKX-based top 10 filtering |
| **Power Query** | Structured data cleaning across null handling, unknown value treatment, column removal, and date/time transformation with documented rationale for each decision |
| **Data Storytelling** | Dashboard designed specifically for an executive audience, with YoY and 5-year views presented side by side to prevent single-year misinterpretation |
| **Stakeholder Communication** | Translated complex multi-table government crash data into plain language KPIs and visuals accessible to a non-technical executive audience |
| **AI Tools (Claude)** | Applied generative AI across mockup generation, business requirement planning, DAX troubleshooting, and project documentation |

---

## Limitations

Understanding what this dashboard does not cover is as important as understanding what it does. The following limitations should be considered when interpreting the findings and recommendations.

**Data limitations**

- The dataset runs to 2019 with a 7-month reporting lag, meaning the dashboard does not reflect current road safety conditions. Any recommendations made are based on data that is now several years old and should be validated against more recent figures before informing funding decisions
- The flat Excel file is a pre-joined snapshot of the source tables. Changes to the underlying Victoria Police or hospital records do not automatically flow through to this dashboard without a manual refresh

**Analytical limitations**

- YoY comparisons are anchored to the two most recent years in the dataset (2019 vs 2018). If the dataset is refreshed with new years, the measures will shift automatically and historical YoY figures will no longer be directly comparable to what was originally reported
- The 5-year trend measure compares only the first and last calendar year in the dataset. Significant spikes or dips in middle years, for example the apparent peak in crash incidents around 2015 and 2016 visible in the trend chart, are not captured in the headline percentage figure and could be overlooked

**Dashboard scope limitations**

- The current build covers crash-level data only. There is no visibility of individual person or vehicle characteristics such as age, gender, road user type, or seatbelt and helmet compliance
- Without demographic data, vulnerable groups including young drivers, older pedestrians, and cyclists cannot be identified, tracked, or compared against the broader crash population
- The map visual uses averaged LGA-level coordinates to plot crash density. Exact hotspot locations within an LGA are not visible, limiting the usefulness of the spatial view for operational road safety teams

**Audience limitations**

- This dashboard is designed exclusively for an executive audience and is not suitable for operational analysts who need granular filtering by road geometry, time of day, DCA crash classification code, or individual road segments

---

## Further Steps

Each further step directly addresses one or more of the limitations identified above.

**1. Expand to the full dashboard suite**

*Addresses: audience limitations, dashboard scope limitations*

The planning phase of this project scoped three dashboards. Only the executive view was built here. Building the analyst operational dashboard would address the need for granular filtering by road geometry, time of day, and DCA code. Building the vulnerable road user dashboard would give advocates, public health agencies, and community safety officers the demographic breakdown that the executive view cannot provide. Together, all three dashboards would give the department a complete three-tier reporting solution covering every audience level.

**2. Integrate person and vehicle data**

*Addresses: dashboard scope limitations*

The current dashboard is built on the flat crash-level dataset. Integrating the person and vehicle CSV tables from the source data would unlock demographic analysis including age group, gender, road user type, helmet and seatbelt compliance, and vehicle type. This would significantly deepen the vulnerable road user analysis, allow the department to track which demographic groups are most at risk, and support more targeted intervention design rather than broad regional programs.

**3. Publish to Power BI Service with scheduled refresh**

*Addresses: data limitations*

The dashboard currently runs on a static file snapshot. Publishing to Power BI Service would enable scheduled data refresh aligned to the dataset's monthly update cycle, role-based access so regional managers see their own data by default, and sharing via a browser without requiring Power BI Desktop. Critically, this would also keep the YoY and 5-year measures current automatically as new years of data are added, resolving the staleness of the current 2019 endpoint.

**4. Add mid-period trend visibility**

*Addresses: analytical limitations*

The current 5-year measure compares only the first and last year. Adding a year-by-year sparkline or small multiples visual alongside each KPI card would surface spikes and dips across the full 2014 to 2019 period, giving executives a more complete picture of whether a metric has been consistently improving or fluctuating before arriving at its current value.

---

## Data Source

Victorian Road Crash Data, Department of Transport and Planning, Victoria. Released under Creative Commons Attribution 4.0 International License. Data consolidated from Victoria Police reports and hospital injury records, updated monthly with a 7-month lag.
