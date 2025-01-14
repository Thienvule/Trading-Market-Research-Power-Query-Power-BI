# Trading-Market-Research-Power-Query-Power-BI - Ongoing
Trading | Market Research | Power Query &amp; Power BI

## Context Overview

**Disclaimer**: This project utilizes real-world data that has been meticulously encoded and anonymized to ensure confidentiality. Sensitive information, including actual names and identifying details, has been transformed or obscured in the public file. This approach preserves the integrity of the analysis while prioritizing data privacy and security. What has been encoded/hidden will be explained carefully for the readers to understand the analysis flow as clearly as possible.
### Business Context
Eagle Dragon (encoded name: ED) is a trading company operating in the feed ingredients industry, specializing in the sale of crude (via its branch company - Phantom Eagle) and refined (branch company - Ember Dragon) oil products. By importing from global manufacturers, ED serves the Vietnamese market.

The primary objective for ED is to source the best prices, which serves as the cornerstone of its trading operations. To evaluate the company’s business activities for 2024, ED has tasked me, as the data analyst, with processing raw data acquired from market research. My goal is to generate insights that assess ED's performance in comparison to competitors and identify opportunities for improved sourcing strategies.

### Exploring Raw Files
Let's take a brief look at the raw data given:
![image](https://github.com/user-attachments/assets/fb3983dc-e9a4-4304-ad56-7213edae68ba)

I have received 12 files corresponding to each month of 2024. Each file contains 46 columns, with the number of rows varying based on the import transactions. This dataset encompasses import market data, which includes ED as well as other companies within the feed ingredients sector. However, since ED operates solely in the crude and refined oil sector, the data will be filtered to focus specifically on these areas.

A raw file (hidden values) of a total of 12 files would look like this: 

![image](https://github.com/user-attachments/assets/3ae0aaa0-e4ab-4e2a-929c-f71fb6d298af)

### Data Dictionary (Raw version)

The complete Data Dictionary will be provided at the end of this project for reference. For the purpose of this analysis, we will focus on these 10 key columns required for the calculations.
1. Tờ khai: Declaration form number or document reference for customs purposes.
2. Ngày đăng ký: The registration date of the customs declaration.
3. Tên doanh nghiệp XNK: The name of the export-import enterprise.
4. Đơn vị đối tác: The exporter involved in the transaction
5. Mã hàng khai báo: Code for the goods declared in the customs document.
6. Đơn giá khai báo (USD): The declared price per unit of goods in USD.
7. Lượng: Quantity of goods declared.
8. Đơn vị tính: Measurement unit for quantity (e.g., KGM, TNE, Bag).
9. Số hợp đồng: Contract number related to the transaction.
10. Thuế suất VAT: Value-added tax rate applied to the transaction.


### North Star Metric

The Trade Manager reveals that the Weighted Average Price is t 





























































### Raw Data Dictionary (CONSIDER DELETING)
1. Tờ khai: Declaration form number or document reference for customs purposes.
2. Ngày đăng ký: The registration date of the customs declaration.
3. Tên nơi mở tờ khai: The name of the location where the customs declaration was made.
4. Mã doanh nghiệp XNK: The export-import enterprise code.
5. Tên doanh nghiệp XNK: The name of the export-import enterprise.
6. Đơn vị đối tác: Partner unit involved in the transaction.
7. Mã hàng khai báo: Code for the goods declared in the customs document.
8. Số thứ tự hàng: Serial number for the goods.
9. Tên hàng: The name of the declared goods.
10. Đơn giá khai báo (USD): The declared price per unit of goods in USD.
11. Đơn giá NT khai báo: The declared unit price in local currency.
12. Đơn giá điều chỉnh (USD): Adjusted unit price per unit of goods in USD.
13. Đơn giá NT điều chỉnh: Adjusted unit price in local currency.
14. PP khai báo: Declaration method, explaining how the customs declaration was submitted.
15. PP áp giá: Pricing method used for customs valuation.
16. Nguyên tệ: Currency type of the declared price.
17. Tỷ giá nguyên tệ: Exchange rate of the local currency compared to VND at the time.
18. Tỷ giá USD: Exchange rate of USD compared to VND at the time.
19. Lượng: Quantity of goods declared.
20. Đơn vị tính: Measurement unit for quantity (e.g., KGM, TNE, Bag).
21. Tên nuớc xuất xứ: Country of origin for the declared goods.
22. Số hợp đồng: Contract number related to the transaction.
23. Ngày hợp đồng: The date of the related contract.
24. Mã phương thức thanh toán: Code representing the payment method used in the transaction.
25. Điều kiện giao hàng: Delivery terms agreed upon in the transaction.
26. Mã phương tiện vận chuyển: Code for the transport method used for the shipment (e.g., air freight, sea freight, road).
27. Phương tiện vận chuyển: Description of the transport method used for the shipment.
28. Kiểm tra giá cấp Tổng cục: Price inspection status at the national level.
29. Kiểm tra giá cấp Cục: Price inspection status at the industry level.
30. Kiểm tra giá cấp Chi cục: Price inspection status at the sub-department level.
31. Thuế suất XNK: Import and export tax rate applied to the goods.
32. Thuế suất TTĐB: Special consumption tax rate applied to the goods.
33. Thuế suất VAT: Value-added tax rate applied to the transaction.
34. Thuế suất tự vệ: Safeguard tax rate applied to the transaction.
35. Thuế XNK: Total import and export tax that must be paid.
36. Thuế TTĐB: Total special consumption tax that must be paid.
37. Thuế VAT: Total value-added tax that must be paid.
38. Thuế môi trường: Environmental tax applied to the goods.
39. Thuế tự vệ: Total antidumping tax that must be paid.
40. Xếp hạng DN: Enterprise ranking.
41. Trạng thái: Status of the transaction.
42. Kết quả kiểm tra STQ: Inspection results for quality control.
43. Nước nhập khẩu: Country of import for the goods.
44. Ngày KTG chi cục: Inspection date at the sub-department level.
45. Kết quả TVG chi cục: Inspection results from the sub-department.
46. Kết quả TVG cục: Inspection results from the industry department.





