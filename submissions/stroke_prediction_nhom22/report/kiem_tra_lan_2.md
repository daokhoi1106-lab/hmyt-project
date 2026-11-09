# Progress Test 2 — nhom22 — stroke_prediction

- Fork: <https://github.com/daokhoi1106-lab/hmyt-project> · Branch: gd5-proposed-model
- Members (student ID or alias) and roles:
- 202414847: research, EDA
- 202414837: research, data preparation
- 202414833: research, models testing and evaluation

## A. Literature review and research gaps

### A1. Search strategy
stroke risk prediction machine learning tabular data models evaluation Shapley Additive Explanation

### A2. Literature matrix

| # | Paper (authors, year) | DOI / link | Dataset (n, source) | Method | Main result (metric, value) | External validation? | Main limitation |
|---|---|---|---|---|---|---|---|
| 1 | Soladoye et al. (2025), *Machine learning techniques for stroke prediction: A systematic review of algorithms, datasets, and regional gaps* | https://doi.org/10.1016/j.ijmedinf.2025.106041 | 58 studies included in the systematic review | PRISMA-based systematic review and descriptive synthesis of ML algorithms and datasets | Ensemble methods achieved 90.4–97.8% accuracy for stroke occurrence prediction | Not applicable — systematic review rather than a single predictive model | High methodological heterogeneity prevented quantitative meta-analysis; restricted to open-access English-language studies |
| 2 | Dritsas & Trigka (2022), *Stroke Risk Prediction with Machine Learning Techniques* | https://doi.org/10.3390/s22134670 | 3,254 records from the public Kaggle Stroke Prediction Dataset | SMOTE, feature importance analysis, individual classifiers and stacking ensemble | Stacking achieved AUC 0.989, accuracy 98.0%, precision 97.4% and recall 97.4% | No | Small public dataset; limited clinical variables and no direct validation using independent hospital data |
| 3 | Akinwumi et al. (2025), *Evaluating machine learning models for stroke prediction based on clinical variables* | https://doi.org/10.3389/fneur.2025.1668420 | 5,110 records from the public Kaggle Stroke Prediction Dataset | Logistic Regression, Random Forest, Gradient Boosting, SVM and KNN; Random Oversampling | Logistic Regression achieved ROC-AUC 0.8362 and accuracy 95.11%; minority-class recall remained poor | No | Severe class imbalance, low sensitivity and underrepresentation of clinically diverse patient populations |
| 4 | Chun et al. (2021), *Stroke risk prediction using machine learning: a prospective cohort study of 0.5 million Chinese adults* | https://doi.org/10.1093/jamia/ocab068 | 503,842 adults from the China Kadoorie Biobank | Cox models, Random Survival Forest, Logistic Regression, SVM, Gradient Boosted Trees and MLP | Gradient Boosted Trees achieved AUROC approximately 0.83–0.84 and better calibration than conventional Cox models | No independent external validation established in the current report | Omission of atrial fibrillation, exclusion of right-censored data and need for external validation |
| 5 | Duan et al. (2025), *Development and validation of a stroke risk prediction model using regional healthcare big data and machine learning* | https://doi.org/10.1016/j.ijnss.2025.10.011 | 92,172 adults from the CHERRY regional electronic health record platform, China | Logistic Regression, Decision Tree, Random Forest, XGBoost and Back-propagation Neural Network | Random Forest achieved validation AUC 0.980, accuracy 0.919, precision 0.912, recall 0.929 and F1-score 0.921 | No external validation; internal validation only | Single-region dataset, reliance on SMOTE and limited explainability analysis |
| 6 | Yang et al. (2021), *Accurate Prediction of Stroke for Hypertensive Patients Based on Medical Big Data and Machine Learning Algorithms: Retrospective Study* | https://doi.org/10.2196/30277 | 57,671 hypertensive patients from the Shenzhen Health Information Big Data Platform | XGBoost, Random Forest, SVM and Logistic Regression using longitudinal clinical features | XGBoost achieved AUROC 0.9220, outperforming the other evaluated algorithms | No independent external validation established in the current report | Retrospective design, missing data, patient exclusion during screening and limited availability of laboratory markers |


### A3. Research gaps
| ID | Gap (1–2 sentences) | Evidence (# in A2) | How your project addresses it |

Most existing tabular stroke prediction studies rely on internal validation and do not establish whether their models generalize to independent populations or different clinical settings | #2, #3, #4, #5, #6 | Our project will clearly document the limitations of using a single public dataset and identify external and temporal validation as necessary future work.
### A4. PROBAST+AI appraisal of the most important paper in A2
### A4. PROBAST+AI appraisal of the most important paper in A2

**Paper#3: This study evaluates machine learning models using the same public Kaggle Stroke Prediction Dataset (5,110 records) as our project. It is particularly relevant because it investigates the limitations of standard evaluation metrics and class-imbalance handling when predicting rare stroke events.

| Domain | Risk of bias (low / high / unclear) | Justification (quote or page number in the paper) |

| Participants and data sources | High | The study uses a publicly available dataset containing 5,110 records, including only 249 stroke cases. The dataset has substantial class imbalance and limited information about its original population and data collection setting. | p9
| Predictors | Unclear | The study uses routinely available clinical and demographic variables. However, further verification of predictor measurement, missing-data handling and the availability of all predictors at the intended prediction time is required. | p9-10
| Outcome | Unclear | The target is a binary stroke label. However, the dataset documentation does not clearly establish whether the label represents a previous stroke or a future event, creating uncertainty about the prediction time and outcome definition. | p9-20
| Analysis | High | The dataset is severely imbalanced, and the reported results show poor minority-class sensitivity despite high overall accuracy. The study also highlights that balancing the dataset alone does not guarantee reliable detection of stroke cases. | p9-12

### Applicability to your team's problem:

This paper has high applicability because it uses the same dataset and clinical variables as our project. Its findings demonstrate why accuracy alone is insufficient for evaluating stroke prediction models. However, its limitations regarding class imbalance, sensitivity and generalizability must be considered. Our project addresses these issues by prioritizing sensitivity and PR-AUC, applying resampling only to training data, and planning to use SHAP for model interpretation.

## B. Results and timeline

### B1. Current results
| Logistic Regression | 80/20 split test, 1022 patients | Recall: 61.3% | Accuracy: 76.7% | https://github.com/daokhoi1106-lab/project/blob/main/Machine%20Learning |



### B2. Ablation (Milestone 3)
| Configuration (component removed / changed) | Main metric | Difference vs full model | Source |
|Random Forest with SMOTE (default parameters)|0.201|Reference configuration|https://github.com/daokhoi1106-lab/project/blob/main/Machine%20Learning|
|Tuned Random Forest with SMOTE (100 trees, max_features=2, bootstrap=True)|0.205|+0.004|https://github.com/daokhoi1106-lab/project/blob/main/Machine%20Learning|
|Tuned Logistic Regression with SMOTE (C=0.1, L2 penalty)|0.242|+0.041|Stroke_detection.ipynb, Cell 40|https://github.com/daokhoi1106-lab/project/blob/main/Machine%20Learning|


### B3. Comparison with the literature

Our project can be compared with previous studies using the Kaggle Stroke Prediction Dataset, particularly Dritsas and Trigka (2022) and Akinwumi et al. (2025).
Dritsas and Trigka reported an AUC of 0.989 using a stacking ensemble after applying SMOTE. However, their evaluation methodology raises concerns regarding potential data leakage if resampling was performed before cross-validation.
In contrast, Akinwumi et al. reported a ROC-AUC of approximately 0.836, while demonstrating that high accuracy does not necessarily indicate good sensitivity for the minority stroke class.
Our project aims to improve evaluation reliability by splitting the dataset before resampling and applying SMOTE only within training folds.

### B4. Timeline to completion

| Complete literature review and verify at least 10 research papers | 202414847 / 202414833 / 202414837 | Week3 | Week3 | Complete |
| Complete data exploration and preprocessing | 202414847 / 202414837 | Week6 | Week6 | Complete |
| Develop and evaluate baseline models | 202414833 / 202414847 | Week10 | Week10 | Complete |
| Complete proposed model and hyperparameter tuning | 202414833 / 202414837 | Week10 | Week10 | Complete |
| Conduct ablation experiments and model interpretation | 202414833 / 202414847 | Week10 | Week10 | Complete |
| Final evaluation, calibration and report preparation | All team members | Final – Week 15 | To be confirmed | Not yet verified |

### B5. Risks / blockers / questions for the instructor

- The dataset contains only 249 stroke cases among 5,110 records, resulting in severe class imbalance and potential instability in model evaluation.
- The original dataset does not clearly specify whether the stroke label represents a previous event or a future event, creating uncertainty about the intended prediction time.
- BMI contains 201 missing records, and missingness is associated with stroke status. Incorrect imputation may introduce bias.
- The dataset contains a large proportion of unknown smoking-status values, which may limit the reliability of this predictor.
- The use of a single public Kaggle dataset limits the generalizability of the proposed model to other populations, particularly Vietnamese patients.
- Further validation is needed to ensure that preprocessing, imputation, scaling and resampling are performed exclusively within training folds.
- Additional experiments are required to assess model calibration, sensitivity and the effect of individual preprocessing components.

## C. Self-assessment against the FAIR, TRIPOD+AI, PROBAST+AI appendix

### C1. FAIR — data

| Item | Answer | Evidence |
| Source, version, download date; checksum of the training file | Source: Kaggle Stroke Prediction Dataset. Dataset contains 5,110 records and 12 columns. Download date, exact version and file checksum have not yet been documented. | Original Kaggle CSV and preprocessing notebook |
| Licence / DUA; basis for being allowed to use the data | Kaggle dataset is restricted to educational purposes according to the current project report. The exact licence and applicable terms of use must be verified on the original dataset page. | Kaggle dataset page |
| Datasheet: population, inclusion/exclusion criteria, variable definitions and units, limitations | The dataset contains 5,110 records, 10 predictor variables and one binary stroke outcome, together with a patient ID. It includes demographic, lifestyle and clinical variables. The original population and collection period are not disclosed. | Dataset CSV and Section III.A of the project report |
| No patient identifiers | The ID column is excluded from model predictors. The dataset contains no documented direct patient identifiers, although the unique ID is retained for record tracking and overlap checks. | Preprocessing notebook and dataset inspection |

### C2. Reporting guideline
- **My research question:** Can machine learning models using routinely available demographic, lifestyle and clinical variables accurately identify individuals at increased risk of stroke while maintaining high sensitivity and reliable predictive performance?
- **Matching reporting guideline:** TRIPOD+AI, because our project develops and evaluates a machine learning-based prediction model using structured clinical and demographic data to estimate stroke risk.
- **Checklist items met / total; items still missing:** Not yet fully assessed. A completed TRIPOD+AI checklist is required. Remaining items include a clearly defined prediction time, outcome definition, complete model specification, calibration assessment, uncertainty estimates and validation details.
- **Outcome, label, prediction time T0, variables available at T0:** The outcome is a binary stroke label (1 = stroke, 0 = no stroke). The dataset contains 10 predictors: gender, age, hypertension, heart disease, ever married, work type, residence type, average glucose level, BMI and smoking status. The original dataset does not clearly specify whether the label represents a previous or future stroke event. Therefore, T0 and the availability of all predictors at T0 cannot yet be established. This limits interpretation of the model as a prospective risk prediction tool.

### C3. PROBAST+AI — self-appraisal of your project
| Domain | Risk of bias (low / high / unclear) | Evidence in the repo (file, line) | What you will do to reduce the risk |
| Participants and data sources | High | Stroke Prediction Dataset contains 5,110 records from a single public source, with limited information about the original population and data collection process. | Clearly document the dataset population and limitations, and acknowledge the need for external validation using independent clinical populations. |
| Predictors | High | BMI has 201 missing values, smoking status has 1,544 Unknown values, and some categorical predictors are strongly associated with age. | Perform imputation and encoding within training folds, add a BMI missingness indicator and assess predictor relevance and potential bias. |
| Outcome (watch for incorporation bias) | Unclear | The dataset contains a binary stroke label, but the original timing and definition of the outcome are not sufficiently documented. | Clarify the outcome definition and prediction time if possible. Explicitly acknowledge the limitation if the original documentation cannot establish temporal ordering. |
| Analysis (patient-level split, fit on train only, sample size, missing data) | High | The dataset contains only 249 positive cases. The existing report identifies preprocessing and model-selection leakage risks that still require correction. | Use stratified splitting, fit preprocessing within training folds, apply SMOTE only to training folds, use nested cross-validation or a separate validation set, and evaluate sensitivity, PR-AUC and calibration. |

**Applicability (population, setting where the model would be used):**
The proposed model is intended as a preliminary stroke risk-stratification tool using routinely available clinical and demographic variables. Its applicability is currently limited because the dataset's original population and collection setting are unknown, and the data may not represent older Vietnamese patients or other clinical populations. External validation using representative hospital or community healthcare data is necessary before clinical application.

### C4. Quick checklist (Appendix §7)
| Item | Met / Not yet | Evidence |
## C4. Project Quality and Reporting Checklist

| No. | Checklist item | Status | Evidence / Comments |
|---|---|---|---|
| 1 | Clearly define the prediction problem and intended use. | Completed | The project aims to predict stroke risk using routine clinical variables as a risk-stratification tool, not to diagnose acute stroke. |
| 2 | Describe the target population and dataset. | Completed | The Kaggle dataset contains 5,110 records and 10 predictor variables. However, 856 records belong to individuals under 18, while the intended population is adults. |
| 3 | Identify all predictors and the outcome. | Completed | Predictors include age, gender, hypertension, heart disease, marital status, work type, residence type, average glucose level, BMI, and smoking status. The outcome is a binary stroke label. |
| 4 | Examine data quality and missing values. | Completed | BMI contains 201 missing values (3.93%), and smoking status includes 1,544 records (30.2%) labelled as "Unknown". |
| 5 | Investigate class imbalance. | Completed | There are 4,861 non-stroke cases and 249 stroke cases. The positive class represents only 4.87% of the dataset. |
| 6 | Perform exploratory data analysis. | Completed | EDA examined feature distributions, correlations, and differences between stroke and non-stroke groups. Age showed the strongest association with stroke. |
| 7 | Split training and testing data before resampling. | Completed | An 80/20 train-test split was used, with SMOTE applied to the training data only. Stratification should be verified. |
| 8 | Prevent data leakage during preprocessing and validation. | Needs improvement | BMI imputation was performed before splitting in the current workflow. SMOTE was also applied before cross-validation, which may cause leakage between folds. |
| 9 | Compare multiple machine learning algorithms. | Completed | Logistic Regression, Random Forest, and SVM were evaluated. A stacking approach was also proposed in the project presentation. |
| 10 | Evaluate models using suitable metrics for imbalanced data. | Completed | Accuracy, recall, and F1-score were evaluated. PR-AUC, sensitivity at a fixed specificity, and calibration remain to be reported. |
| 11 | Select a model based on the clinical objective. | Completed | Tuned Logistic Regression was selected for its higher stroke recall (61.29%), despite lower accuracy (76.71%). |
| 12 | Explain model predictions using XAI techniques. | Partially completed | SHAP was included to examine feature contributions. LIME was introduced, but complete LIME results have not yet been demonstrated. |
| 13 | Perform external or temporal validation. | Not completed | Evaluation currently relies on the Kaggle dataset. No independent external dataset has been used. |
| 14 | Assess fairness across demographic groups. | Partially completed | Age and gender distributions were examined. Ethnicity and regional information are unavailable, limiting broader fairness assessment. |
| 15 | Provide sufficient information for reproducibility. | Partially completed | The dataset source, preprocessing methods, algorithms, and code repository are documented. Software versions, random seeds, and full evaluation settings still need further documentation. |
| 16 | Discuss limitations and avoid unsupported clinical claims. | Completed | The report acknowledges class imbalance, dataset limitations, potential data leakage, and the lack of external validation. The model is considered experimental rather than clinically validated. ||

## D. AI use declaration
| Tool | Used for which part | How the team verified the output |

| Claude | Drafting, organizing and condensing the project report based on the group's slides, research and notebook. | The group reviewed the generated content against the original slides, research papers and notebook results. |
| Consensus | Initial literature search and identification of relevant research papers. | The group checked paper titles, publication details, DOI links and reported findings against the original publications. |
| NotebookLM | Summarizing research papers and extracting relevant information for the literature review. | The group compared summaries with the original papers and verified reported numerical results. |
