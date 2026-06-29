# Telecom Customer Churn Analysis (Databel Case Study)

An interactive Power BI data analysis project focused on diagnosing and understanding customer attrition (churn) for the fictitious telecom provider, **Databel**. This project transforms raw customer snapshot data into actionable business intelligence by identifying high-risk segments, behavioral patterns, and the root causes behind customer departures.

---

## Executive Summary & Key Insights

Databel's overall baseline **churn rate sits at 26.86%**. By diving deep into demographic patterns, contract mechanics, and geographical distributions, this analysis uncovered the primary drivers of this attrition:

*   **The Competitor Threat:** The absolute #1 driver of customer loss was external market pressure. **45.51% of all churned customers** left because a **"Competitor made a better offer"** or provided superior hardware devices.
*   **Contract Vulnerability (The Monthly Risk Multiplier):** Customers on a **Month-to-Month contract type are 51.01% more likely to churn** compared to those locked into stable 1 or 2-year agreements. In fact, selecting a Month-to-Month filter reveals it accounts for roughly 1,600 out of 1,800 total churners.
*   **Geographic Hotspot:** Regional competition is highly uneven. **California (CA) exhibits a critically high churn rate of 63.24%**, indicating aggressive local competitor promotions or localized infrastructure dissatisfaction.
*   **The "Early Stage" Vulnerability:** Attrition drops significantly over time. Customers in the **earliest stages of their lifecycle** (under 12 months with the provider) exhibit a dramatically higher probability of leaving.
*   **Demographic Skew:** The **older demographic / Senior Citizen** cohort charts a churn rate significantly higher than the baseline average (~10% higher than younger segments), spiking all the way to 52% for customers aged 80+.

---

## Technical Implementation Details

To solve the "leaky bucket" problem for Databel, the raw transactional data was structured and refined within Power BI Desktop using the following methodologies:

### Data Preparation & Transformation
*   **Data Consistency Check:** Engineered unique verification measures (`COUNT` vs. `DISTINCTCOUNT` on `Customer ID`) to validate that the dataset container held exactly 1 row per unique user with zero structural duplicates.
*   **Binomial Normalization:** Converted the text-based `Churn Label` ("Yes"/"No") into a clean, binary indicator (`1` / `0`) using conditional logical syntax to smoothly feed downstream calculation engines.

### DAX Measures Crafted
*   `Total Customers = COUNT('Databel - Data'[Customer ID])`
*   `Number of Churners = SUM('Databel - Data'[Churned])`
*   `Churn Rate % = DIVIDE([Number of Churners], [Total Customers], 0)`
*   **Demographic Segmentation:** Implemented nesting `IF()` functions and `SWITCH()` logic to dynamically classify age cohorts into clean bins ("Under 30", "Senior", "Other") for granular pattern analysis.

### Dashboard Interactivity & Visuals
*   **Interactive Root-Cause Tree:** Built column and bar charts clustering precise churn reasons into high-level categories (Price, Product, Competitor, Support).
*   **Geographic Map Overlays:** Rendered multi-state geographical layers to visually isolate the California anomaly.
*   **Cross-Filtering Capabilities:** Enabled seamless stakeholder drill-downs—clicking a contract type slice instantly updates all contextual demographic profiles and risk factors.

---

## Repository Structure

*   `churn analysis project.pbix` - The complete, interactive Power BI workbook containing the data model, DAX measures, and report pages.
*   `databel- data.csv` - The original raw telecom customer profile snapshot dataset (29 operational columns).

---

## Strategic Recommendations for Databel

1.  **Introduce Long-Term Incentives for "Early Stage" Accounts:** Because attrition peaks in the first year, onboarding programs should offer milestone discounts or data bonuses to pull customers past the high-risk early retention phase.
2.  **Targeted Month-to-Month Conversion Campaigns:** Proactively target monthly accounts with a financial incentive (e.g., a discounted rate) to convert them to fixed 1 or 2-year contracts, effectively cutting their churn threat down to under 3%.
3.  **Deploy Defensive Promos in California:** Run an aggressive counter-marketing or custom pricing plan targeting CA users to blunt competitor poaching strategies.
