# E-commerce Dataset Insights & KPI Planning

## 1. Postal Codes:
   - The `postal_code` column contains many missing values and needs cleaning or imputation based on region/state/city if possible.

## 2. Product Table Normalization:
   - If `product_id` is available, the `product_name` column can be separated into a new **Product Table** to avoid long string repetition in the main **Orders Table**.

## 3. Category/Sub-Category Separation:
   - Consider creating separate **Category** and **Sub-Category** tables. Even though the names are small, separating them allows for better filtering, hierarchical analysis, and data integrity.

## 4. Sales vs. Profit Insights:
   - If the `Sales` column indicates the amount paid by the customer:
     - Create KPIs to compare **Profit vs. Quantity Sold**.
     - If **Profit is negative but quantity is high**, it may point to high **Shipping Costs**.
       - **Action:** Consider exploring better shipping partners in that region/country/state/city.
     - If **Quantity is not high**, analyze whether **Discounts** are eating into profits.
       - Compare similar past orders of the same product with different discounts or shipping costs.

## 5. Returns Analysis:
   - KPIs to monitor:
     - **Return Rate per Market** (region-wise, country-wise, etc.)
     - **Successful Orders** rate (non-returned vs. returned).
     - Identify regions with high return rates to investigate further.

## 6. Category-wise Return Analysis:
   - Identify which **Product Categories** and **Sub-Categories** have the most returns.
   - Deep-dive by year to track dissatisfaction trends over time.

## 7. Market Profitability:
   - Analyze which **Markets (Regions)** have:
     - High **Revenue** but **Low Profit**.
     - **Insight:** These markets might have strong potential but require optimization in pricing, shipping, or discount strategies.

## 8. Customer Segmentation:
   - Identify what type of customers are buying (e.g., Corporate, Consumer, Home Office).
   - Segment purchasing behavior and frequency.

## 9. Underperforming Countries:
   - In each market, identify **Countries with Low Order Rates**.
     - **Action:** Target these regions with marketing campaigns to increase reach and orders.

## 10. Yearly KPIs:
   - **Total Revenue per Year**
   - **Number of Orders per Year**
   - **Return Rate per Year**
   - **Profit or Loss per Market Annually**

## 11. Top-Selling Product Categories:
   - Identify the **Highest Selling Categories** and **Sub-Categories**.
   - Analyze **Average-Selling Products** to see if there's potential to scale or promote them further.

## 12. People Sheet:
   - KPI to find which **manager** is responsible for high profit and revenue regions.
   - Identify regions where a manager needs to implement marketing strategies to reach more people.
   - Identify manager of the regions where the return rate is greater compared to other regions.

---

## Conclusion:
Here I conclude my exploration of the supermarket sales dataset. My exploration has given me ideas for different KPIs to work on. The next step is to finalize my KPIs.
