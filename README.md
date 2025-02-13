# CAR SALES DASHBOARD

## OVERVIEW
The objective is to design and develop a dynamic and interactive Car Sales Dashboard using Power BI. This dashboard visualizes critical KPIs related to car sales for understanding and making data-driven business decisions by monitoring sales and analyzing trends.

## GENERAL FEATURES
### Key Metrics Tracked:
#### The dashboard focuses on the following KPIs:
- Sales Overview: Year-to-Date (YTD), Month-to-Date (MTD), Year-over-Year (YOY) growth, and comparisons with previous year figures.
- Average Price Analysis: Insights into average car prices over time and YOY growth.
- Cars Sold Metrics: Total cars sold by YTD/MTD, YOY growth, and comparisons with previous periods.
#### Visualizations Included:
- Weekly Sales Trend: Line chart for displaying weekly YTD sales trends.
- Sales by Body Style: Pie chart for showing the proportion of total sales by car body style.
- Sales by Color: Pie chart for highlighting contributions of different car colors to total sales.
- Regional Sales Distribution: Map chart for visualizing YTD car sales across dealer regions.
- Company-Wise Sales Trends: Tabular grid for summarizing YTD sales for each company.

## DAX FORMULAS USED
The following DAX formulas were used for KPI Calculation and visualization in dashboard
### Average Price Calculations
#### Average Price: Calculates the average price of cars sold.
```
Average Price = SUM(car_data[Price ($)]) / COUNT(car_data[Car_id])
```
#### Average Price Difference: Measures the difference between YTD average price and PYTD average price.
```
Average Price Difference = [YTD Average Price] - [PYTD Average Price]
```
#### Average Price Color: Assigns a color (Green/Red) based on whether the average price difference is positive or negative.
```
Average Price Color = IF([Average Price Difference] > 0, "Green", "Red")
```
### Cars Sold Metrics
#### YTD Cars Sold: Calculates the total number of cars sold year-to-date.
```
YTD Cars Sold = TOTALYTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])
```
#### PYTD Cars Sold: Calculates the total number of cars sold in the previous year up to the same date.
```
PYTD Cars Sold = CALCULATE(COUNT(car_data[Car_id]), SAMEPERIODLASTYEAR('Calendar Table'[Date]))
```
#### Cars Sold Difference: Measures the difference in cars sold between YTD and PYTD.
```
Cars Sold Difference = [YTD Cars Sold] - [PYTD Cars Sold]
```
#### Car Sold Color: Assigns a color (Green/Red) based on whether cars sold difference is positive or negative.
```
Car Sold Color = IF([Cars Sold Difference] > 0, "Green", "Red")
```
### Sales Metrics
#### YTD Total Sales: Calculates total sales year-to-date.
```
YTD Total Sales = TOTALYTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])
```
#### PYTD Total Sales: Calculates total sales for the previous year up to the same date.
```
PYTD Total Sales = CALCULATE(SUM(car_data[Price ($)]), SAMEPERIODLASTYEAR('Calendar Table'[Date]))
```
#### Sales Difference: Measures the difference between YTD total sales and PYTD total sales.
```
Sales Difference = [YTD Total Sales] - [PYTD Total Sales]
```
#### Sales Diff Color: Assigns a color (Green/Red) based on whether sales difference is positive or negative.
```
Sales Diff Color = IF([Sales Difference] > 0, "Green", "Red")
```
### Month-to-Date (MTD) Metrics
MTD Total Sales: Calculates total sales for the current month-to-date.
```
MTD Total Sales = TOTALMTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])
```
#### MTD Average Price: Calculates average price for the current month-to-date.
```
MTD Average Price = TOTALMTD([Average Price], 'Calendar Table'[Date])
```
#### MTD Cars Sold: Calculates total cars sold for the current month-to-date.
```
MTD Cars Sold = TOTALMTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])
```
### Year-over-Year (YOY) Growth Metrics
#### YOY Sales Growth: Measures YOY growth in total sales.
```
YOY Sales Growth = [Sales Difference] / [PYTD Total Sales]
```
#### YOY Average Price Growth: Measures YOY growth in average price.
```
YOY Average Price Growth = [Average Price Difference] / [PYTD Average Price]
```
#### YOY Car Sold Growth: Measures YOY growth in cars sold.
```
YOY Car sold Growth = [Cars Sold Difference] / [PYTD Cars Sold]
```
### Additional Calculations
#### Max Point on Area Chart: Highlights the maximum point on an area chart for weekly total sales.
```
Max Point on Area Chart = IF(MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sales]) = [Total Sales], MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sales]), BLANK())
```

## KEY FEATURES
- Interactive visualizations along with dynamic filtering options.
- Better monitoring of critical KPIs.
- Charts and Grids for better understanding and decision-making.
- Allows analysis of sales trends across various dimensions (time, region, body style, color).

