# RBMS-BSC-LPN-File-Python-Dataframe
The script's purpose is to check each record for existing MARC 260/264 subfield $a values and 008 MARC Country Code value against a dataframe version of the RBMS/BSC Latin Place Names File, supply normalized geographic data in the MARC 752 field when possible, and output the results into three separate spreadsheets for review.

## RBMS-BSC-LPN-File-Dataframe.ipynb
MARC record evaluation and dataframe querying takes place before a record is sent on to one of the Python script’s three PyMARC writers.  The evaluation process splits the original MARC file into one of three possible paths based on the data contained within the records.

### Option 1: When 752s Are Already Present on MARC Record
The script identifies MARC records with MARC 752s already present and writes them to a file for manual review and URI enrichment.

### Option 2: Script Adds 752s to MARC Record
The Python script assigns the MARC Country Code in the 008 field and the MARC 260/264 subfield $a to variables.  Then, the script queries the pandas dataframe to find a relevant match. If a match within the dataframe exists, the script compiles the subfield components for the MARC 752 field and the script adds the field to the MARC record. 

### Option 3: Script Does Not add 752s to MARC Record
By design, the script does not add a MARC 752 field for some use cases.  They can be broadly categorized into the following five groups:
- The script identifies potential errors present in the MARC record.
- The script identifies an imprint location that could refer to several places and the cataloger will need to evaluate the record manually and in greater context.
- The script can not identify the imprint place. 
- The script user needs to add additional imprint information to the CSV file.
- The MARC record lists two places of imprint.
A rare materials cataloger needs to resolve and verify, in further consultation with bibliographic utilities and with research on the typical locations of the publisher, manufacturer, etc. by a manual process.

## MasterChartcleaner.csv
This csv file is fed into the script as a pandas (https://pandas.pydata.org/index.html) dataframe.  It contains all the RBMS/BSC Latin Place Names File (http://rbms.info/lpn/) as well as additional entries from rare materials bibliographic practice.   Each row within the CSV file is also populated with the various values comprising the MARC 752 subfield components, including the country ($a), the first-order political jurisdiction (i.e. state or province) ($b), city ($d), relator term ($e), relator term URI ($4), and Real World Object URI ($1).  The script user feeds additional locations and place name variations into the script for processing making for a flexible, locally customizable, and responsive design. 

## Relationship to the RBMS/BSC Latin Place Names File
The CSV version of the Latin Place Names File has also been enriched with data from other bibliographic utilities.  Please report any errors in the CSV to kkdavis@umn.edu

## Test-37-Records.mrc
This binary MARC file is supplied for testing purposes.

## Script Output (CSV and DAT files)
The Python script publishes additional pandas (https://pandas.pydata.org/index.html) dataframes as CSV files. The CSV files are meant for human consumption and at a glance can help further diagnose errors within the MARC records and/or verify various components of the MARC 260/264/752 fields.  The DAT files are formatted as UTF-8 binary MARC.

