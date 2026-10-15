Cancer Variant Prioritization Using Machine Learning
An exploratory machine learning project that investigates whether genomic variant annotations can predict clinical significance. The notebook compares a Random Forest with XGBoost, experiments with feature engineering, and uses baseline and information-theoretic diagnostics to understand the results.
Key finding: All trained models achieved approximately 25% test accuracy on four nearly balanced classes—close to chance-level performance. This is a useful negative result: the provided dataset and features did not yield a reliable predictive signal in these experiments. Do not use these models for medical or clinical decisions.


Project objectives
- Explore a cancer variant dataset and its clinical-significance labels.
- Visualize relationships among variant types, population allele frequency, CADD scores, and labels.
- Train and evaluate multiclass classification models.
- Investigate whether feature engineering improves prediction.
- Benchmark predictive performance against a simple baseline and examine feature–target associations.
Dataset
The notebook loads cancer_variant_prioritization_dataset (1).csv, which must be provided separately. It contains 10,000 records and 9 columns, with no missing values in the notebook's initial inspection.
Column	Description
Chromosome	Chromosome identifier
Position	Genomic position
Gene	Gene name
Variant_Type	Type of genetic variant
Population_AF	Population allele frequency
CADD_Score	CADD annotation score
SIFT	SIFT annotation category
PolyPhen	PolyPhen annotation category
Clinical_Significance	Target label


Target classes and counts:
Class	Records
Likely_pathogenic	2,543
VUS (variant of uncertain significance)	2,534
Benign	2,495
Pathogenic	2,428


The notebook does not establish the dataset's provenance or independent clinical validity. Check its origin, licensing, annotation quality, and potential simulation or sampling procedures before drawing biological conclusions.
Workflow
1. Explore data: Check structure, missingness, and target distribution.
2. Visualize: Use Seaborn and Plotly for target counts, CADD score versus allele frequency, variant-type distributions, and CADD score box plots.
3. Preprocess: Encode categorical columns and target labels with LabelEncoder.
4. Train models: Make a stratified 80/20 train/test split (random_state=42); evaluate Random Forest and XGBoost.
5. Engineer features: Experiment with numeric SIFT/PolyPhen mappings, variant-type indicators, gene-frequency information, and a derived pathogenicity index.
6. Diagnose signal: Compare models with a stratified Dummy Classifier, estimate mutual information, and inspect model feature importances.
Results
These are the recorded outputs of the supplied notebook, not newly rerun or externally validated results.
Method	Test accuracy
Stratified Dummy Classifier	24.25%
Random Forest (100 trees)	24.95%
XGBoost	25.40%
Feature-engineered / optimized XGBoost	24.60%


For four approximately balanced classes, an uninformed prediction strategy is expected to attain about 25% accuracy. The models did not meaningfully surpass this level. Mutual-information estimates were very small for all investigated features; several were estimated as zero. This suggests little detectable predictive association in this dataset under the tested methods, not proof that these biological annotations are universally unrelated to clinical significance.
Interpretation: Greater model complexity and engineered features did not improve performance. The most important result is the diagnostic finding, rather than an effective clinical-significance classifier.
Run the notebook
Requirements
- Python 3
- Jupyter Notebook or Google Colab
- pandas, numpy, matplotlib, seaborn, scikit-learn, plotly, xgboost
Install packages locally:
python -m pip install pandas numpy matplotlib seaborn scikit-learn plotly xgboost notebook
1. Open Untitled0.ipynb from this repository, or use the Open in Colab button above.
2. Obtain the dataset and place cancer_variant_prioritization_dataset (1).csv in the notebook's accessible filesystem.
3. Update the pd.read_csv(...) path in the notebook. The saved notebook currently uses an absolute path:
   df_variant = pd.read_csv('/cancer_variant_prioritization_dataset (1).csv')
   For a local copy in the same directory, change it to:
   df_variant = pd.read_csv('cancer_variant_prioritization_dataset (1).csv')
4. Run the cells in order. Some preprocessing, training, and diagnostic cells are repeated in the original notebook; these repetitions are not required to understand the results.
Repository layout
Cancer-Variant-Dataset-for-Machine-Learning/
├── README.md
├── Untitled0.ipynb
└── cancer_variant_prioritization_dataset (1).csv  # Add separately if distribution is permitted
Limitations and next steps
- Clinical validity: The data's source and labeling procedure are not documented in the notebook; validate them before scientific use.
- Predictive utility: Current accuracy is near the random baseline. The notebook does not establish a clinically useful model.
- Evaluation: Use cross-validation, uncertainty intervals, and external datasets to test whether any improvement is reproducible.
- Encoding: Label encoding of nominal predictors introduces arbitrary numeric orderings; consider one-hot encoding or suitable categorical methods.
- Data leakage: Fit feature preprocessing and engineered feature statistics on training data only in a reproducible pipeline.
- Biological context: Consider richer, independently verified variant annotations and clinically reviewed labels if the goal is real-world prioritization.
Technologies
Python · Pandas · NumPy · Scikit-learn · XGBoost · Matplotlib · Seaborn · Plotly · Google Colab
Author
Blessing Sekeramavi
GitHub: BlessingSK1998
Disclaimer
This is an educational/research exploration, not a validated clinical tool. Its outputs should not guide diagnosis, genetic counseling, treatment, or variant classification in practice.
