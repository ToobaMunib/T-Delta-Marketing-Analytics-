# T-Delta-Marketing-Analytics-
Customer Sentiment Analysis Project - SQL, Python, Power BI
Project Overview

This project demonstrates a complete end-to-end data analytics solution combining SQL data cleaning, Python sentiment analysis, and Power BI visualization to help T.Delta identify marketing optimization opportunities.

Status: Completed | Date: March 2026

Business Problem

T.Delta, an online retail business, faced declining customer engagement and conversion rates despite increased marketing investments. The project aimed to:

Analyze customer sentiment from reviews and social media
Identify root causes of low engagement
Provide actionable recommendations to improve conversion rates
Project Objectives
Increase Conversion Rates - Identify drop-off points in customer journey
Enhance Customer Engagement - Determine high-performing content types
Improve Customer Feedback Scores - Understand customer pain points and preferences
Technologies Used
Tool	Purpose
SQL Server	Data cleaning, aggregation, and preparation
Python	Sentiment analysis using NLTK VADER
Power BI	Interactive dashboard visualization
Excel	Data exploration and preliminary analysis
Project Workflow
Phase 1: Data Collection & Cleaning (SQL)
Extracted customer review data from fact_customer_reviews table
Removed duplicates using ROW_NUMBER() window function
Standardized data formats and handled missing values
Calculated key metrics (average order value, engagement rates)

Key SQL Queries:

sql
-- Remove duplicate reviews
WITH DuplicateRecords AS (
    SELECT 
        ReviewID,
        CustomerID,
        ProductID,
        ReviewDate,
        Rating,
        ReviewText,
        ROW_NUMBER() OVER (
            PARTITION BY CustomerID, ProductID, ReviewDate 
            ORDER BY ReviewID
        ) AS row_num
    FROM fact_customer_reviews
)
SELECT * FROM DuplicateRecords WHERE row_num = 1
Phase 2: Sentiment Analysis (Python)
Implemented NLTK VADER SentimentIntensityAnalyzer
Classified reviews as Positive, Negative, or Neutral
Calculated sentiment scores for each review
Aggregated sentiment by product, date, and customer segment

Key Python Code:

python
from nltk.sentiment.vader import SentimentIntensityAnalyzer
import pandas as pd

sia = SentimentIntensityAnalyzer()

def analyze_sentiment(text):
    scores = sia.polarity_scores(text)
    return scores['compound']

df['SentimentScore'] = df['ReviewText'].apply(analyze_sentiment)

def categorize_sentiment(score):
    if score >= 0.05:
        return 'Positive'
    elif score <= -0.05:
        return 'Negative'
    else:
        return 'Neutral'

df['SentimentCategory'] = df['SentimentScore'].apply(categorize_sentiment)
Phase 3: Dashboard & Visualization (Power BI)
Created interactive dashboards showing:
Sentiment distribution across products
Customer engagement trends over time
Conversion rate by content type
Top performing campaigns
Customer feedback themes
Key Findings
Sentiment Distribution:
Positive reviews: [46%]
Negative reviews: [24%]
Neutral reviews: [30%]
Engagement Insights:
Social media content drives highest engagement
Email campaigns need optimization
Product recommendations increase conversion
Customer Pain Points:
Shipping delays affecting satisfaction
Product quality issues in specific categories
Checkout process friction
Recommendations:
Focus marketing on high-sentiment products
Improve email campaign personalization
Address shipping and quality concerns
Optimize checkout experience
Power BI Dashboard
Interactive Dashboard Features:
Real-time sentiment analysis metrics
Customer engagement tracking by campaign
Conversion funnel visualization
Sentiment trends over time
Product-level performance analysis

Access Dashboard: 
https://1drv.ms/u/c/d69167803e8724fa/IQA9LZMoYQfVT7QrHZ0bcfeiAdRplfIYs-gyXjUWL7BqUhY?e=1eIhEx

Review this README for project overview
View the Power BI dashboard for interactive analysis
Check the presentation for detailed findings
Review code in the repository for implementation details

To Replicate This Project:
Clone this repository
Ensure you have SQL Server, Python 3.x, and Power BI installed
Replace database credentials in sentiment_analysis.py
Run python sentiment_analysis.py to perform sentiment analysis
Import cleaned data into Power BI for visualization
Project Structure
T-Delta-Analytics/
├── README.md (this file)
├── SQL_Scripts/
│   ├── data_cleaning.sql
│   ├── duplicate_removal.sql
│   └── aggregation_queries.sql
├── Python_Scripts/
│   ├── sentiment_analysis.py
│   ├── data_preparation.py
│   └── requirements.txt
├── Power_BI/
│   └── T_Delta_Dashboard.pbix
├── Documentation/
│   ├── Project_Presentation.pptx
│   └── Technical_Documentation.md
└── Data/
    └── Sample_Data.csv
Key Skills Demonstrated
Data Engineering: ETL processes, data cleaning, SQL optimization
Data Analysis: Statistical analysis, trend identification, insight generation
Machine Learning: Sentiment analysis, text processing (NLTK)
Business Intelligence: Dashboard design, KPI tracking, data storytelling
Tools: SQL Server, Python (Pandas, NLTK), Power BI, Excel
Problem Solving: Root cause analysis, actionable recommendations
Installation & Requirements
bash
# Python dependencies
pandas>=1.0
pyodbc>=4.0
nltk>=3.0
sqlalchemy>=1.4

# To install:
pip install -r requirements.txt
Results & Impact
Sentiment Analysis: Processed 1000+ customer reviews
Data Cleaned: Removed duplicates and standardized formats
Actionable Insights: Identified 5+ optimization opportunities
Business Impact: Provided recommendations to increase conversion by estimated 15-20%

Author
Tooba Munib 

MSc in Governance of Digitalization
Åbo Akademi University, Finland
Specializing in Business Analytics & Data Management

Contact
Feel free to reach out for questions about this project or to discuss data analytics opportunities!

License

This project is for portfolio purposes. The T.Delta company name and data are fictional examples.
