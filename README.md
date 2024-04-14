# Ecommerce Analysis - Dashboard

## Problem Statement

Currently, the company wants to implement improvements to achieve effective Business operations and goals. The company has 3 main goals.
- Increase sales
- Reduce delivery costs
- Market basker analysis

## Insight

### Executive Summary

![Screenshot 2024-04-14 122358](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/77fa5077-5b25-470c-a6aa-d052bbfc8f37)

Food category has the highest sales, and the best-selling product is Taste of the Wild High Prairie Grain-Free Dry Dog Food 40 lb which is also in this product group.
But the Food category does not bring a very significant profit margin percentage (only 22.67%), which can be inferred that the cost of purchasing and delivery of this category is too high. Compared to the Electronics category, which accounts for more than 44.28% of the total profit, it can be seen that the company manages costs very well for this category.

=> It is necessary to identify products that tend to be purchased together with products with high sales volume. Based on that, conduct upsell promotion projects to reduce delivery costs per product unit.
## Shipping metrics
![Screenshot 2024-04-14 122646](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/76215cae-fb81-4c98-ab75-2bd3939d924f)
Through the dashboard we can see that if we do well in cross-selling, delivery costs will be significantly reduced. Specifically, if the number of products per order is 11 products, we will save $118,190.40.
## Market Basket Analysis
![Screenshot 2024-04-14 122846](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/ea7b6e68-f28c-4404-a330-1703c47298be)

Relying on Market Basket Analysis helps marketing, sales and product strategy departments deploy effective cross-sell projects by identifying which products are often purchased together.

For example, Taste of the Wild High Prairie Grain-Free Dry Dog Food 40 lb is the top-selling product, and Memory Foam Pet Beds for Small, Medium, and Large Dogs and Cats is often purchased with it. The marketing department can offer discounts when purchasing the above two products together.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2:  Rename the tables.

      "face_table" to "sales"
      "dim_customers" to "customers"
      "dim_products" to "dim_products"
      "state_region_mapping.csv" to "State Mapping"
- Step 3 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 4 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on the entire dataset".
- Step 5:   It was observed that in none of the columns errors & empty values were present.
- Step 6: In "Invoice No" column was present 2% null values, need to remove transactions with empty invoice values. Open Power Query Editor  and filter out any "null".

![Screenshot 2024-04-13 142627](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/9ed2d369-2e37-45f1-860f-449f1243a4b7)

- Step 7: Check and fix the relationships automatically created by Power BI.

        The"Customers" and "Sales" table should be connected using the "Customer ID" column (one to many, single, single).
        The "Product" and "Sales" table should be connected using the "Stock Code" column (one to many, single).
        The "State Mapping" and "Customer" table should be connected using the "Order State" column  (many to many, both).


- Step 8:  Create a new blank table called "New_Measures" to contain the new measure.
- Step 9: Create a new measure called "Number of Customers" to uniquely count customers from the "Sales" table.

           Number of Customers=DISTINCTCOUNTNOBLANK(Sales[Customer ID]).

- Step 10: Create a new measure called  "Customer LTV (avg)" to assumpt for the Customer Lifetime value (The Lifetime value means the total value of all sales by a customer).  

          Customer LTV (avg) = SUM(Sales[Sales])/[Number of Customers]

 Step 11 : A Shap map was also added to the report design area representing the Customer LTV (avg)/State. 

 ![Screenshot 2024-04-13 162910](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/2e203620-3285-45c3-ad1b-22205c2e3c55)



=> Through this visual, we realize that North Dakota has the highest customer LTVs, which means customers in North Dakota play an important role in the total sales of the company. Marketing company should drive customer campaigns base on this insight.


- Step 12: Cleaning "Sales" table, replace "Indoor Pet Camera (Wi-Fi)" value into "Indoor Pet Camera" value.

- Step 13: Adding clustered  column chart to the report design area representing the Quality/Description.
- Step 14: Adding clustered bar chart to the report design area representing the Shipping_Cost _1000_mile/Description.
- Step 15: a Treemap visual was also added to the report design area representing the Total sales amount and Product category/Description. 


![Screenshot 2024-04-13 171017](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/4263578f-1f86-4043-8523-dbb5ae22241a)

"Taste of the Wild High Prairie Grain-Free Dry Dog Food 40 lb." leads in sales. But it also has the highest "Shipping_cost_1000_mile," and in addition to this, it has one of the lowest quantities. 
In conclusion, customers purchase Taste of the Wild High Prairie Grain-Free Dry Dog Food 40 lb with 1 item per order, which means customers don't usually purchase any product when they buy it.

Sheba Perfect Portions Pat Wet Cat Food Sheba Perfect Portions Pat Wet Cat Food sells well, and it also has the lowest "Shipping_cost_1000_mile," which means customers tend to purchase relevant products when they buy it. 

 

- Step 16: Create a visualization that displays the sales by quantity in clustered column chart. Filter out quantities less than zero and display the percentage of the grand total.
- Step 17: Duplicate the "Sales" table and rename the new table "Invoice Totals".
- Step 18: Group the information in the Invoice Totals table.

![Screenshot 2024-04-13 184125](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/f6b23ed9-4d84-4f50-aa18-d5f9720d1af7)

- Step 19: Create a visualization that displays the total sales by total quantity in clustered column chart. Filter out quantities less than zero and display the percentage of the grand total.

![Screenshot 2024-04-13 184810](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/b0e060af-6d71-4eca-8b14-eecd3072fc1c)


The percentage of total sales where a single item has been shipped by Whiskique is 5.98% which mean, the company do a good job selling multiple product types in singe invoice. This is a room for improvement in selling higher quantities of the same product.

- Step 20: Duplicate the "Sales" table and rename the new table "Market Basket Analysis".
- Step 21: Check and fix the relationships automatically created by Power BI.

        The "Sales" and "Market Basket" table should be connected using the "Invoice No" column  (many to many, both). 
- Step 22: Adding a table visual to the report design area representing the Description.
- Step 23: Create a bar chart showing the product count by product description.


![Screenshot 2024-04-13 194104](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/3301b8a1-f330-44bb-b87e-71f1f848d5e3)

This dashboard allows the company to see which product are purchased more often in combination with a specific product they select. 

For example: Earth-Rated Dog Poop Bags are bought when customers purchase Milk-Bone MaroSnacks Dog Treats with Real Bone.

- Step 24: A Shape map was also added to the report design area representing the Total sales/State. While creating this visual, field named "Region" was also added to the Legends bucket, thus total sales are also seggregated according the Region. 
 
![Screenshot 2024-04-14 082236](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/97a0b68e-d494-4802-9bae-9c25ba6668f9)

The state of Florida has the highest revenue on the East Coast.
The state of California has the highest revenue on the  West Coast.
The state of Texas the highest revenue on the  Central Coast.

- Step 25: To prepare for what-if Analysis, Create a new pamameter called "What-if quantity" of integer type, allow values from 1 to 20 in step of one, with current value set to five.

![Screenshot 2024-04-14 083042](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/6e686ebc-8373-4d8b-a68f-a4183b94775c)

- Step 26: Create a new measure in the What-if quantity table called "Blended Shipping Cost Factor", which calculates the discounted shipping cost based on the following table.
![Screenshot 2024-04-14 083441](https://github.com/HanhVy/Inventory-Analysis/assets/166614604/6317f059-1bb4-41e6-bafa-81c1584c473d)
             
             Blended Shipping Cost Factor = IF('What-if quantity'[What-if quantity Value]=1,1,IF('What-if quantity'[What-if quantity Value]=2, 0.8,IF('What-if quantity'[What-if quantity Value]<=4,0.6,IF('What-if quantity'[What-if quantity Value]<=7,0.5,IF('What-if quantity'[What-if quantity Value]<=9,0.4,0.3)))))



- Step 27: Create a new measure called "Shipping (Baseline)" which calculates the shipping cost based on the current adjustment of 70% applied to the shipping cost when shipping more than one item.

        Shipping (Baseline) = SUMX(Sales, IF(Sales[Quantity]=1,Sales[Shipping Cost],Sales[Shipping Cost]+ (Sales[Quantity]-1)*(Sales[Shipping Cost]*0.7)))

- Step 28: Create a new measure called "Shipping (What-if)" which calculates the shipping cost based on "Blended Shipping Cost Factor" instead of 0.7 as  Shipping (Baseline).

        Shipping (What-if) = SUMX(Sales,IF(Sales[Quantity]=1, Sales[Shipping Cost], Sales[Shipping Cost] + (Sales[Quantity]-1)*(Sales[Shipping Cost]*[Blended Shipping Cost Factor])))


- Step 29: Create a new measure called "Shipping (Different)" that calculates the different between "Shipping (What-if)" and "Shipping (Baseline)" 

          Shipping (Difference) = [Shipping (Baseline)]-[Shipping (What-if)]



- Step 30: Create three new measure called "Baseline running total", "What-if running total", "Difference running total" in the "Sales" table that calculates running total.


       Difference running total = SUMX(FILTER(ALLSELECTED(Sales),Sales[Transaction Date]<=MAX(Sales[Transaction Date])),[Shipping (Difference)])


       What-if running total = SUMX(FILTER(ALLSELECTED(Sales),Sales[Transaction Date]<=MAX(Sales[Transaction Date])), [Shipping (What-if)])
       

       Baseline running total = SUMX(FILTER(ALLSELECTED(Sales),Sales[Transaction Date]<=MAX('Market Basket'[Transaction Date])),[Shipping (Difference)])








