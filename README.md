# Hospital-Visits-AnalysisIntroduction

Healthcare organizations generate large amounts of operational and financial data from patient visits, admissions, diagnoses, procedures, billing, and patient feedback. When these data points are stored in a flat dataset, it can be difficult to identify patterns in revenue, patient activity, departmental performance, and satisfaction.

For this project, I developed an interactive Hospital Visits & Revenue Dashboard using Microsoft Power BI. The objective was to transform a raw hospital visits dataset into a dashboard that allows users to explore financial performance, patient demographics, departmental activity, doctor-level performance, and patient satisfaction.

The project involved working with a CSV dataset containing 30 hospital visit records and 31 fields, followed by data preparation, analysis, DAX measure creation, visualization, and dashboard design.

1. Project Objectives

The main objectives of the project were to:

Analyze hospital revenue generated from patient visits.
Compare revenue across departments.
Examine revenue patterns by date and patient gender.
Analyze doctor-level billing and patient volumes.
Monitor patient satisfaction.
Compare actual revenue against a predefined hospital revenue target.
Create an interactive dashboard that allows users to filter results by department.

The project also provided an opportunity to practice a complete Power BI workflow from raw data to business intelligence reporting.

2. Dataset Overview

The dataset contains 30 hospital visit records with 31 columns.

The fields cover several areas of hospital operations, including:

Patient information
Patient ID
Patient name
Patient gender
Patient age
County
Sub-county
Doctor information
Doctor ID
Doctor name
Doctor gender
Doctor specialty
Doctor experience
Hospital structure
Department
Ward
Department ID
Ward ID
Clinical information
Diagnosis
Diagnosis category
Procedure
Procedure category
Admission type
Length of stay
Triage level
Financial information
Total bill in KES
Insurance provider
Payment method
Patient experience
Patient satisfaction score
Follow-up requirement

The dataset contained 25 unique patients, 4 doctors, 4 departments, 18 diagnoses, and 15 procedures.

3. Data Quality Assessment

Before creating the dashboard, I assessed the dataset for common data-quality issues.

The initial checks showed:

Data-quality check	Result
Total records	30
Total columns	31
Duplicate records	0
Duplicate visit IDs	0
Missing values	8
Missing-value field	Insurance provider
Date range	June 1–15, 2026

The only missing values were in the insurance_provider field, where 8 records did not contain an insurance provider.

Rather than treating these missing values as a data error automatically, they can be retained as blank/unknown values because a missing insurance provider may represent a patient who did not provide insurance information or did not use insurance.

4. Data Preparation

The raw CSV was imported into Power BI and prepared for analysis.

The key preparation steps included:

Date transformation

The visit_date field was converted from text into a proper date data type.

This was important because Power BI needs a valid date field to support:

Daily analysis
Monthly trends
Date hierarchies
Time-based visualizations

The dataset covers:

June 1, 2026 – June 15, 2026

Data-type validation

Numeric fields such as:

patient_age
doctor_experience_years
length_of_stay_days
total_bill_kes
patient_satisfaction_score

were checked to ensure that Power BI interpreted them correctly.

Categorical fields such as:

Department
Gender
Admission type
Diagnosis category
Payment method
Triage level

were treated as categorical dimensions.

5. Key DAX Measures

Instead of relying entirely on implicit aggregations, explicit DAX measures can make the model easier to maintain and the dashboard easier to understand.

Total Hospital Revenue
Total Revenue =
SUM(HospitalVisits[total_bill_kes])

The dataset produced total revenue of:

KES 488,000

Total Visits
Total Visits =
COUNT(HospitalVisits[visit_id])

Result:

30 visits

Average Bill per Visit
Average Bill =
DIVIDE(
    [Total Revenue],
    [Total Visits]
)

Result:

KES 16,266.67 per visit

Average Patient Satisfaction
Average Satisfaction =
AVERAGE(HospitalVisits[patient_satisfaction_score])

Result:

4.28 / 5

Revenue Target

For the dashboard, I used a revenue target of KES 500,000.

Revenue Target = 500000
Target Achievement
Target Achievement % =
DIVIDE(
    [Total Revenue],
    [Revenue Target]
)

With KES 488,000 generated against a KES 500,000 target, the dashboard indicates approximately:

97.6% target achievement

6. Dashboard Design

The dashboard was designed around several analytical questions rather than simply displaying raw data.

The main visual sections include:

Revenue by Department

The department analysis shows:

Department	Visits	Revenue
Cardiology	9	KES 210,100
Orthopedics	6	KES 105,200
General Medicine	9	KES 97,800
Pediatrics	6	KES 74,900

Total:

KES 488,000

Cardiology generated approximately 43.1% of total revenue, while Orthopedics contributed approximately 21.6%.

This visualization makes it easy for a user to see how revenue is distributed across hospital departments.

7. Revenue by Patient Gender

The dataset contains:

Gender	Visits	Revenue	Average Satisfaction
Female	16	KES 247,400	4.46
Male	14	KES 240,600	4.08

Female patients accounted for 16 of the 30 visits, while male patients accounted for 14.

The difference in revenue between the two groups is relatively small despite the difference in visit counts.

This demonstrates why looking at both volume and revenue is useful rather than relying on one metric.

8. Revenue Trend Over Time

The daily revenue trend reveals substantial variation during the 15-day period.

For example:

June 2 generated approximately KES 70,000
June 5 generated approximately KES 91,000
June 8 generated approximately KES 60,000
June 9 generated approximately KES 84,000

In contrast, several days generated less than KES 10,000.

An important characteristic of this dataset is that there are exactly two visits per day. Therefore, changes in daily revenue are largely driven by differences in the billing amounts of individual visits rather than differences in the number of visits.

That is an interesting analytical observation to mention in the article.

9. Doctor-Level Analysis

The dashboard also compares billing by doctor.

Doctor	Visits	Revenue
Dr. Brian Mwangi	9	KES 210,100
Dr. Peter Otieno	6	KES 105,200
Dr. Sarah Wanjiku	9	KES 97,800
Dr. Faith Chebet	6	KES 74,900

Dr. Brian Mwangi's department generated the largest amount of billing in this dataset, while Dr. Faith Chebet's generated the lowest.

However, because each doctor is associated with a particular department in this dataset, doctor revenue should not be interpreted as a standalone measure of doctor performance. Differences can reflect department mix, procedures, diagnoses, admission types, and patient complexity.

That is an important limitation to document in a professional data-analysis project.

10. Admission Type Analysis

Another interesting finding comes from admission type.

Admission type	Visits	Revenue
Outpatient	20	KES 97,500
Inpatient	9	KES 368,500
Emergency	1	KES 22,000

Although inpatient visits represent only 9 of the 30 visits, they account for KES 368,500, or roughly 75.5% of total revenue.

This illustrates how visit volume alone does not explain financial performance.

A smaller number of higher-complexity or longer-duration encounters can contribute substantially more revenue.

11. Triage-Level Analysis

The dataset also contains four triage categories.

Triage	Visits	Revenue
Red	7	KES 307,000
Orange	3	KES 83,500
Yellow	10	KES 62,600
Green	10	KES 34,900

The Red category accounts for the largest share of revenue.

This pattern is consistent with the fact that higher-acuity cases in the dataset tend to have larger bills.

However, because the dataset is small and synthetic/project-sized, this should not be generalized to broader hospital populations.

12. Patient Satisfaction

The overall patient satisfaction score is:

4.28 / 5

The departmental averages are:

Department	Average Satisfaction
Cardiology	4.49
Pediatrics	4.43
Orthopedics	4.23
General Medicine	4.00

This provides another perspective alongside revenue.

A department can therefore be analyzed using multiple dimensions:

Revenue → Patient volume → Satisfaction

rather than looking at financial performance alone.

13. Important Dashboard Design Improvement

There is one thing I would change before publishing the dashboard as a polished portfolio project.

Your current satisfaction donut is titled:

Sum of patient_satisfaction_score by department_name

The visual is currently adding satisfaction scores together.

For example, Cardiology has a satisfaction total of 40.4.

That is mathematically valid, but average satisfaction is much more meaningful for a healthcare dashboard because the number of patients differs between departments.

I would replace it with:

Average Satisfaction =
AVERAGE(HospitalVisits[patient_satisfaction_score])

and change the visual title to:

Average Patient Satisfaction by Department

This makes the interpretation much clearer.

14. Revenue Target Analysis

The dashboard contains a gauge showing:

Target: KES 500,000

Actual: KES 488,000

Therefore:

Target achievement = 488,000 / 500,000
                   = 97.6%

The dashboard can therefore communicate the financial position using a simple KPI:

KES 488K Revenue | 97.6% of Target

For a portfolio project, I would also make the target explicitly configurable rather than embedding 500000 directly in several measures.

15. Interactive Filtering

The dashboard includes a department slicer containing:

Cardiology
General Medicine
Orthopedics
Pediatrics

This allows users to select a department and observe how the dashboard responds.

For example, selecting Cardiology can filter the revenue, doctor, satisfaction, and other visuals to that department.

This demonstrates one of the key advantages of Power BI over static reports: users can interact with the data rather than simply reading predefined charts.

16. Technical Architecture

The project follows a straightforward BI workflow:

Raw CSV
   ↓
Data Profiling
   ↓
Power Query
   ↓
Data Type & Quality Checks
   ↓
DAX Measures
   ↓
Power BI Data Model
   ↓
Interactive Visualizations
   ↓
Dashboard
   ↓
Business Insights

The project demonstrates the transition from raw operational data to decision-support information.

17. Tools and Technologies
Microsoft Power BI

Used for:

Data transformation
Data modeling
DAX calculations
KPI development
Interactive visualization
Dashboard design
Power Query

Used for:

Data ingestion
Data-type conversion
Data-quality inspection
Transformation of the source data
DAX

Used for:

Revenue calculations
Visit counts
Average billing
Satisfaction metrics
Target achievement
CSV

Used as the original source data format.

18. Key Insights

Based on the 30 records analyzed, the dashboard identified several patterns:

1. Total revenue was KES 488,000.

2. Cardiology generated the largest departmental revenue at KES 210,100.

3. Inpatient encounters generated KES 368,500, representing approximately 75.5% of total revenue despite accounting for only 9 visits.

4. Red-triage encounters generated KES 307,000.

5. Female patients accounted for 16 visits and KES 247,400 in billing, while male patients accounted for 14 visits and KES 240,600.

6. Overall average patient satisfaction was 4.28/5.

7. The hospital generated KES 488,000 against the dashboard target of KES 500,000, equivalent to 97.6% target achievement.

These findings demonstrate how combining operational, financial, clinical, and patient-experience fields can provide a more complete view of hospital activity.

19. Challenges and Lessons Learned

One of the main lessons from the project was that creating a dashboard is not simply about choosing attractive charts.

The analytical meaning of each measure matters.

For example, using:

SUM(patient_satisfaction_score)

answers the question:

"What is the total of all satisfaction scores?"

But:

AVERAGE(patient_satisfaction_score)

answers a more useful question:

"What was the average satisfaction level?"

This distinction is important when designing business intelligence dashboards.

I also learned the importance of:

Validating data types before visualization.
Checking missing values.
Checking duplicate records.
Choosing appropriate aggregation methods.
Using explicit DAX measures.
Avoiding misleading visual titles.
Considering dataset limitations before interpreting results.
20. Limitations

This project has several limitations.

First, the dataset contains only 30 records, so the findings should not be treated as representative of an entire hospital.

Second, the analysis covers only 15 days.

Third, several variables are highly structured, with each doctor corresponding to a department. This limits the ability to independently compare doctors.

Finally, the dataset contains only eight missing insurance-provider values and does not provide enough historical information to analyze long-term trends.

These limitations would need to be addressed before using a similar dashboard for actual operational decision-making.

Conclusion

This project demonstrates how Power BI can transform a flat hospital dataset into an interactive analytical dashboard.

Starting with a CSV containing patient, clinical, financial, and satisfaction information, I performed data-quality checks, prepared the dataset for analysis, created DAX measures, designed interactive visualizations, and extracted meaningful patterns from the data.

The final dashboard provides users with a consolidated view of:

Revenue | Patient Visits | Departments | Doctors | Admission Types | Triage | Gender | Satisfaction | Revenue Target

More importantly, the project reinforced the idea that effective data analytics is not only about creating visualizations. It requires understanding the underlying data, selecting appropriate measures, validating calculations, and communicating insights without overstating what the data can prove.
