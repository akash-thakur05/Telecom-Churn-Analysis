# Power Query Transformations & DAX Measures

## Power Query — New Columns in prod_Churn

```
Churn Status = if [Customer_Status] = "Churned" then 1 else 0

Monthly Charge Range =
  if [Monthly_Charge] < 20 then "< 20"
  else if [Monthly_Charge] < 50 then "20-50"
  else if [Monthly_Charge] < 100 then "50-100"
  else "> 100"
```

## Power Query — Age Group Table (mapping_AgeGrp)

```
Age Group =
  if [Age] < 20 then "< 20"
  else if [Age] < 36 then "20 - 35"
  else if [Age] < 51 then "36 - 50"
  else "> 50"

AgeGrpSorting =
  if [Age Group] = "< 20" then 1
  else if [Age Group] = "20 - 35" then 2
  else if [Age Group] = "36 - 50" then 3
  else 4
```

## Power Query — Tenure Group Table (mapping_TenureGrp)

```
Tenure Group =
  if [Tenure_in_Months] < 6 then "< 6 Months"
  else if [Tenure_in_Months] < 12 then "6-12 Months"
  else if [Tenure_in_Months] < 18 then "12-18 Months"
  else if [Tenure_in_Months] < 24 then "18-24 Months"
  else ">= 24 Months"
```

## DAX Measures

```dax
Total Customers = COUNT(prod_Churn[Customer_ID])
New Joiners = CALCULATE(COUNT(prod_Churn[Customer_ID]), prod_Churn[Customer_Status] = "Joined")
Total Churn = SUM(prod_Churn[Churn Status])
Churn Rate = [Total Churn] / [Total Customers]
Count Predicted Churner = COUNT(Predictions[Customer_ID]) + 0
Title Predicted Churners = "COUNT OF PREDICTED CHURNERS : " & COUNT(Predictions[Customer_ID])
```
