# Study of the reliability of borrowers

## Description of the project

The customer is the credit department of the bank. It is necessary to find out whether the marital status and the number of children of the client affect the fact of repaying the loan on time. Input data from the bank - statistics on the solvency of customers.

The results of the study will be taken into account when building a credit scoring model - a special system that assesses the ability of a potential borrower to return a loan to a bank.

## Results of the study

**Data**

For the analysis, unloading of statistics on the solvency of customers was used. In the process of processing the dataset, several shortcomings were discovered that had to be processed.

- There are missing values in two columns. These are `days_employed` (work experience) and `total_income` - stores income data. The gaps in these columns were filled with the median value for each type from the `income_type` column.
Also, negative values were found in the `days_employed` column and values are not in days, but in hours. We recommend that you pay attention to the completion and format of data that fall into these columns, as incorrect and missing values \u200b\u200bmay distort the results.

- There are two anomalous values in the `children` column - -1 and 20. Rows with these values were not taken into account in this study. In the future, we recommend that you study the reasons for the appearance of these values in the upload (how are they filled in - by clients or automatically from other systems?)

- The `education` column has the same values, but written differently: using uppercase and lowercase letters. For processing, they brought them to lower case.

For convenience, the study combined part of the data into categories.
- *by income level*:
   - 0–30000 - 'E';
   - 30001–50000 - 'D';
   - 50001–200000 - 'C';
   - 200001–1000000 - 'B';
   - 1000001 and above - 'A'.

- *for the purpose of taking a loan*:
   - 'car operations',
   - 'real estate transactions',
   - 'holding a wedding',
   - 'getting an education'.

**Research results**

We looked at four parameters that can affect the return of a loan on time. Found out the following:
1. The presence of children negatively affects the repayment of the loan on time, however, the number of children is of relatively little importance.
2. "not married / not married" and "civil marriage" - groups with a high percentage of debtors.
3. Loan repayment on time is better provided by clients with "above average" incomes (200,001–1,000,000)
4. Wedding and real estate transactions - more likely to repay the loan on time than car transactions and education purposes
