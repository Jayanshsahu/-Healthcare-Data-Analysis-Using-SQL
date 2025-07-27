                                             🏥 -Healthcare-Data-Analysis-Using-SQL
                                             
                  This project focuses on performing end-to-end SQL-based data analysis on a synthetic
                  healthcare dataset. It includes comprehensive querying to extract patient, hospital,
                  treatment, and insurance insights From understanding patientdemographics
                  to ranking hospitals and medical conditions, the project highlights
                  how SQL can derive actionable intelligence in healthcare analytics.


❓ Problem Statement

                  Healthcare providers and policy makers require insights into patient 
                  data to optimize resources, improve patient care, and manage costs. This project aims to:

                  Analyze hospitalizations and billing trends

                  Identify high-risk patients and care patterns

                  Track common medical conditions and treatment paths

                  Rank hospitals, insurance providers, and blood type distributions


📂 Raw Data Details

                  Dataset Name: healthcare_dataset

                  Format: SQL-ready tabular dataset

                  Data Size: ~20+ columns and numerous rows (volume not specified)

                  Source: Synthetic dataset created for learning and analysis

                  Database: Healthcare


🧾 Column Overview


                  | Column              | Description                                         |
                  | ------------------- | --------------------------------------------------- |
                  | Name                | Name of the patient                                 |
                  | Age                 | Patient's age                                       |
                  | Gender              | Patient's gender                                    |
                  | Blood\_Type         | Blood group                                         |
                  | Medical\_Condition  | Diagnosed condition                                 |
                  | Medication          | Medicines prescribed                                |
                  | Insurance\_Provider | Name of insurance provider                          |
                  | Hospital            | Hospital where admitted                             |
                  | Doctor              | Doctor's name                                       |
                  | Date\_of\_Admission | Admission date                                      |
                  | Discharge\_Date     | Discharge date                                      |
                  | Billing\_Amount     | Total treatment cost                                |
                  | Test\_Results       | Test outcome (`Normal`, `Abnormal`, `Inconclusive`) |



📂 Raw Data Details

Dataset Name: Healthcare

Format: Structured table (relational database)

Data Source: Synthetic dataset designed for educational and analytical purposes (not real patient data)

Database Name: Healthcare

Table Name: healthcare


<img width="960" height="470" alt="Screenshot tt 190001" src="https://github.com/user-attachments/assets/e7906436-ab2d-4ad9-893d-11d75c3b08ec" />



📊 Key Business Questions & Findings

                  1. 📈 Patient Demographics

                  Total Records:
                  SELECT COUNT(*) FROM Healthcare;

                  Max & Avg Age:
                  SELECT MAX(age) FROM Healthcare;
                  SELECT ROUND(AVG(age), 0) FROM Healthcare;


🏥 Hospital & Medical Insights

           Most Preferred Hospital:
                  SELECT Hospital, COUNT(*) FROM Healthcare GROUP BY Hospital ORDER BY COUNT(*) DESC;




           Most Common Medical Conditions:
                  SELECT Medical_Condition, COUNT(*) FROM Healthcare GROUP BY Medical_Condition ORDER BY COUNT(*) DESC;




           Top Medicines per Condition (Ranked):
                  SELECT Medical_Condition, Medication, COUNT(*) AS Total, 
                  RANK() OVER(PARTITION BY Medical_Condition ORDER BY COUNT(*) DESC) AS Rank_Medicine
                  FROM Healthcare GROUP BY 1,2;




            💸 Financial Analysis
                  Avg Billing by Condition:
                  SELECT Medical_Condition, ROUND(AVG(Billing_Amount),2) FROM Healthcare GROUP BY Medical_Condition;




           Total Billing by Insurance Provider:
                  SELECT Insurance_Provider, ROUND(SUM(Billing_Amount), 2) FROM Healthcare GROUP BY Insurance_Provider;




           Min, Max, Avg by Insurance:
                      SELECT Insurance_Provider, ROUND(AVG(Billing_Amount),0), 
                      ROUND(MIN(Billing_Amount),0), ROUND(MAX(Billing_Amount),0)
                      FROM Healthcare GROUP BY Insurance_Provider;




          Universal Donors/Receivers:
                    SELECT 
                    (SELECT COUNT(*) FROM Healthcare WHERE Blood_Type = 'O-') AS Universal_Blood_Donor,
                    (SELECT COUNT(*) FROM Healthcare WHERE Blood_Type = 'AB+') AS Universal_Blood_Receiver;




           🧪 Test Result-Based Patient Status
                  Risk Categorization:

                  SELECT Name, Medical_Condition, Test_Results,
                  CASE 
                  WHEN Test_Results = 'Inconclusive' THEN 'Need More Checks'
                                      WHEN Test_Results = 'Normal' THEN 'Ready for Discharge'
                    
                  WHEN Test_Results = 'Abnormal' THEN 'Needs More Attention'
                  END AS Status
                  FROM Healthcare;




           🧠 Learnings & Skills Applied

                  SQL Joins, Aggregations, Ranking (RANK, DENSE_RANK)

                  Stored Procedures & Conditional Logic

                  Real-world healthcare use-case simulation

                  Window functions and CASE WHEN statements





           📜 License
                  This project is released under the MIT License.
                  For educational and demonstrative use only.



           ✅ Summary
                  This healthcare project demonstrates how structured data analysis with SQL can bring
                  out hidden trends in medical records. From cost insights to hospital performance, the
                  queries help simulate decisions that could assist hospital managers, 
                  insurance analysts, and healthcare planners.
