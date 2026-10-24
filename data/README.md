# Data

The notebook uses two files of AdventureWorksDW, Microsoft's official sample data warehouse. They are not stored in this repository.

1. Download the official ZIP file:
   https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip
2. Extract it.
3. Copy these two files into this `data` folder:
   - `DimSalesTerritory.csv`: the sales territories (region, country, territory group)
   - `FactInternetSales.csv`: the internet sales orders

The files have no header row and use `|` as the separator. The order of their columns is in the `CREATE TABLE` statements of `instawdbdw.sql`, which is in the same ZIP file.

Source: Microsoft SQL Server Samples, https://github.com/microsoft/sql-server-samples (MIT License).