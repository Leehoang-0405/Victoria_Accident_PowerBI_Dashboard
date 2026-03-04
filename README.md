# Victoria Accident Executive Dashboard

## Project Overview

5 years of Victorian road crash data (66,173 crashes, 1,471 fatalities, 32,419 serious injuries) transformed into a single executive dashboard for the Department of Transport and Planning. The goal: give senior decision makers a clear, consolidated view of crash trends, regional risk, and contributing factors to support evidence-based resource allocation.

<img width="979" height="959" alt="Screenshot 2026-03-04 at 3 54 14 PM" src="https://github.com/user-attachments/assets/18a1ffc6-92ad-4492-a60f-596cf1999abb" />

---

## Methodology

**Data Cleaning — Power Query**
- Nulls removed from categorical columns used for filtering and segmentation
- Unknown values below 1% of total records removed as statistically insignificant (hit-and-run status, light condition, police attendance)
- Road geometry unknowns retained at 9% — removal would have introduced geographic bias
- Redundant column dropped to prevent ambiguity in downstream measure logic
- Accident time transformed from date/time to AM/PM time format for readability and filtering

**DAX Measures — 20+ measures across 6 categories**
- **Base measures:** `COUNTROWS` and filtered `CALCULATE` expressions for total crashes, fatalities, serious injuries, alcohol-related, and police attendance
- **YoY measures:** Dynamic percentage change using `MAX`, `DATE`, `YEAR`, and `DATESBETWEEN` — formatted as directional text ("▼ 32.2% YoY") with paired context labels showing the exact comparison period
- **5-year trend measures:** `FIRSTDATE` and `LASTDATE` wrapped in `REMOVEFILTERS` to anchor year boundaries to the full dataset, preventing filter context from distorting the long-term comparison
- **Ranking measures:** `RANKX` with `ALLSELECTED` and `DENSE` tie-handling for a dynamic top 7 LGA table that responds correctly to region slicers
- **Color logic measures:** Return 1 or 0 to drive conditional formatting — logic deliberately inverted for police attendance where an increase is the positive outcome
- **Geographic measures:** `AVERAGE` latitude and longitude with a `-1` exclusion filter to plot one correctly positioned bubble per LGA on the map visual

**AI Tools — Claude (Anthropic)**
Used for dashboard mockup generation, DAX troubleshooting, and documentation writing — applied to work faster and at a higher standard.

---

## Design and Accessibility

- **Minimal layout:** KPI cards, bar chart, line chart, bubble map, and table — no decorative elements, every visual earns its place
- **Colour used sparingly:** Colour appears only where it carries meaning — white cards and grey backgrounds for everything else
- **Colour blind friendly palette:** Red-teal (`#DC3220` / `#40B0A6`) chosen over red-green, which is inaccessible to the most common form of colour blindness
- **Consistent colour logic:** `#DC3220` signals negative trends and fatal incidents across all visuals; `#40B0A6` signals positive trends; `#E66100` represents serious injuries in both the line chart and severity distribution — no colour is reused for a different meaning

---

## Results and Recommendations

- Fatalities rose 18.6% over 5 years despite a 6.2% fall in total crashes — investment should shift toward severity reduction, not just crash volume
- Geelong records the highest fatality count (48) and second highest serious injury count (1,576) among top regions — priority candidate for the next infrastructure funding cycle
- Alcohol-related crashes fell 11.4% over 5 years — the strongest sustained improvement across all metrics, indicating existing enforcement programs are working

---

## Further Steps

- Build the analyst operational dashboard (crash patterns by road geometry, time, and classification codes) and vulnerable road user dashboard (pedestrians, cyclists, young and older drivers)
- Join person and vehicle tables to unlock demographic analysis including age group, road user type, and helmet and seatbelt compliance
- Publish to Power BI Service for scheduled data refresh and role-based regional access

---

## Data Source

Victorian Road Crash Data, Department of Transport and Planning. Released under Creative Commons Attribution 4.0. Sourced from Victoria Police reports and hospital injury records, updated monthly with a 7-month lag.
