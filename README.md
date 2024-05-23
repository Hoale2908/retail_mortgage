# Loan-To-Value and Retail Mortgage Loan Default

## Project objective: 
- Assess the quality of the dataset and make modifications as needed.
- Assess the impact of the Loan-To-Value (LTV) ratio on the Probability of Default of mortgage loan applicants.

![alt text](http://url/to/img.png)

## 1. Variables not requiring any modifications:

There are no missing data or outliers detected in **Application ID** and **Default in 12 Months.** 

## 2. Variables requiring modifications:

**LTV (Loan to Value), Mortgage Value On Application (Estimate), and Amount at Application:**
- There are 29 records with missing *LTV* data (denoted by "99999999.99") and 10 records with missing *Mortgage Value On Application (Estimate)* data (denoted by "99999999"). Additionally, 3 other records have an *LTV* of less than 1% or more than 2400%. As the model's performance depends on the accuracy of *LTV*, it is recommended that these records be removed from the sample.
- There are 2 records with negative *LTV* which may have been caused by data entry errors in *Amount at Application* (these values are also negative). We will convert these amounts to positive values. 

**Date of Application:** 
- There are 5 records with missing data (0.5% of the sample). *Date of Application* is usually not a direct cause for loan default unless there is a significant economic downturn which can negatively impact a vast number of loan applicants. Therefore, we can impute the missing data with a special value (i.e. "2015-01-01") for future reference.  
- Records that are dated before 2009-01-01 will be removed from the sample. The remaining records are between 2009-01-01 and 2015-01-01.

**Loan Tenor (in months):**
- There are 3 records with missing data. Given that it only represent 0.3% of the sample, we can assume that these applicants have a loan tenor equal to the sample's mean and update them accordingly.

**Age of Applicant** and **Years in Current Job:**
- It follows that applicants should be at least 18 years old. However, there are 83 records where the applicant's age is under 18 and the *Years in Current Job* is exactly 18 years less than *Age of Applicant*, which suggests a substraction was performed for this field rather than gathering the actual information. Since this represents less than 1% of the sample, we will replace *Age of Applicant* with the mean age and the corresponding *Years in Current Job* with "N/A". Other records with negative *Years in Current Job* will also be replaced with "N/A".

**Employment Status, Area,** and **Exposure to Other Banks:**
- Missing data in Employment Status, Area, and Exposure to Other Banks accounts for 14.4%, 1%, and 57% of the sample, respectively. These variables can still be helpful to the model, thus it is recommended to fill them with relevant "Other" or "0".
