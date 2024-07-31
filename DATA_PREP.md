## Cleaning With Tableau Data Prep

1. Open Tableau Prep:
   - Launch Tableau Prep from your applications menu.

2. Create a New Flow:
   - On the start screen, click "New Flow" to start a new project.

3. Import the CSV File:
   - Click on "Connect to Data" on the left sidebar.
   - Select "Text File" and then browse to find your `raw.csv` file.
   - Click "Open" to import the file into Tableau Prep.

4. Add the Data to the Flow:
   - Drag the `raw.csv` file from the Connections pane into the flow workspace.

5. Handle Rows with Too Few Columns:
   - In the "Clean" step, look for rows with fewer columns than expected. You may need to manually review and remove these rows.
   - To remove these rows, click on the “Filter” icon, and set conditions to remove rows with missing values in key columns.

6. Remove Unnecessary Columns:
   - Click on the column header for the zipcode column. We don't need that. 
   - Right-click and select "Remove" to delete these columns from your dataset.

7. Remove Duplicate Rows:
   - In the "Clean" step, click on the “Remove Duplicates” button.
   - Tableau Prep will identify and remove duplicate rows based on all columns.

8. Handle Missing Values:
   - In the "Clean" step, identify columns with missing values (look for blank cells or NaN).
   - Click on the “Fill” or “Remove” options to handle missing values:
     - To fill missing values, select “Fill” and choose a default value.
     - To remove rows with missing values, click on the filter icon and set conditions to exclude rows with blanks.

9. Filter Outliers:
   - In the "Clean" step, visually inspect the data for values that are out of the expected range (e.g., unusually high or low values).
   - Click on the “Filter” icon and set conditions to remove rows with values outside expected ranges.

10. Handle Rows with Too Few Columns:
    - Check again for rows with fewer columns than expected.
    - If necessary, use the filter options to remove or correct these rows.

11. Correct Data Errors:
    - Review the data for errors such as invalid email formats or incorrect ages.
    - Click on individual cells with errors and manually correct them or use the “Replace” function.

12. Standardize Data Formats:
    - Ensure that all data formats are consistent (e.g., dates in a standard format).
    - Click on the column header and select “Change Data Type” to adjust formats if needed.

13. Correct Data Types:
    - Verify that each column has the correct data type (e.g., numeric for age and weight).
    - Click on the column header, then “Change Data Type,” and select the correct type if misclassified.

14. Encode Categorical Data:
   - For the "Married" column, create a new calculated field (i.e., “Married” as 1 and “Single” as 0).
   - Click on the “Add” button (usually represented with a “+” symbol) in the "Clean" step.
   - Select "Create Calculated Field" from the dropdown menu.
   - In the dialog that appears:
     - Give the new calculated field a name (e.g., "Married_Encoded").
     - In the calculation area, define the encoding logic using an IF statement. For example:
       ```sql
       IF [Married] = 'Married' THEN 1
       ELSE 0
       END
       ```
   - Click "OK" to save the calculated field.
   - Ensure that the new calculated field (e.g., "Married_Encoded") is added to your dataset.
   - Verify the encoding by inspecting the new field and checking a few sample rows to confirm that the values are as expected (1 for "Married" and 0 for "Single").


15. Save and Export Your Cleaned Data:
    - Click on “File” and then “Save As” to save your Tableau Prep flow.
    - To export the cleaned data, click on the “Output” tab, then select “Export Data” to save the cleaned dataset.

16. Review the Cleaned Data:
    - Inspect the cleaned data in Tableau Prep to ensure all cleaning tasks have been completed properly.

17. Close Tableau Prep:
    - After saving and exporting, close Tableau Prep.

18. Document Your Cleaning Process:
    - Record the steps you took in your README.md and any changes made to the data for future reference.
