# Data Cleaning Project with Pandas

This project demonstrates comprehensive data-cleaning techniques using the Pandas library in Python. The data used in this project is an Excel file containing a customer call list. The primary tasks performed include data ingestion, removal of duplicates, cleaning of specific columns, and standardization of data.

## Table of Contents

1. [Project Structure](#project-structure)
2. [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Running the Project](#running-the-project)
3. [Detailed Steps](#detailed-steps)
    - [Task 0: Ingestion of the Data Source in Pandas](#task-0-ingestion-of-the-data-source-in-pandas)
    - [Task 1: Drop the Duplicates](#task-1-drop-the-duplicates)
    - [Task 2: Remove the Unwanted Columns](#task-2-remove-the-unwanted-columns)
    - [Task 3: Clean Up the Last Name](#task-3-clean-up-the-last-name)
    - [Task 4: Clean the Phone Number Column](#task-4-clean-the-phone-number-column)
    - [Task 5: Split the Address](#task-5-split-the-address)
    - [Task 6: Standardizing the 'Paying Customer' Column](#task-6-standardizing-the-paying-customer-column)
    - [Task 7: Standardizing the 'Do Not Contact' Column](#task-7-standardizing-the-do-not-contact-column)
    - [Task 8: Replacing NaN or 'None' Values with Blank](#task-8-replacing-nan-or-none-values-with-blank)
    - [Task 9: Remove the Rows of Customers Who Do Not Want to Be Called](#task-9-remove-the-rows-of-customers-who-do-not-want-to-be-called)
    - [Task 10: Remove the Rows Where the Customers Do Not Have a Phone Number](#task-10-remove-the-rows-where-the-customers-do-not-have-a-phone-number)
    - [Task 11: Reset the Index](#task-11-reset-the-index)
4. [Contributing](#contributing)



## Project Structure

The project is organized in a Jupyter Notebook and covers the following steps:

1. **Ingestion of the Data Source**: Loading the Excel file into a Pandas DataFrame.
2. **Dropping Duplicates**: Identifying and removing duplicate entries in the dataset.
3. **Removing Unwanted Columns**: Dropping columns that are not needed for analysis.
4. **Cleaning Up Last Names**: Stripping unwanted characters from the last names.
5. **Cleaning the Phone Number Column**: Removing non-alphanumeric characters and formatting phone numbers.
6. **Splitting the Address Column**: Separating the address into street address, state, and zip code.
7. **Standardizing the 'Paying Customer' Column**: Converting 'Yes'/'No' responses to 'Y'/'N'.
8. **Standardizing the 'Do Not Contact' Column**: Converting 'Yes'/'No' responses to 'Y'/'N'.
9. **Replacing NaN or 'None' Values**: Filling missing values with blanks.
10. **Removing Uncontactable Customers**: Removing rows where customers do not want to be contacted.
11. **Removing Customers Without Phone Numbers**: Removing rows where customers have no phone numbers.
12. **Resetting the Index**: Resetting the DataFrame index after row deletions.

## Getting Started

### Prerequisites

- Python 3.x
- Pandas library
- Jupyter Notebook
- An Excel file named `Customer Call List.xlsx`

### Installation

To run this project, you need to have the necessary Python packages installed. You can install them using pip:

```bash
pip install pandas jupyter
```

### Running the Project

1. Clone the repository or download the Jupyter Notebook file.
2. Ensure the Excel file `Customer Call List.xlsx` is in the correct path.
3. Open the Jupyter Notebook:

```bash
jupyter notebook data_cleaning_pandas.ipynb
```

4. Run the cells in the notebook sequentially to perform data cleaning.

## Detailed Steps

### Task 0: Ingestion of the Data Source in Pandas

First, we load the Excel file into a Pandas DataFrame:

```python
import pandas as pd

df = pd.read_excel("path/to/Customer Call List.xlsx")
df.head()
```

### Task 1: Drop the Duplicates

Next, we remove any duplicate rows from the DataFrame:

```python
df = df.drop_duplicates()
df.head()
```

### Task 2: Remove the Unwanted Columns

Remove columns that are not needed for further analysis:

```python
df = df.drop(columns='Not_Useful_Column')
df.head()
```

### Task 3: Clean Up the Last Name

Strip unwanted characters from the last names:

```python
df['Last_Name'] = df['Last_Name'].str.strip('...')
df['Last_Name'] = df['Last_Name'].str.strip('/')
df['Last_Name'] = df['Last_Name'].str.strip('_')
df.head()
```

### Task 4: Clean the Phone Number Column

Remove non-alphanumeric characters and format phone numbers:

```python
df['Phone_Number'] = df['Phone_Number'].str.replace('[^a-zA-Z0-9]', '', regex=True)
df['Phone_Number'] = df['Phone_Number'].apply(lambda x: str(x))
df['Phone_Number'] = df['Phone_Number'].apply(lambda x: x[0:3] + '-' + x[3:6] + '-' + x[6:10])
df['Phone_Number'] = df['Phone_Number'].str.replace('nan--', '')
df['Phone_Number'] = df['Phone_Number'].str.replace('Na--', '')
df.head()
```

### Task 5: Split the Address

Separate the address into street address, state, and zip code:

```python
df[['Street_Address', 'State', 'Zip_Code']] = df['Address'].str.split(',', n=2, expand=True)
df.head()
```

### Task 6: Standardizing the 'Paying Customer' Column

Convert 'Yes'/'No' responses to 'Y'/'N':

```python
df['Paying Customer'] = df['Paying Customer'].str.replace('Yes', 'Y')
df['Paying Customer'] = df['Paying Customer'].str.replace('No', 'N')
df.head()
```

### Task 7: Standardizing the 'Do Not Contact' Column

Convert 'Yes'/'No' responses to 'Y'/'N':

```python
df['Do_Not_Contact'] = df['Do_Not_Contact'].str.replace('Yes', 'Y')
df['Do_Not_Contact'] = df['Do_Not_Contact'].str.replace('No', 'N')
df.head()
```

### Task 8: Replacing NaN or 'None' Values with Blank

Fill missing values with blanks:

```python
df = df.fillna('')
df.head()
```

### Task 9: Remove the Rows of Customers Who Do Not Want to Be Called

Remove rows where customers do not want to be contacted:

```python
for x in df.index:
    if df.loc[x, "Do_Not_Contact"] == 'Y':
        df.drop(x, inplace=True)
df.head()
```

### Task 10: Remove the Rows Where the Customers Do Not Have a Phone Number

Remove rows where customers have no phone numbers:

```python
for x in df.index:
    if df.loc[x, "Phone_Number"] == '':
        df.drop(x, inplace=True)
df.head()
```

### Task 11: Reset the Index

Reset the DataFrame index after row deletions:

```python
df = df.reset_index(drop=True)
df.head()
```

## Contributing

If you wish to contribute to this project, feel free to fork the repository and submit a pull request. For major changes, please open an issue first to discuss what you would like to change.


