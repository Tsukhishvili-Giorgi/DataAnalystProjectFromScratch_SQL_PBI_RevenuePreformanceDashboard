# DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard
# Revenue Performance Dashboard


## Problem Statement

###  Revenue by Region:

Sum total fees from the service data table and group them
by the region from the branch data table to see which
region generates the most revenue.

### Revenue by Deparment:

Sum total fees from the service data table and group them
by the department from the service data table to see which
department generates the most revenue.

### Revenue by Client:

Determine the Top client.


### Steps followed 

- Step 1 : Load data into SQL, dataset is a SQL file.
- Step 2 : Cleaned data and created problem solving queries.
- Step 3 : Queries for each problem statement:
### Revenues by Region:

        SELECT b.Region,
		        s.service_date AS ServiceDate,
		        SUM(s.total_revenue) AS TotalRevenue
        FROM serviceData s
        Join branchData B ON s.branch_id = b.Branch_ID
        GROUP BY b.Region, s.service_date;

### Revenue by Deparment:

        SELECT department,
		        SUM(total_revenue) AS TotalRevenue,
		        service_date AS ServiceDate
        FROM  ServiceData
        GROUP BY department, service_date;

### Revenue by Client:

        SELECT client_name,
	        SUM(total_revenue) AS TotalRevenue,
	        service_date AS ServiceDate
        FROM  ServiceData
        GROUP BY client_name, service_date;

- Step 4 : Saved this queries and import it into PowerBI Desktop;
- Step 5 : Created DAX measures for KPI:

        * Total Revenue = Sum(serviceData[total_revenue])
        * Total Hours = Sum(serviceData[hours])
        * Revenue % of Overall by Region =
                DIVIDE(
                        SUM('Revenues by Region'[TotalRevenue]),
                        CALCULATE([Total Revenue], ALL(serviceData))
                ) * 100
        * Month on Month Revenue % Increase = 
                VAR CurrentMonthRevenue = SUM(serviceData[total_revenue])
                VAR PreviousMonthRevenue = CALCULATE(
                        SUM(serviceData[total_revenue]),
                        DATEADD(serviceData[service_date], -1, MONTH)
                )       
                VAR RevenueChange = IF(
                        PreviousMonthRevenue = 0,
                        BLANK(),
                        (CurrentMonthRevenue/PreviousMonthRevenue) -1
                )       
                RETURN RevenueChange *100
- Step 6 : Established Relationships between Data Models;
- Step 7 : Created Dashboard design for page "Revenue Performance Dashboard".
- Step 8 : Visual filters (Slicers) were added for three fields named:
Region

Quarter

Month


- Step 9 : Created Date Hierarchy:

        DateTable = CALENDAR(MIN(serviceData[service_date]),MAX(serviceData[service_date]))

- Step 10 : Create Key meausre table for all measurement;
- Step 11 : A donut chart and 100 % stacked column chart are used to show Revenue by Region. While creating this visual, a Column named "Region" was also added to the Legends field, and TotalRevenue meausre was added to the Value field.

![Total_Revenue_By_Region](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/c9315b20-ae37-4604-8571-70337c30927a)

![Revenue%_Of_Overall](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/d22d0e9d-2a76-4112-b90f-ce251b0bb55b)

- Step 12 : A line chart used to show the Month on Month Revenue % Increase:

![Month_on_Month_Revenue%_Increase](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/c57ff5c2-1a4a-460e-af75-5edafcb28327)


- Step 13 : The Cards used to show TotalRevenue and TotalHour.

![Total_Revenue](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/a84d9dad-33d0-4929-b9b8-d088ba91aef7)

![Total_Hour](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/2aec66ea-4789-42f6-9766-635d0661679c)

- Step 14 : A Table used to show Client's name by Revenue.

![Table_Of_Clients_By_Revenue](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/d0ed16d7-57ae-4bbd-91d8-394ba64404c9)

- Step 15 : 100 % Stacked bar chart are used to show Revenue by Deparment.

![image](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/5c1142f2-a95e-4314-adff-076bf6058fd0)


 # Report Snapshot (Power BI DESKTOP)

 ## Revenue Performance Dashboard

![Revenue_Preformance_Dashboard](https://github.com/Tsukhishvili-Giorgi/DataAnalystProjectFromScratch_SQL_PBI_RevenuePreformanceDashboard/assets/117026869/edff0442-5119-45e6-9b20-b157e676ac6f)

# Insights

The following inferences can be drawn from the dashboard;


## [1] Revenue by Region

### Total Revenue = 195 319 800

 - Europe = 73 691 700 (37.73 %)

 - Americas = 48 765 000 (24.97 %)

 - APAC = 48 759 000 (24.96 %)

 - EMEA = 24 104 100 (12.34 %)

           Thus, the higher number of Revenue is from the Europe.
           
## [2] Revenue by Department

- Audit = 39 224 100

- Management = 39 221 400

- Advisory = 39 024 300

- Tax = 38 991 000

- Legal = 38 859 000

        Thus, the revenue of almost all departments is more or less equal.
  
  ### [3] Top 5 Clients
        
- Smith Inc - 379 500

- Smith PLC -323 100

- Smith Group - 308 400

- Smith LLC - 285 000

- Williams and Sons - 283 200


