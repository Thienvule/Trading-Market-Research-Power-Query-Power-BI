# Trading-Market-Research-Power-Query-Power-BI 
Trading | Market Research | Power Query &amp; Power BI

## Overview
### Context Overview
**Disclaimer**: This project utilizes real-world data that has been meticulously encoded and anonymized to ensure confidentiality. Sensitive information, including actual names and identifying details, has been transformed or obscured in the public file. This approach preserves the integrity of the analysis while prioritizing data privacy and security. What has been encoded/hidden will be explained carefully for the readers to understand the analysis flow as clearly as possible.
### Business Context
Dragon Eagle (encoded name - DE) is a trading company operating in the feed ingredients industry, specializing in the sale of crude (via its branch company - Phantom Eagle) and refined (branch company - Ember Dragon) oil products. By importing from global manufacturers, ED serves the Vietnamese market.

The primary objective for ED is to source the best prices, which serves as the cornerstone of its trading operations. To evaluate the company’s business activities for 2024, ED has tasked me, as the data analyst, with processing raw data acquired from market research. My goal is to generate insights that assess ED's performance in comparison to competitors and identify opportunities for improved sourcing strategies.

## Power Query - Raw File Processing
In Power Query, the data cleaning process commenced after loading and combining all 12 files. The raw data contained numerous data type and typographical errors, which I addressed using tools such as formatting (trim, clean) and value replacements for erroneous entries. However, detailing these steps would involve excessive reading, so I will skip to the query logic that creates the necessary columns for the final Power BI dashboards. 

Note: In this github repository, I would not show Power Query code as it would contain sensitive data, yet I would provide the logic to create the needed columns below. 

Let's take a brief look at the raw data given:

![image](https://github.com/user-attachments/assets/fb3983dc-e9a4-4304-ad56-7213edae68ba)

I have received 12 files corresponding to each month of 2024. Each file contains 46 columns, with the number of rows varying based on the import transactions. This dataset encompasses import market data, which includes ED as well as other companies within the feed ingredients sector. However, since ED operates solely in the crude and refined oil sector, the data will be filtered to focus specifically on these areas.

A raw file (hidden values) of a total of 12 files would look like this: 

![image](https://github.com/user-attachments/assets/3ae0aaa0-e4ab-4e2a-929c-f71fb6d298af)

### Data Dictionary

The complete Data Dictionary will be provided in the "Data Dictionary" tab of the published file for reference. For the purpose of this analysis, we will focus on these 9 key columns required for the calculations.

1. Tờ khai: Declaration form number or document reference for customs purposes.
   Reason to be used (R): The first 2 letters of the final 4 letters represent the importing harbor. 
   
   ![a](https://github.com/user-attachments/assets/b31c6231-4759-4166-a874-27adeb2a66f5)

  Note: The actual digits and letters in the declaration ID have been encoded or removed to ensure the company's data privacy.
  
   This will follow the harbor index, highlighting the company’s importing regions. This insight will help us identify areas of strong performance as well as opportunities     for improvement.
   
   ![image](https://github.com/user-attachments/assets/bff02f05-10a0-4a3a-a4c9-7556f09c94ab)

Note: This tab is provided in the published file.
  
2. Ngày đăng ký: The registration date of the customs declaration.
   This date reflects when companies submitted their import orders to customs and will serve as the primary date for the time series analysis in this project. I have also extract a Month column of this date for better sorting while processing the raw file.
   
3. Tên doanh nghiệp XNK: The name of the export-import enterprise a.k.a Buyers.
   The importers of the market, including Dragon Eagle and its branches, which will be encoded later using a column called "Importer Code"
   
4. Đơn vị đối tác: The exporter involved in the transaction a.k.a Sellers.

5. Mã hàng khai báo: Code for the goods declared in the customs document.
   DE is involved in the sale of crude and refined oil, as indicated by codes that begin with "1507." Specifically, "15071000" corresponds to crude oil, while the other "1507" codes represent refined oil products. This is crucial for ED to analyze the performance of each product type.


6. Đơn giá khai báo (USD): The declared price per unit of goods in USD for a specific quantity in a specific unit.
7. Lượng: Quantity of goods declared in a specific unit.
8. Đơn vị tính: Measurement unit for quantity (e.g., KGM, TNE, Bag).
  DE wants to analyze using the unit of tonnes (TNE). Here is the rule:
  - 1 TNE = 1000 KGM (kilograms)
  - 1 BAG (bag) = 21 TNE
Therefore, I will need a column of Unit Price by TNE and Quantity by TNE following this rule:
  - KGM -> TNE: Price * 1000 and Quantity / 1000
  - BAG -> TNE: Price / 21 and Quantity * 21
    
9. Thuế suất VAT: Value-added tax rate applied to the transaction.
This column is crucial for segmentation. ED operates in two market segments: Feed and Food. The Feed segment involves selling ingredients for livestock, while the Food segment pertains to oil intended for human consumption. A tax rate of 0 indicates a Feed transaction, whereas all other rates signify Food transactions.

### North Star Metric

The Trade Manager emphasizes that the Weighted Average Price is a key metric, as sourcing the best prices is the core value of this business.

Weighted Average Price = SUM(Total Spend) / SUM(Quantity (TNE * Unit Price (TNE)))

This metric will be calculated using a DAX when we get to the PBI part.

## Power BI - Dashboards
Note: All columns created according to the logic outlined in the "Data Dictionary" section have been developed using Power Query. However, due to the technical nature of this section, it will be presented after the Power BI results of the project.


A "Measure" table is created to store custom measures along the way

![image](https://github.com/user-attachments/assets/5652843e-54a0-4f96-82e9-7437334ff03c)

### Interactive Dashboard

![image](https://github.com/user-attachments/assets/cf9878f6-775f-4bcd-ac7b-2ca39d070ea4)


1. Market: Avg price and Quantity (TNE)
The North Star metrics are vibrantly presented here. Without any filters, the users can immediately know the market benchmark and total market size.

![image](https://github.com/user-attachments/assets/c7362fd8-806a-44b9-bbb8-2904a588874f)

Avg Price DAX:

![image](https://github.com/user-attachments/assets/bb2ed24e-4a12-4840-8a17-18f39987fb99)


![image](https://github.com/user-attachments/assets/f46ad7cb-fc55-49b0-a38e-7aee2e29076b)


2. Dragon Eagle

![image](https://github.com/user-attachments/assets/76a624cd-af99-4af0-ae2b-1de25678173d)

This card includes metrics of only Dragon Eagle, used to compare with the market benchmark and any filtered competitors.

  a. Dragon Eagle Market Size:
  
  ![image](https://github.com/user-attachments/assets/74d936c3-4678-4122-899e-1eb23abe694a)
  
  b. Dragon Eagle Quantity:
  
  ![image](https://github.com/user-attachments/assets/feeef919-709b-46cb-96f9-0cf9eb064480)

  c. Phantom Eagle Quantity: 
  
  ![image](https://github.com/user-attachments/assets/409873bb-b5f8-44be-9958-de5477feb4a5)

  d. Phantom Eagle Weighted Average Price:
  
  ![image](https://github.com/user-attachments/assets/10218b4f-9285-4f3b-874c-a44c56ac0621)

  e. Ember Dragon Quantity
  
  ![image](https://github.com/user-attachments/assets/742f4691-216f-4373-87c9-a039e46f8778)

  f. Ember Dragon Weighted Average Price:
  
  ![image](https://github.com/user-attachments/assets/9606daec-b5a3-4023-ab2a-dc23b4daef13)

3. Region and egment Contribution

![image](https://github.com/user-attachments/assets/b4406293-94ef-43f2-8501-fca59b6e4083)

4. Quantity by Month and Importer

![image](https://github.com/user-attachments/assets/c33b5fb8-b3d3-4168-b730-2a3d2f030e0f)

These two trends facilitate a comparison between Dragon Eagle's import quantities and the average quantities of its competitors. In this market, the quantity imported closely aligns with the quantity sold. Therefore, understanding this metric can aid in optimizing performance across sales, marketing, sourcing, and other areas.

This is how the top competitors (Top 10) average quantity is calculated: 

![image](https://github.com/user-attachments/assets/9e4a7d9f-94b7-49ce-a9ac-fc549d236b91)

5. Weighted Avgerage Price Trend
   
![image](https://github.com/user-attachments/assets/e923a19c-742f-4d07-a691-e00aa91bbd66)

Comparing our weighted average price with the market allows us to assess the effectiveness of our sourcing activities. If we achieve better sourcing prices but our quantities are lower than the market average, it indicates room for improvement in our optimization efforts.

6. Top Importers By Quantity

![image](https://github.com/user-attachments/assets/68327883-590a-414e-88ae-0f0d9337fbd3)

The top players (filtered to the Top 10) are identified based on their imported quantities. This bar-line chart provides insights into both the quantity imported and the Weighted Average Price of these players.

7. Top Exporters by Quantity
Understanding our vendors is crucial; we want to identify the top vendors who offer the best prices and highest sales volumes. Additionally, we aim to explore potential partnerships with other vendors for future collaboration.

Together, charts 6 and 7 provide insights into import volumes and pricing while illustrating who the buyers are. The filtering section (8) allows for a deeper analysis of this data.

![image](https://github.com/user-attachments/assets/5fc8a47b-4b67-4167-9312-6a59c09a524c)

For example, by filtering for a competitor like Firestorm Cobra, we can quickly ascertain their total imports for 2024, the specific average price, and the quantities imported from various suppliers. Of course we can compare more than 1 competitor at a time if need be.
### Trend Dashboard

This dashboard is going to be used simultaneous with the interactive dashboard to provide the coming insights.

![image](https://github.com/user-attachments/assets/7c86c869-07da-44fe-8518-e5fe407b2c85)

### Insights

As the first dashboard is an interactive dashboard, users can effortlessly explore the aspects they wish to analyze. However, I will present some of my insights and analyses to provide a helpful starting point for their exploration.

#### Insight 1: Overall Market Overview

![image](https://github.com/user-attachments/assets/3bf05063-3c26-418a-982d-7a9f2ce1d04d)

- Average Price: $1,113
- Total Quantity: ~78,000 TNE
- Regional Breakdown:
  - Southern Market: Dominates with over 70% share.
  - Northern Market: Accounts for nearly 30%.
  - Central Region: Holds a minimal share.
- Segment: Food represents approximately two-thirds of total market activity.

#### Insight 2: Dragon Eagle Overview

![image](https://github.com/user-attachments/assets/a66e6ba3-8ee9-4db5-aa2f-4816c7ab12cb)

Importer Insights
- Total Production: ~8,000 TNE (~10% market share).
- Market Position: Strong foothold in a growing market.
- Monthly Comparisons: Ranked in the top 10 for both refined and crude oil sectors (PE & ED).
  
  ![image](https://github.com/user-attachments/assets/638108f2-61a9-4bbc-a65d-9fc841b9a4f1)

- Region and Segment:
  - Dragon Eagle primarily operates in the southern region of Vietnam, with minimal efforts in the North and Central regions. The company's main segment is Feed, accounting for 61% of its business.

     ![image](https://github.com/user-attachments/assets/f7a3d6ba-a6d6-45b1-9043-eb290460d68a)
    
  - Note: Phantom Eagle serves the Feed market, while Ember Dragon focuses on the Food market.
- Quantity Trend:

  ![image](https://github.com/user-attachments/assets/1353a471-9b39-4970-a6cc-967f4913e977)

  Overall, our quantities consistently outperformed our competitors throughout the year, particularly in August and September. However, we observed significant underperformance in November, which is puzzling since the average sourced price for that month was lower than the market average.
    
  - Crude Oil:

    ![image](https://github.com/user-attachments/assets/f69048f9-926e-4e3d-aa51-53c36e10243b)


    Despite effective sourcing operations, there were notable gaps in this product category.
    
  - Refined Oil:
    
    ![image](https://github.com/user-attachments/assets/8149e461-e0f3-4375-ada7-8092c9585570)

    The average price for refined oil closely aligns with market trends, yet gaps were evident in May and November.

 => Recommendation: Investigate departments related to sales quantities, such as sales and marketing. Additionally, consult the sourcing team for further insights.
    
- Average Price Trends:

  ![image](https://github.com/user-attachments/assets/3bfaf9c5-fa71-496b-99bb-50aa4118baea)

  Overall, the sourced prices throughout the year consistently surpassed the benchmark weighted average price, indicating strong sourcing strategies and effective partnerships.
  - Crude Oil: Prices were consistently lower than market rates throughout 2024, demonstrating effective sourcing. Continued collaboration with current partners is crucial, along with exploring new exporter opportunities.
    
    ![image](https://github.com/user-attachments/assets/74717103-2ee6-40ba-b812-aac367aae794)

  - Refined Oil: Prices generally tracked the market, with slight increases in June and October. Consider purchasing early and storing when prices are favorable.
    
    ![image](https://github.com/user-attachments/assets/64978e0a-43bd-4858-916b-d42459ae9e37)


Exporter Insights

![image](https://github.com/user-attachments/assets/5351da8d-eb7e-4978-82fe-e421c70868f9)

- Current Partners: Verdant Meadow (VM) and Radiant Bliss (RB) are noted for their high production and competitive pricing.
- New Opportunities: Significant appearances from Glistening Marsh (GM) and Feathered Sky (FS), characterized by favorable prices and high production. Engaging with these partners could prove beneficial.



#### Insight 3: Crude Oil - Competitor Analysis
**Phantom Eagle (Feed Market)**
- Phantom Eagle's Market Size 2024: 13.42%.
- Monthly Production Comparison: Generally aligns with competitors, but experiences significant gaps mid-year and late-year, producing 1/3 less and 1/2 less respectively during these times despite favorable average prices. Further investigation is needed to understand these low sales periods.

##### Thunder Jabber:

![image](https://github.com/user-attachments/assets/be7c7d57-7909-4d1f-8c4a-1eefedf0a1fc)

![image](https://github.com/user-attachments/assets/d0b0ed9b-a1a6-4e9a-bcfe-c6cc8bc9cacc)

- Position: Leading the market with 14.5K TNE compared to Mekong's 4.7K TNE.
- Average Price: $1,100, higher than Mekong's $1,023 and showed a steady increase; 
- Source: exclusively sourced from Glistening Marsh.
- Quantity Trend: Sporadic imports in March and April, with stronger imports in Q3 and Q4. Mekong maintains consistent imports averaging 400 TNE.
- Segment: Food - They may import then refine the crude materials themselves as they also have exporter facility here in Vietnam
- Region: South
=> Recommendation: Consider working with GM to see if we can strike a good deal.



##### Golden Eagle & Silver Vortex:

![image](https://github.com/user-attachments/assets/441f45af-c276-47e6-9928-8ef6b715f6c1)

![image](https://github.com/user-attachments/assets/f28da800-f51c-4ee3-9b11-95b5f7463042)

- Position: Second in market share with an average of 6.7K TNE, pricing around $1,015 
- Source: sourced from Radiant Bliss.
- Average Price: Generally higher than Phantom Eagle post-mid-2024, possibly due to higher order volumes and advantageous deals.
- End-of-Year Pricing: We (PE) may be affected by Verdant Meadow's stock depletion, leading to reliance on RB’s higher pricing.
- Region: Golden Eagle (North and a bit South), Silver Vortex (South)
- Recommendation: Consider stockpiling from September-October to take advantage of TNK's peak supply and most favorable prices.



##### Emerald Archer:

![image](https://github.com/user-attachments/assets/f0edc815-eb0e-470b-97f5-5a0b0fdca5ed)

![image](https://github.com/user-attachments/assets/8aebc3e2-4561-4c51-bb9d-55b065217e4b)

- Position: Fourth in market share with 2,500 TNE at $1,013, 
- Source: sourcing from Verdant Meadow.
- Quantity Trend: Mekong generally outsells Emerald Archer, except in October-November when production dips significantly.
- Average Price: Prices with VM are significantly more favorable than Phantom Eagle, possibly due to larger order quantities.
- Region: North
- Recommendation: Explore increasing spend with VM to lock in favorable deals.


#### Other Considerations:

- Tempest Lynx: Orders placed at GO YEN with potential for self-transport (Tempest Lynx as an exporter). Also operating in the Food segment, it can import and then refine the products itself.
- Spirit Lynx: Successfully secured good pricing from TNK for limited quantities but lacks further information after the first month.
- Iron Panther: Purchases crude oil and operates in the food segment. Acquired at a very high price but in small quantities? Why?


#### **Insight 4: Refined Oil Product Insights**

**Ember Dragon Analysis (Food Market)**

![image](https://github.com/user-attachments/assets/dd83b17f-9ce7-40d2-b076-818452120776)

- Market Size 2024: 7.17%
- Monthly Production Comparison:
- Ember Dragon’s production is generally much lower than the market average, only catching up in August, September, and October.
- Average Price: Comparable to or higher than the market, with better sourcing options in November and December.
- Regional Breakdown:
   - South: Dominates with 90% market share.
   - North: Approximately 9%.
   - Central: Minimal presence.
- Segment Focus: Food.

##### Ice Coyote (IC)
![image](https://github.com/user-attachments/assets/cf0b2741-5f76-4b84-9fe2-f3cbf29d83fe)

![image](https://github.com/user-attachments/assets/420e2c8a-104c-4ef5-b75a-d491a71e09e9)

- Position: Leading the market with 11K TNE at a slightly higher price point.
- Sources: RB, VM, Glistening Falls, & Enchanted Forest.
- Quantity Trend: Ice Coyote consistently imports higher volumes (2-7 times more than ED).
- Average Price: Although initially priced less favorably than ED, IC started to create a significant gap in production from February 2024. By May 2024, they secured better pricing and maintained high production until October. Even in October, while ED had favorable pricing, IC's volume remained unmatched.
- Region: South.
- Segment Focus: Food.
- Assumption: IC has strong financial backing, allowing them to procure from more expensive sources.

=> Recommendation: Investigate why IC, despite being in the same region and sourcing from similar suppliers, is able to sell a lot more than us?



##### Tempest Griffin

![image](https://github.com/user-attachments/assets/de1cfbdd-566a-4d93-823b-dc8251b085e8)

![image](https://github.com/user-attachments/assets/b7669280-3ea0-4bdb-ae0c-475c253f8216)

- Position: Second in market share.
- Sources: Primarily from VM and RB, mainly sourcing from RB.
- Quantity Trend: Consistently high production levels.
- Average Price: Prices are consistently about $20 better than Savo, potentially due to bulk deals.
- Region: South.
- Segment Focus: Food.


##### Dusk Guardian (DG) và Golden Eagle (GE)

- Position: Ranges from 3-4K TNE priced at $1,100.
- Sources: VM, RB (GE exclusively), Rustic Bloom.
- Quantity & Average Price Trend:
   - DG began sales only in Q4 2024 but surpassed ED's total production by 1,000 TNE, likely due to large initial orders securing better prices than ED. In December, DG accepted higher-priced procurement from Rustic Bloom to meet volume needs.
   - GE consistently matches or exceeds production levels, primarily active in Q1 and Q3-Q4, often offering better prices than ED.
- Region: Primarily North and South (mostly North).
- Segment Focus:
   - Dầu TV Northern: Food.
   - An Dương: Feed.
   
##### Other consideration

- Other competing companies have lower production levels but higher prices than ED, indicating potential operational inefficiencies or supply issues.
- If we wish to analyze the best deals for the specified month, we can assess whether we secured the optimal price at that time.


Recommendations Summary

- **Engage with New Partners:** Seek collaborations with Glistening Marsh and Feathered Sky for competitive pricing and enhanced production.
- **Increase Stock during Favorable Pricing:** Plan to stockpile refined oil from Radiant Bliss during September-October to benefit from times of lower pricing.
- **Investigate Market Dynamics:** Conduct a deeper analysis into competitors like Ice Coyote to understand pricing and sales volume discrepancies.
- **Strengthen Relationships with Current Suppliers:** Continue partnerships with Verdant Meadow and Radiant Bliss to maintain competitive pricing and reliable sourcing.
- **Optimize Sourcing Strategies:** Focus on strategic sourcing to ensure efficient procurement at lower costs, enhancing competitive positioning.























































