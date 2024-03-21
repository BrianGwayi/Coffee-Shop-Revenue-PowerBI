# Coffee Shop Revenue Performance

This simple revenue report will help the client; a coffee retailer understand their
financial health and whether they are meeting revenue targets. Keeping a close eye on previous
month revenue also help identify growth opportunities, resource allocation and ultimately lead
the business to long term Sucess.

## Landing Page

![PBIDesktop_OlUKNlaaPm](https://github.com/BrianGwayi/Coffee-Shop-Revenue-PowerBI/assets/115585139/33c60224-0e7f-453c-9233-c07c251fdc48)


## Detailed Page

![PBIDesktop_tu1YirWecQ](https://github.com/BrianGwayi/Coffee-Shop-Revenue-PowerBI/assets/115585139/07a7cbd9-4957-44e3-bc11-f35243ed4fa9)


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
| | Indicator-Icons | Icon-Previous | ---- | 'Previous-Color-Code = IF([Current-Month] < [Previous-Month], "#FB5C36", "#1ed760")') |
| | | Icon-Target | ---- | 'Target-Color-Code = IF([Current-Month] < [Monthly-Target], "#FB5C36", "#1ed760")') |
| | Store-Color-Coding | STOR1-Color-Code | ---- | 'STOR1-Color-Code = IF([STOR-101] < [STOR-101-Tar], "#FB5C36", "#1ed760")') |
| | | STOR2-Color-Code | ---- | 'STOR2-Color-Code = IF([STOR-102] < [STOR-102-Tar], "#FB5C36", "#1ed760")') |
| | | STOR3-Color-Code | ---- | 'Store3-Color-Code = IF([STOR-103] < [STOR-103-Tar], "#FB5C36", "#1ed760")') |
| | Store-Pct | STOR-101-pct | Revenue contribution % | 'STOR-101-Pct = var MTDRevenue = CALCULATE([Current-Month], ALL(Transactions) VAR STOR101 = CALCULATE([Current-Month], Transactions[store_location] = "STOR 101") VAR STOR = DIVIDE(STOR101, MTDRevenue) RETURN STOR' |
| | | STOR-102-pct | Revenue contribution % | 'STOR-102-Pct = var MTDRevenue = CALCULATE([Current-Month], ALL(Transactions)) VAR MTDStore1 = CALCULATE([Current-Month], Transactions[store_location] = "STOR-102") VAR Store1Pct = DIVIDE(MTDStore1, MTDRevenue) RETURN Store1Pct')' |
| | | STOR-102-pct | Revenue contribution % | 'STOR1-Color-Code = IF([STOR-101] < [STOR-101-Tar], "#FB5C36", "#1ed760")') |

