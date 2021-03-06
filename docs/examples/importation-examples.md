---
layout: default
title: Importation examples
parent: Examples
nav_order: 1
---

{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Import CSV file data

The [EXAMPLE1] shows how you can import all the data from a CSV file using the RFC-4180 standard as paramount. 

#### [EXAMPLE1]
*Note: the example uses the option `QuotationMode.Critical`, [learn more here](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html).*
```vb
Sub ImportRecords_RFC4180()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String
	
	filePath = "C:\Demo_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	Call CSVix.OpenConnection(fileName) 'Open a physical connection to the CSV file
	Call CSVix.ImportFromCSV 'Import data
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```

## Import top 10 records from a CSV file into a VBA array 

The [EXAMPLE2] shows how you can import the Top 10 records from a CSV file using the RFC-4180 standard as paramount.

#### [EXAMPLE2]
*Note: the example uses the option `QuotationMode.Critical`, [learn more here](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html).*
```vb
Sub ImportTopTenRecords_RFC4180()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String
	
	filePath = "C:\Demo_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	CSVix.EndingRecord = 10 'Sets the importation ending
	Call CSVix.OpenConnection(fileName) 'Open a physical connection to the CSV file
	Call CSVix.ImportFromCSV 'Import the range of records
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```
The [EXAMPLE3] accomplishes the same task of the [EXAMPLE1], the difference is that a temporary variable is used to store the CSV file's content instead of use the `OpenConnection` method. Also, the [EXAMPLE3] shows how to omit the CSV's headers.

#### [EXAMPLE3]
*Note: the example uses the option `QuotationMode.Critical`, [learn more here](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html).*
```vb
Sub ImportTopTenRecords_RFC4180()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String, tmpCSV As String
	
	filePath = "C:\Demo_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	tmpCSV = CSVix.GetDataFromCSV(filePath) 'Store CSV file's content.
	CSVix.EndingRecord = 10 'Sets the importation ending
	Call CSVix.ImportFromCSVString(tmpCSV, HeadersOmission:=True) 'Import the range of records omitting the headers
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```

## Import ten middle records from a CSV file into a VBA array 
The [EXAMPLE4] shows how you can import 10 middle records from a CSV file using the RFC-4180 standard as paramount.

#### [EXAMPLE4]
*Note: the example uses the option `QuotationMode.Critical`, [learn more here](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html).*
```vb
Sub ImportTenMiddleRecords_RFC4180()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String, tmpCSV As String
	
	filePath = "C:\Demo_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	tmpCSV = CSVix.GetDataFromCSV(filePath) 'Store CSV file's content.
	CSVix.StartingRecord = 11 'Sets the importation ending
	CSVix.EndingRecord = 20 'Sets the importation ending
	Call CSVix.ImportFromCSVString(tmpCSV, HeadersOmission:=True) 'Import the range of records omitting the headers
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```

## Import CSV file that haven’t special syntax

This is the fastest way to work with CSV files because the CSV interface class don't check the syntax given at the RFC-4180 standard. If your CSV files has trailing spaces, or you don't know if it holds a field needing to be escaped, please [reset the config options](https://ws-garcia.github.io/VBA-CSV-interface/api/methods/resettodefault.html) for the current instance to avoid incorrect results.

The [EXAMPLE5] shows how you can import all the data from a CSV file without checking the syntax given at the RFC-4180 standard. The file to be parsed has neither field needing to be escaped.

See also
:[QuotationMode](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html), [EscapeType](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/escapetype.html).
#### [EXAMPLE5]
*Note: the example uses the option `QuotationMode.All`, and `EscapeType.NullChar`*
```vb
Sub ImportRecords()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String
	
	filePath = "C:\Demo_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	Call CSVix.OpenConnection(fileName) 'Open a physical connection to the CSV file
	CSVix.QuotingMode = All 'Alter behavior for escaped files
	CSVix.EscapeChar = NullChar 'Specify that CSV file has neither field needing to be escaped.
	Call CSVix.ImportFromCSV 'Import data
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```
The [EXAMPLE6] shows how you can import all the data from a CSV file without checking the syntax given at the RFC-4180 standard. In the file to be parsed, all fields need to be escaped.

See also
:[QuotationMode](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/quotationmode.html), [EscapeType](https://ws-garcia.github.io/VBA-CSV-interface/api/enumerations/escapetype.html).
#### [EXAMPLE6]
*Note: the example uses the option `QuotationMode.All`, and `EscapeType.DoubleQuotes`*
```vb
Sub ImportRecords()
	Dim CSVix As CSVinterface
	Dim MyArray() As String
	Dim filePath As String
	
	filePath = "C:\Demo_Headed_400k_records.csv" 'Change this to suit your needs
	Set CSVix = New CSVinterface 'Create new instance
	Call CSVix.OpenConnection(fileName) 'Open a physical connection to the CSV file
	CSVix.QuotingMode = All 'Alter behavior for escaped files
	CSVix.EscapeChar = DoubleQuotes 'Specify that all fields need to be escaped.
	Call CSVix.ImportFromCSV 'Import data
	Call CSVix(MyArray) 'Dumps the data to array
	Set CSVix = Nothing 'Terminate the current instance
End Sub
```