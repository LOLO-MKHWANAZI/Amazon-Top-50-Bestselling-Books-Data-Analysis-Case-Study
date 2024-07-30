# Amazon-Top-50-Bestselling-Books-Data-Analysis-Case-Study!

# Data Analysis Process for Amazon's Top 50 Best Selling Books Dataset

## Introduction
This document outlines the data analysis process for examining the Amazon Top 50 Best Selling Books dataset. The analysis aims to uncover insights into trends, patterns, and relationships within the data, guiding strategic decisions and actions.

## Phase 1: Ask

### Define the Objective
The primary objective is to analyze the dataset of Amazon's Top 50 Best Selling Books to gain insights into trends, patterns, and relationships. This analysis will help in understanding the market dynamics, customer preferences, and factors influencing book sales.

### Key Questions
- What are the most popular genres?
- How do price and user ratings correlate?
- What trends can be observed over time in publication dates?

## Phase 2: Prepare

### Data Collection
#### Step 1: Data Collection
1. **Identify Required Data:**
   - Title
   - Author
   - Genre
   - Price
   - Rating
   - Number of Reviews
   - Publication Date
   - Publisher
2. **Data Ingestion:**
   - Load the dataset into BigQuery for further analysis.
   - Ensure the data is in a suitable format for analysis.

### Data Cleaning
- Handle missing values by filling or removing them.
- Correct inconsistent formatting.
- Remove duplicate entries.
- Correct data types where necessary.

## Phase 3: Process

### Exploratory Data Analysis (EDA)
#### Step 3: Analyze
1. **Descriptive Statistics:**
   - Generate summary statistics (mean, median, mode) for key metrics such as price, rating, and number of reviews.
2. **Relationships and Trends:**
   - Identify and analyze correlations between variables, such as price and rating, and observe trends over time, such as publication dates.
3. **Categorization and Grouping:**
   - Analyze the distribution of genres and examine patterns based on author and publisher.

## Phase 4: Analyze

### Data Visualization and Insights
#### Step 4: Share
1. **Visualizations in Tableau:**
   - Create various visualizations to represent the data:
     - Bar charts for genre distribution.
     - Scatter plots for price vs. rating.
     - Line charts for trends over time.
2. **Insights and Recommendations:**
   - Derive key insights from the visualizations and provide actionable recommendations based on the analysis.

## Implementation Steps

### Setting Up BigQuery and Loading Data
#### Step 1: BigQuery Setup
1. **Create a Google Cloud Platform (GCP) Account:**
   - Set up a new project in the Google Cloud Console.
   - Enable the BigQuery API and set up billing.
2. **Create a Dataset in BigQuery:**
   - Navigate to BigQuery in the Google Cloud Console.
   - Create a new dataset.

#### Step 2: Uploading Data
1. **Prepare the CSV File:**
   - Ensure the CSV file containing the dataset is accessible.
2. **Create a New Table in BigQuery:**
   - Upload the CSV file, specifying the schema.
3. **Verify Data Structure:**
   - Run SQL queries to confirm the structure and contents of the data.

### Data Cleaning with SQL in BigQuery
#### Step 3: Data Cleaning
1. **Remove Duplicates:**
   - Use SQL queries to remove duplicate records.
2. **Handle Missing Values:**
   - Replace missing values appropriately.
3. **Correct Data Types:**
   - Standardize text fields and ensure correct data types.

### Performing EDA with SQL
#### Step 4: Exploratory Data Analysis (EDA)
1. **Generate Summary Statistics:**
   - Use SQL queries to compute averages and other statistics.
2. **Identify Relationships and Trends:**
   - Analyze the data to find correlations and trends.

### Example SQL Queries for Data Cleaning and EDA
#### Load Data and View Structure

```SQL
SELECT *
FROM `my-books-project-88198.upload_books_dataset.bestselling_books`
LIMIT 1000;


```
#### Remove Duplicates
```SQL
CREATE OR REPLACE TABLE `my-books-project-88198.upload_books_dataset.cleaned_books` AS
SELECT DISTINCT * 
FROM `my-books-project-88198.upload_books_dataset.bestselling_books`;
```
#### Handle Missing Values
```SQL
CREATE OR REPLACE TABLE `my-books-project-88198.upload_books_dataset.filled_books` AS
SELECT
  Name,
  Author,
  COALESCE(User_Rating, 0) AS User_Rating,
  COALESCE(Reviews, 0) AS Reviews,
  COALESCE(Price, 0) AS Price,
  Year,
  Genre
FROM `my-books-project-88198.upload_books_dataset.cleaned_books`;
```
#### Correct Data Types
```SQL
CREATE OR REPLACE TABLE `my-books-project-88198.upload_books_dataset.cleaned_books_final` AS
SELECT
  CAST(Name AS STRING) AS Name,
  CAST(Author AS STRING) AS Author,
  CAST(User_Rating AS FLOAT64) AS User_Rating,
  CAST(Reviews AS INT64) AS Reviews,
  CAST(Price AS INT64) AS Price,
  CAST(Year AS INT64) AS Year,
  CAST(Genre AS STRING) AS Genre
FROM `my-books-project-88198.upload_books_dataset.filled_books`;
```
#### Generate Summary Statistics
```SQL
SELECT
  AVG(Price) AS Avg_Price,
  AVG(User_Rating) AS Avg_Rating,
  AVG(Reviews) AS Avg_Reviews
FROM `my-books-project-88198.upload_books_dataset.cleaned_books_final`;

```
#### Genre Distribution
```SQL
SELECT
  Genre,
  COUNT(*) AS Count
FROM `my-books-project-88198.upload_books_dataset.cleaned_books_final`
GROUP BY Genre
ORDER BY Count DESC;
```
#### Price vs. Rating Correlation
```SQL
SELECT
  Price,
  User_Rating
FROM `my-books-project-88198.upload_books_dataset.cleaned_books_final`;
```


### Data Visualization with Tableau
#### Step 5: Visualization
1. **Connect Tableau to BigQuery:**
   - Open Tableau and connect to the data source.
   - Select the appropriate project, dataset, and table.
2. **Create Visualizations:**
   - **Genre Distribution Bar Chart:**
     - Columns: Genre
     - Rows: COUNT(Name)
     - Visualization Type: Bar Chart
     - 
    ![Distribution of Bestselling Books by Genre](https://github.com/user-attachments/assets/80a87a52-8b4d-43b9-b686-b1eee9937205)
   - 
   - **Price vs. Rating Scatter Plot:**
     - Columns: Price
     - Rows: User_Rating
     - Visualization Type: Scatter Plot
     - Optional: Differentiate by Genre and adjust size by Reviews.
   - **Publication Trends Line Chart:**
     - Columns: Year
     - Rows: COUNT(Name)
     - Visualization Type: Line Chart
   - **Top Authors by Number of Bestsellers:**
     - Columns: Author
     - Rows: COUNT(Name)
     - Visualization Type: Bar Chart
     - Filter: Top 10 by count

#### Step 6: Design the Dashboard
1. **Create a New Dashboard:**
   - Add visualizations to the dashboard.
   - Adjust the size and position for a balanced layout.
   - Add titles, captions, and interactivity.
   - Use filters and dashboard actions to enhance the user experience.

### Example Layout
- **Title:** "Analysis of Amazon Top 50 Best Selling Books"
- **Filters:** Genre and Year filters at the top.
- **Top Row:** Genre Distribution Bar Chart (left) and Top Authors by Number of Bestsellers (right).
- **Bottom Row:** Price vs. Rating Scatter Plot (left) and Publication Trends Line Chart (right).

## Act on Insights
Based on the visualizations and analysis, consider the following actions:

- **For Publishers:** Focus on trending genres and optimize pricing strategies based on customer ratings and reviews.
- **For Authors:** Identify popular genres and analyze top-performing books to understand market trends.
- **For Retailers:** Adjust marketing strategies to highlight books in popular genres and with high ratings.
