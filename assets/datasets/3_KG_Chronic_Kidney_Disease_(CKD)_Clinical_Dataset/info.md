# Information About Dataset (KG Chronic Kidney Disease (CKD) Clinical Dataset)

## Characteristics:

```
DATASET OVERVIEW
Instances (rows):            25800
Columns:                     36
Features (excl. target):     35
Valid instances (no NaN):    25800 (100.00%)
Instances with any NaN:      0
Duplicate rows:              0
Memory:                      13249.1 KB
Features per instance ratio: 0.0014

COLUMN TYPES AND CLASSES
                                          type  unique  missing  missing_%                                                                                                         classes
Target                    categorical (string)       5        0        0.0  [Healthy Kidney, Kidney Failure (Stage 5), Mild CKD (Stage 1–2), Moderate CKD (Stage 3), Severe CKD (Stage 4)]
Age                          numeric (integer)      65        0        0.0                                                                                                               -
Gender                        numeric (binary)       2        0        0.0                                                                                                          [0, 1]
BMI                          numeric (integer)      17        0        0.0                                                                                                               -
Systolic_BP                  numeric (integer)     100        0        0.0                                                                                                               -
Diastolic_BP                 numeric (integer)      60        0        0.0                                                                                                               -
Heart_Rate                   numeric (integer)      50        0        0.0                                                                                                               -
Serum_Creatinine             numeric (integer)      10        0        0.0                                                                                  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Blood_Urea_Nitrogen          numeric (integer)     143        0        0.0                                                                                                               -
eGFR                         numeric (integer)     115        0        0.0                                                                                                               -
Urine_Albumin                numeric (integer)     815        0        0.0                                                                                                               -
Urine_Protein                numeric (integer)     480        0        0.0                                                                                                               -
Albumin_Creatinine_Ratio     numeric (integer)     941        0        0.0                                                                                                               -
Urine_Specific_Gravity         numeric (float)   25800        0        0.0                                                                                                               -
Sodium                       numeric (integer)      10        0        0.0                                                              [135, 136, 137, 138, 139, 140, 141, 142, 143, 144]
Potassium                    numeric (integer)       6        0        0.0                                                                                              [3, 4, 5, 6, 7, 8]
Calcium                      numeric (integer)       3        0        0.0                                                                                                      [10, 8, 9]
Phosphorus                   numeric (integer)       7        0        0.0                                                                                           [2, 3, 4, 5, 6, 7, 8]
Chloride                     numeric (integer)      14        0        0.0                                                                                                               -
Bicarbonate                  numeric (integer)      18        0        0.0                                                                                                               -
Hemoglobin                   numeric (integer)      12        0        0.0                                                                                                               -
RBC_Count                      numeric (float)   25800        0        0.0                                                                                                               -
WBC_Count                    numeric (integer)    6818        0        0.0                                                                                                               -
Platelet_Count               numeric (integer)   24680        0        0.0                                                                                                               -
Packed_Cell_Volume           numeric (integer)      30        0        0.0                                                                                                               -
Blood_Glucose_Random         numeric (integer)     130        0        0.0                                                                                                               -
Fasting_Glucose              numeric (integer)      60        0        0.0                                                                                                               -
HbA1c                          numeric (float)   25800        0        0.0                                                                                                               -
Cholesterol                  numeric (integer)     130        0        0.0                                                                                                               -
Triglycerides                numeric (integer)     200        0        0.0                                                                                                               -
Serum_Albumin                numeric (integer)       4        0        0.0                                                                                                    [1, 2, 3, 4]
Total_Protein                  numeric (float)   25800        0        0.0                                                                                                               -
Diabetes                  categorical (string)       2        0        0.0                                                                                                       [No, Yes]
Hypertension              categorical (string)       2        0        0.0                                                                                                       [No, Yes]
Smoking_Status            categorical (string)       2        0        0.0                                                                                                       [No, Yes]
Family_History_Kidney     categorical (string)       2        0        0.0                                                                                                       [No, Yes]

TYPE COUNTS
type
numeric (integer)       26
categorical (string)     5
numeric (float)          4
numeric (binary)         1

TARGET: Target
Task:                  classification
Number of classes:     5
Class values:          ['Healthy Kidney', 'Kidney Failure (Stage 5)', 'Mild CKD (Stage 1–2)', 'Moderate CKD (Stage 3)', 'Severe CKD (Stage 4)']
                          count      %
Target                                
Healthy Kidney            19359  75.03
Mild CKD (Stage 1–2)       3066  11.88
Moderate CKD (Stage 3)     1807   7.00
Severe CKD (Stage 4)       1052   4.08
Kidney Failure (Stage 5)    516   2.00
Imbalance ratio (max/min): 37.52
Majority-class baseline:   75.03%

NUMERIC FEATURE STATS
                                 min        max        mean        std   skew
Age                           20.000      84.00      51.968     18.796  0.000
Gender                         0.000       1.00       0.502      0.500 -0.010
BMI                           18.000      34.00      25.982      4.901  0.001
Systolic_BP                   90.000     189.00     113.454     19.127  1.322
Diastolic_BP                  60.000     119.00      75.265     12.085  1.130
Heart_Rate                    60.000     109.00      84.380     14.386  0.011
Serum_Creatinine               0.000       9.00       0.627      1.477  3.138
Blood_Urea_Nitrogen            7.000     149.00      21.672     20.773  3.035
eGFR                           5.000     119.00      91.513     26.764 -1.559
Urine_Albumin                  0.000     999.00      59.774    136.119  3.749
Urine_Protein                  0.000     499.00      31.111     73.049  3.691
Albumin_Creatinine_Ratio       0.000    1199.00      68.853    155.902  4.107
Urine_Specific_Gravity         1.005       1.03       1.017      0.007  0.001
Sodium                       135.000     144.00     139.485      2.871  0.005
Potassium                      3.000       8.00       3.720      0.826  1.837
Calcium                        8.000      10.00       9.001      0.816 -0.002
Phosphorus                     2.000       8.00       2.967      1.102  1.707
Chloride                      96.000     109.00     102.508      4.035 -0.001
Bicarbonate                   10.000      27.00      23.283      2.939 -1.210
Hemoglobin                     5.000      16.00      13.449      2.316 -1.289
RBC_Count                      4.000       6.00       4.999      0.577 -0.004
WBC_Count                   4000.000   10999.00    7488.379   2021.658 -0.001
Platelet_Count            150022.000  449965.00  300253.748  86406.140 -0.006
Packed_Cell_Volume            20.000      49.00      42.187      5.497 -1.314
Blood_Glucose_Random          70.000     199.00     134.326     37.566  0.005
Fasting_Glucose               70.000     129.00      99.474     17.277 -0.002
HbA1c                          4.001      10.00       6.995      1.732 -0.000
Cholesterol                  150.000     279.00     214.500     37.412 -0.002
Triglycerides                100.000     299.00     199.833     58.042 -0.006
Serum_Albumin                  1.000       4.00       3.600      0.763 -1.763
Total_Protein                  5.000       8.00       6.507      0.864 -0.012
```

## Source

- https://www.kaggle.com/datasets/priyankabarik/chronic-kidney-disease-ckd-clinical-dataset

## Usage

*Allowed only with Citation*


