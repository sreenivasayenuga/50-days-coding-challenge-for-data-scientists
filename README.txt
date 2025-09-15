Steps for analysis in Excel:
1. Import Raw Data from CSV in Excel named analysis.xlsl
- Copy the "Raw Data" section into Excel, paste into "Raw Data" sheet.
- Use Text to Columns (Comma-delimited) to split.
2. Create sheets in Excel in the names of By Family Size, Summary Stats, Monthly Averages, By Incomes, By Appliances, By Summary, and By Dashboard
3. Check missing data, duplicates, text, number, etc for data preprocessing.   
4. Create new features from existing features for feature engineering
- Use simple '+' for adding values of two columns for finding total energy and drag down.
- Add new column named as income level using the logical formula, =IF(C2<30000, "Low (<30k)", IF(C2<60000, "Medium (30-60k)", IF(C2<90000, "High (60-90k)", "Very High (>90k)"))) and drag down. 
5. Identify the problem, which is high electricity consumption and find ways for efficiencies from consumption using data on hand
6. Enable Data Analysis ToolPak from file->options->add-ins->analysis->toolpak->go->go->check->ok
7. In summary stats sheet, use AVERAGE function referencing raw data
- A2: "Avg Electricity", B2: =AVERAGE('Raw Data'!D2:D251)
- A3: "Avg Gas", B3: =AVERAGE('Raw Data'!E2:E251)
- A4: "Avg Total", B4: =AVERAGE('Raw Data'!H2:H251)
8. In summary stats sheet, add correlations using Data->Data Analysis->Correlation or alternatively use CORREL function. The formula usually throws error if the values are not numeric and the columns are not contiguous. Fix those issues if you have.
- use match function, =MATCH(G2, {"Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"}, 0), for converting text to numeric
- alternative use if function,=IF(G2="Jan",1,IF(G2="Feb",2,IF(G2="Mar",3,IF(G2="Apr",4,IF(G2="May",5,IF(G2="Jun",6,IF(G2="Jul",7,IF(G2="Aug",8,IF(G2="Sep",9,IF(G2="Oct",10,IF(G2="Nov",11,12))))))))))) for converting text to numeric. 
- Select range: 'Raw Data'!B2:H251 (Family_Size, Monthly_Income, Electricity_Usage, Gas_Usage, Appliances_Count, Total_Energy).
- Output to D1 in "Summary Stat or alternative use CORREL as follows:
- E2 (Family_Size vs. Family_Size): =CORREL('Raw Data'!B2:B251, 'Raw Data'!B2:B251) → 1.00
- J2 (Family_Size vs. Total_Energy): =CORREL('Raw Data'!B2:B251, 'Raw Data'!H2:H251) → 0.04
- J3 (Monthly_Income vs. Total_Energy): =CORREL('Raw Data'!C2:C251, 'Raw Data'!H2:H251) → 0.02
- J6 (Appliances_Count vs. Total_Energy): =CORREL('Raw Data'!F2:F251, 'Raw Data'!H2:H251) → -0.01
- J7 (Month_Numeric vs. Total_Energy): =CORREL('Raw Data'!I2:I251, 'Raw Data'!H2:H251) → 0.16
9. In monthly averages sheet, insert pivot table referencing raw data where rows are months and values are electricity usage, gas usage, and total energy. Select average in the field. Sort values in descending order.
10. In by family size sheet, insert pivot table referencing raw data where rows are family size and values are total energy set to average field value. Sort values in descending order.
11. In by income sheet, insert pivot table referencing raw data where rows are income levels and values are total energy set to average field value. Sort values in descending order.
12. In by appliances sheet, insert pivot table referencing raw data where rows are appliances count and values are total energy set to average field value. Sort values in descending order.
13. In dashboard sheet, create visualisations referencing pivot tables data from insert->charts->bar->clustered bar or slicers
14. Give summary with recommendations

