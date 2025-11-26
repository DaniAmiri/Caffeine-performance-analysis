# Caffeine Intake and Cognitive Performance Analysis

## Abstract
This project examines the short-term impact of caffeine consumption on cognitive performance. Two types of cognitive tests were performed before and after caffeine intake: mathematical performance tests (response time and accuracy) and reaction-time tests. Caffeine intake logs were combined with timestamps from both tests to measure performance improvements and analyze their relationship with caffeine dosage and timing.

## Project Structure
Caffeine-performance-analysis/
│
├── data/
│   ├── coffee_log.csv
│   ├── math_test.csv
│   └── reaction_test.csv
│
├── caffeine_analysis.ipynb
└── README.md


## Dataset Description

### Coffee Log
- Date:
   Calendar date of caffeine intake
- Time (When did you take your caffeine?):
   Time of intake
- Amount of Caffeine (mg)
- coffee_date_time:
   Combined datetime column used for alignment

### Math Test
- response_time_seconds
- points:
   Number of correct answers (out of 5)
- percent_correct:
   Percent accuracy
- test_date_time:
   Combined datetime column used for alignment

### Reaction Test
- reaction_time_ms 
- test_date_time:
   Combined datetime column used for alignment

## Methodology

### Data Cleaning
- Unified all timestamps into standard Python datetime
- Corrected AM/PM inconsistencies (e.g., 12:00 pm incorrectly recorded as 12:00 am)  
- Dropped irrelevant columns (e.g., internal IDs and system-generated fields) to keep only variables needed for analysis.
- Removed incorrect duplicated reaction test recorded twice before the second caffeine consumption on day 10 
- Only days with all three datasets included (9, 10, 12)

### Before/After Test Alignment

A custom summary loop was implemented to pair each caffeine intake event with its nearest cognitive tests.  
For each caffeine event:

1. Filter all tests occurring on the same day  
2. Select the closest before-caffeine math and reaction tests  
3. Select the closest after-caffeine math and reaction tests

### Delta Computation

Δ reaction time (ms) = reaction_before_ms – reaction_after_ms
Δ math response time (s) = math_before_time_s – math_after_time_s
Δ math accuracy (%) = math_after_acc – math_before_acc

### Statistical and Visual Analysis
- Scatter plots with date/time annotations
- Correlation matrix computed between caffeine dose and all delta metrics
- Linear regression modeling using scikit-learn
- Extraction of slope and intercept values

## Results Summary
- The analysis showed that math response time increased after caffeine intake, meaning the participant took longer to complete the mathematical task at higher caffeine doses.
- Despite slower response times, the participant achieved a higher number of correct answers and improved accuracy after consuming caffeine.
- Reaction time generally improved after caffeine intake, but the magnitude of improvement varied across days.

## Reproducibility
Install required packages:
```
pip install pandas matplotlib scikit-learn
```

Run the notebook:
```
git clone https://github.com/DaniAmiri/Caffeine-performance-analysis.git
cd Caffeine-performance-analysis
jupyter notebook
```

Open:
```
caffeine_analysis.ipynb
```

## Limitations
- Very small dataset (3 complete days)
- Manual timestamp correction required
- Limited number of caffeine-test pairings
- Only short-term caffeine effects modeled

## Author
Dani Amiri  
GitHub: https://github.com/DaniAmiri
