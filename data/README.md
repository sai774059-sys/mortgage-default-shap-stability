# Data

This folder is a placeholder for the dataset. The raw data files are not included in this repository due to their size (approximately 50 GB uncompressed).

## Dataset

Freddie Mac Single-Family Loan-Level Dataset

Coverage: Fixed-rate single-family mortgage originations in the United States, 2016 to 2021

Access: Publicly available with free registration

Download page: https://www.freddiemac.com/research/datasets/sf-loanlevel-dataset

## File Structure

After downloading, the dataset should be organised as follows:

```
data/
|-- raw/
|   |-- 2016Q1/
|   |   |-- historical_data_2016Q1.txt        (origination file)
|   |   |-- historical_data_time_2016Q1.txt   (performance file)
|   |-- 2016Q2/
|   |   |-- ...
|   |-- ...
|   |-- 2021Q4/
|       |-- historical_data_2021Q4.txt
|       |-- historical_data_time_2021Q4.txt
```
Add data/README.mdA total of 24 origination files and 24 performance files are required, covering Q1 2016 through Q4 2021.

## Processing

Once the raw files are in place, the data processing cells in the notebook handle:

1. Year-by-year streaming of performance files in 300,000-row chunks
2. Computing the 90+ days past due within 12 months default flag
3. Merging with origination features
4. Saving processed labelled data to Parquet format

Processed Parquet files will be written to this folder after the notebook's preprocessing phase is run.

## Data Dictionary

The official Freddie Mac data dictionary and user guide are available at:
https://www.freddiemac.com/fmac-resources/research/pdf/user_guide.pdf

## Key Statistics

| Metric | Value |
|---|---|
| Total loans (2016-2021) | 14,146,041 |
| Total performance records | ~680 million |
| Default rate (overall) | 0.86% |
| Class imbalance ratio | 115:1 |
| Training set size (2016-2019) | 6,135,929 loans |
| Test set size (2020-2021) | 8,010,112 loans |
