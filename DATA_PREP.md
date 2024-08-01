## Cleaning With Tableau Prep

1. Open Tableau Prep:
   - Launch Tableau Prep from your applications menu.

2. Create a New Flow:
   - On the start screen, click New Flow to start a new project.

3. Import the CSV File:
   - Click on Connect to Data on the left sidebar.
   - Select Text File and then browse to find your `raw.csv` file.
   - Click Open to import the file into Tableau Prep.

4. Add the Data to the Flow:
   - Drag the `raw.csv` file from the Connections pane into the flow workspace.

5. Handle Rows with Too Few or Too Many Columns:
   - Generally, it is recommended to address these issues either in GitHub directly or by reviewing the file in Excel BEFORE importing your file into Tableau Prep. The following information is provided for those who would like to know how to perform this step in Tableau Prep. 
   - In Tableau Prep, identify rows that do not have the expected number of columns (9 in this case).
   - Use the following method to filter out rows with an incorrect number of columns:
     - Add a Clean step to your flow.
     - In the Clean step, create a calculated field to count the number of non-null columns in each row:
       - Click on the Add button (the plus symbol) and select Create Calculated Field.
       - Name the calculated field `ColumnCount`.
       - Use the following calculation to count non-null columns:
         ```sql
         IIF(ISNULL([ID]), 0, 1) + 
         IIF(ISNULL([Date]), 0, 1) + 
         IIF(ISNULL([Email]), 0, 1) + 
         IIF(ISNULL([Zip]), 0, 1) + 
         IIF(ISNULL([Age]), 0, 1) + 
         IIF(ISNULL([Height_Ft]), 0, 1) + 
         IIF(ISNULL([Height_In]), 0, 1) + 
         IIF(ISNULL([Weight_lbs]), 0, 1) + 
         IIF(ISNULL([Married]), 0, 1)
         ```
       - This calculation assigns a value of 1 for each non-null column and sums the values to get the total number of columns.
     - Add a Filter step to filter out rows with an incorrect number of columns:
       - Click on the Filter icon (funnel symbol).
       - Set the filter condition to `ColumnCount != 9` to exclude rows that do not have 9 columns.
     - After filtering, verify the number of remaining rows:
       - Rows Removed: 6 (Row 6, Rows 21-25)
       - Remaining Rows: 19

7. Remove Unnecessary Columns:
   - Click on the column header for the zipcode column. We don't need that.
   - Right-click and select Remove to delete this column from your dataset.

8. Remove Duplicate Rows:
   - In the Clean step, click on the Remove Duplicates button.
   - Tableau Prep will identify and remove duplicate rows based on all columns.

9. Handle Missing Values:
   - In the Clean step, identify columns with missing values (look for blank cells or NaN).
   - Click on the Fill or Remove options to handle missing values:
     - To fill missing values, select Fill and choose a default value.
     - To remove rows with missing values, click on the filter icon and set conditions to exclude rows with blanks.

10. Filter Outliers:
   - In the Clean step, visually inspect the data for values that are out of the expected range (e.g., unusually high or low values).
   - Click on the Filter icon and set conditions to remove rows with values outside expected ranges.

11. Correct Data Errors:
    - Review the data for errors such as invalid email formats or incorrect ages.
    - Click on individual cells with errors and manually correct them or use the Replace function.

12. Standardize Data Formats:
    - Ensure that all data formats are consistent (e.g., dates in a standard format).
    - Click on the column header and select Change Data Type to adjust formats if needed.

13. Correct Data Types:
    - Verify that each column has the correct data type (e.g., numeric for age and weight).
    - Click on the column header, then Change Data Type, and select the correct type if misclassified.

14. Encode Categorical Data:
    - For the "Married" column, create a new calculated field (i.e., “Married” as 1 and “Single” as 0).
    - Click on the Add button (usually represented with a “+” symbol) in the Clean step.
    - Select Create Calculated Field from the dropdown menu.
    - In the dialog that appears:
      - Give the new calculated field a name (e.g., Married_Encoded).
      - In the calculation area, define the encoding logic using an IF statement. For example:
      - ```sql
        IF [Married] = 'Married' THEN 1
        ELSE 0
        END
        ```
    - Click OK to save the calculated field.
    - Ensure that the new calculated field (e.g., Married_Encoded) is added to your dataset.
    - Verify the encoding by inspecting the new field and checking a few sample rows to confirm that the values are as expected (1 for "Married" and 0 for "Single").

15. Save and Export Your Cleaned Data:
    - Click on File and then Save As to save your Tableau Prep flow.
    - To export the cleaned data, click on the Output tab, then select Export Data to save the cleaned dataset.

16. Review the Cleaned Data:
    - Inspect the cleaned data in Tableau Prep to ensure all cleaning tasks have been completed properly.

17. Close Tableau Prep:
    - After saving and exporting, close Tableau Prep.

18. Document Your Cleaning Process:
    - Record the steps you took in your README.md and any changes made to the data for future reference.
   

-----

## Notes

- When working with CSV files, you may want to ensure your data is somewhat clean and well-formatted before importing it into Tableau Prep. Tools like Excel or a text editor can help you fix any formatting issues, e.g. incorrect number of columns and more. - The calculated fields in Tableau Prep use a SQL-like syntax. Understanding basic SQL concepts can be very helpful.
- Ensure you understand different data types (e.g., string, integer, date) and how to change them in Tableau Prep. Incorrect data types can lead to errors in analysis.
- Always keep a backup of your original data file before making any changes. This way, you can revert to the original data if needed.
- Tableau Prep's data profile pane is a powerful tool for understanding the distribution of your data, identifying outliers, and spotting errors.
- Data cleaning is an iterative process. You may need to repeat certain steps or try different techniques to achieve the best results.
- Make use of Tableau's extensive online resources, tutorials, and community forums to learn more about data cleaning and preparation.

## Multiple Tools

It is often useful to employ a variety of tools during the cleaning and transofrmation process. Best to have broad experience with Excel, SQL, Tableau Prep, and Python and then choose a limited set of areas in which you want to "go deep" and become a team expert. We work together. 
