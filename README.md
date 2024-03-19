
# Coffee Shop Revenue Performance

This is a simple revenue report will help the client; a coffee retailer understand their
financial health and whether they are meeting revenue targets. Keeping a close eye on previous
month revenue also help identify growth opportunities, resource allocation and ultimately lead
the business to long term Sucess.

![PBIDesktop](https://github.com/BrianGwayi/CoffeeShopRevenue-PowerBI/assets/115585139/19b46add-415c-4cb8-8111-9655d44fe189)

# Documentation
## Tables
| Table-Name  | Description  | Table-Type |
| :------------ |:---------------:| -----:|
| Measures-Table | ---- | Power Query Table|
| Revenue-Calendar | ---- | Calculated Table|
| Update-DateTime | ---- | Power Query Table |
| Transactions | ----  | Power Query Table|

## Measures
| Table-Name  | Display-Folder  | Measure-Name | Description | Measure-Expression |
| :------------ |:---------------:| -----:|:------------| :------------|
| Measures-Table | Categories | Arabica | ---- | 'Arabica = CALCULATE([Current-Month],Transactions[product_category] = "Arabica"') |
| | | Excelsa | ---- | 'Excelsa = CALCULATE([Current-Month],Transactions[product_category] = "Excelsa"') |
| | | Liberica | ---- | 'Liberica = CALCULATE([Current-Month],Transactions[product_category] = "Liberica"') |
| | | Robusta | ---- | 'Robusta = CALCULATE([Current-Month],Transactions[product_category] = "Robusta"') |
| | Color-Coding | Previous-Color-Code | ---- | 'Previous-Color-Code = IF([Current-Month] < [Previous-Month], "#FB5C36", "#1ed760")') |
| | | Target-Color-Code | ---- | 'Target-Color-Code = IF([Current-Month] < [Monthly-Target], "#FB5C36", "#1ed760")') |



### Month to Date (MTD) Revenue

`Current-Month = CALCULATE(
        SUMX(Transactions,
        Transactions[transaction_qty] * Transactions[unit_price]),
        DATESMTD('Revenue-Calendar'[Date]))`

### Month to Date (MTD) Revenue for Stores
#### #Store 1
`STOR-101 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-101")`

#### #Store 2
`STOR-102 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-102")`

#### #Store 3
`STOR-103 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-103")`

### Month to Date (MTD) Revenue for Coffee Types

#### Arabica
`Arabica = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Arabica")`

#### Excelsa
`Excelsa = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Excelsa")`

#### Liberica
`Liberica = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Liberica")`
        
#### Robusta
`Robusta = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Robusta")`

### Previous Month Revenue
`Previous-Month = CALCULATE
        SUMX(Transactions,
        Transactions[transaction_qty] * Transactions[unit_price]),
        PREVIOUSMONTH(DATESMTD('Revenue-Calendar'[Date])))`

### Comparison Month to Date (MTD) vs Target
`MTD-Vs-Tar = [Current-Month] - [Monthly-Target]`

### Comparison Month to Date (MTD) vs Previous Month
`MTD-Vs-Prev = [Current-Month] - [Previous-Month]`

### Comparison Month to Date vs Taget for Stores
`Tar-Var-Store1 = [STOR-101] - [STOR-101-Tar]`
`Tar-Var-Store2 = [STOR-102] - [STOR-102-Tar]`
`Tar-Var-Store3 = [STOR-103] - [STOR-103-Tar]`


### Store Contribution%
#### Store 1
`STOR-101-Pct = 
        var MTDRevenue = 
        CALCULATE([Current-Month],
        ALL(Transactions))

        VAR STOR101 = 
        CALCULATE([Current-Month],
        Transactions[store_location] = "STOR-101")

        VAR STOR = DIVIDE(STOR101, MTDRevenue)
        RETURN STOR`


#### Store 2
`STOR-102-Pct = 
        var MTDRevenue = 
        CALCULATE([Current-Month],
        ALL(Transactions))

        VAR MTDStore1 = 
        CALCULATE([Current-Month],
        Transactions[store_location] = "STOR-102")
        
        VAR Store1Pct = DIVIDE(MTDStore1, MTDRevenue)
        RETURN Store1Pct`


#### Store 3
`STOR-103-Pct = 
        var MTDRevenue = 
        CALCULATE([Current-Month],
        ALL(Transactions))

        VAR STOR103 = 
        CALCULATE([Current-Month],
        Transactions[store_location] = "STOR-103")
        
        VAR STOR = DIVIDE(STOR103, MTDRevenue)
        RETURN STOR`

### Fields Color Coding
#### Color Code - Month to Date (MTD) vs Previous
`Previous-Color-Code = 
    IF([Current-Month] < [Previous-Month], "#FB5C36", "#1ed760")`

#### Color Code - Month to Date (MTD) vs Target
`Target-Color-Code = 
    IF([Current-Month] < [Monthly-Target], "#FB5C36", "#1ed760")`

### Color Coding - Month to Date (MTD) vs Target for Stores
`STOR1-Color-Code = 
    IF([STOR-101] < [STOR-101-Tar], "#FB5C36", "#1ed760")`

`Store2-Color-Code = 
    IF([STOR-102] < [STOR-102-Tar], "#FB5C36", "#1ed760")`

`Store3-Color-Code = 
    IF([STOR-103] < [STOR-103-Tar], "#FB5C36", "#1ed760")`

### Indicator Icons
#### Month to Date vs Previous
`Icon-Previous = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([Current-Month] < [Previous-Month],NegativeIcon,PositiveIcon)
    
RETURN
    Result`

#### Month to Date vs Target
`Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([Current-Month] < [Monthly-Target],NegativeIcon,PositiveIcon)
RETURN
    Result`


### Indicator Icon by Store
`Store1-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-101] < [STOR-101-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result`


`Store2-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-102] < [STOR-102-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result`

`Store3-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-103] < [STOR-103-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result`

