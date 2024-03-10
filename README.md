
# Coffee Shop Revenue Performance

This simple Revenue report will help the Client understand their
financial health and whether they are meeting revenue targets. Keeping a close eye on revenue also help identify growth opportunities, resource allocation and ultimately lead the business to long term Sucess.


![PBIDesktop_GRI1uflsJR](https://github.com/BrianGwayi/CoffeeShopRevenue-PowerBI/assets/115585139/a57364a4-cb60-407a-8fd5-a3988029aaa2)

# Calculations for Measures
## Total Month to Date (MTD) Revenue

`Current-Month = CALCULATE(
        SUMX(Transactions,
        Transactions[transaction_qty] * Transactions[unit_price]),
        DATESMTD('Revenue-Calendar'[Date]))`

## Month to Date (MTD) Revenue for Individual Stores
STOR-101 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-101")

STOR-102 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-102")

STOR-103 = CALCULATE(
        [Current-Month],
        Transactions[store_location] = "STOR-103")

## Total Previous Month Revenue
Previous-Month = CALCULATE
        SUMX(Transactions,
        Transactions[transaction_qty] * Transactions[unit_price]),
        PREVIOUSMONTH(DATESMTD('Revenue-Calendar'[Date])))

## Overall Monthly Target
Monthly-Target = 170000

## Monthly Targets for Individual Stores
STOR-101-Tar = 50000
STOR-102-Tar = 60000
STOR-103-Tar = 45000


## Comparison Month to Date (MTD) vs Target
MTD-Vs-Tar = [Current-Month] - [Monthly-Target]

## Comparison Month to Date (MTD) vs Previous Month
MTD-Vs-Prev = [Current-Month] - [Previous-Month] 

## Coffee MTD Performance for each Categories

Arabica = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Arabica")

Excelsa = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Excelsa")

Liberica = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Liberica")

Robusta = CALCULATE(
        [Current-Month],
        Transactions[product_category] = "Robusta")

## Comparison for each Store
Tar-Var-Store1 = [STOR-101] - [STOR-101-Tar]
Tar-Var-Store2 = [STOR-102] - [STOR-102-Tar]
Tar-Var-Store3 = [STOR-103] - [STOR-103-Tar]


## Store Contribution%
STOR-101-Pct = 

var MTDRevenue = 
    CALCULATE([Current-Month],
        ALL(Transactions))

VAR STOR101 = 
    CALCULATE([Current-Month],
    Transactions[store_location] = "STOR-101")

VAR STOR = DIVIDE(STOR101, MTDRevenue)

    RETURN STOR


STOR-102-Pct = 

var MTDRevenue = 
    CALCULATE([Current-Month],
        ALL(Transactions))

VAR MTDStore1 = 
    CALCULATE([Current-Month],
    Transactions[store_location] = "STOR-102")

VAR Store1Pct = DIVIDE(MTDStore1, MTDRevenue)

    RETURN Store1Pct


STOR-103-Pct = 

var MTDRevenue = 
    CALCULATE([Current-Month],
        ALL(Transactions))

VAR STOR103 = 
    CALCULATE([Current-Month],
    Transactions[store_location] = "STOR-103")

VAR STOR = DIVIDE(STOR103, MTDRevenue)

    RETURN STOR

## Fields Color Coding
Previous-Color-Code = 
    IF([Current-Month] < [Previous-Month], "#FB5C36", "#1ed760")

Target-Color-Code = 
    IF([Current-Month] < [Monthly-Target], "#FB5C36", "#1ed760")

## Color Coding for Stores
STOR1-Color-Code = 
    IF([STOR-101] < [STOR-101-Tar], "#FB5C36", "#1ed760")

Store2-Color-Code = 
    IF([STOR-102] < [STOR-102-Tar], "#FB5C36", "#1ed760")

Store3-Color-Code = 
    IF([STOR-103] < [STOR-103-Tar], "#FB5C36", "#1ed760")

## Indicator Icons
Icon-Previous = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([Current-Month] < [Previous-Month],NegativeIcon,PositiveIcon)
    
RETURN
    Result


Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([Current-Month] < [Monthly-Target],NegativeIcon,PositiveIcon)
RETURN
    Result


## Indicator Icon by Store
Store1-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-101] < [STOR-101-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result


Store2-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-102] < [STOR-102-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result

Store3-Icon-Target = 
var PositiveIcon = UNICHAR(9650)
var NegativeIcon = UNICHAR(9660)
var Result = 
    IF([STOR-103] < [STOR-103-Tar], NegativeIcon, PositiveIcon)
RETURN
    Result

