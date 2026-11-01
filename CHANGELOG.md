# Changelog

All notable changes to this project are documented here.
The changelog is maintained from Mon 26 Oct 2026 onwards: every session or
commit that changes the repo must be recorded here.

## [1.0.0] - 2026-10-29

### Changed - Mon 26 Oct 2026 - @melgazar - commit: `ad8057a`

1. **Repo name** - renamed the repository to meet the naming requirement in
   the [Coursework Process Handbook (v1.1)](assets/docs/uni_materials/CWProcessHandbook-v1.1.pdf).

   - From: `F21DL_Group_13`
   - To: **[f21dl-2026-27-PG-group-13](https://github.com/elgazar24/f21dl-2026-27-PG-group-13)**
2. **Notebooks hierarchy** - restructured the
   [notebooks](src/notebooks) folder into topic-based folders:

   - `Data_Analysis`
   - `Data_Exploration`
   - `Feature_Engineering`
   - `Feature_Selection`
   - `Models`
3. **Models structure** - changed [Models](src/notebooks/Models) from one
   stand-alone notebook file per model to a folder with multiple files per
   model, to avoid spaghetti code and follow best practices and SOLID.

   - To be: `Decision_Tree`, `KNN`, `MLP`, `Naive_Bayes`
4. **Datasets structure** - changed [Datasets](assets/datasets) to four category dataset types
5. **Filled the Info Files for the Datasets in more organized and accurate way**

### Changed - Thu 29 Oct 2026 - @melgazar - commit: `ad8057a`

1. **configs/config.json** - rewrote as the single source for all notebooks:
   dataset folders and file paths (relative to `configs/`), target columns
   and classes, null symbols, the feature list of each dataset with its
   types, per-stage file slots, and `selected_features` per dataset. The
   used dataset is switched in one place.
2. **Data exploration** - rebuilt
   [1_Data_Exploration](src/notebooks/1_Data_Exploration) into three
   self-contained notebooks (`00_main` entry, `get_general_info`,
   `data_cleaning`) that read everything from the config and only show
   results; removed the old helper scripts.
3. **DS1 source repair** - the UCI csv header was missing the `pcv` column,
   which shifted every column after `hemo`; 15 rows carried stray tab
   characters and 3 rows were malformed. Repaired in place, so a plain
   `read_csv` loads 400 rows x 25 columns with the documented 250/150 class
   split. Regenerated `DS1_cleaned.csv` from the repaired source.
4. **Feature selection** - built
   [Feature_Selection](src/notebooks/Feature_Selection): `00_main` entry,
   `target_sanity_check` (labels vs core labs: DS1 labels clearly track
   them, DS2 labels do not), and `feature_selection` (mutual information +
   RF permutation importance, redundancy pruning, agreement ranking) which
   writes `selected_features` into the config per dataset (DS1: 12 of 24,
   DS2: 15 of 47, provisional).
5. **requirements.txt** - added `nbclient`, `nbconvert` and `nbformat` for
   headless notebook execution.
6. **.gitignore** - added `__pycache__/`.

## [1.1.0] - 2026-11-02

### Changed - Mon 2 Nov 2026 - @melgazar - commit: `5923352`

1. **DS3 unification** - merged the pre-split `Training_CKD_dataset.csv`
   (21,000 rows) and `Testing_CKD_dataset.csv` (4,800 rows) into a single
   `original_data/CKD_dataset.csv` (25,800 rows x 36 columns, zero
   duplicate rows across the old split), so DS3 is handled like every
   other dataset. Updated `configs/config.json`, regenerated DS3's
   `info.md` and `cleaned_data/DS3_cleaned.csv`, and corrected the dataset
   record count in `README.md`.
2. **DS3/DS4 reliability check** - ran the feature engineering pipeline on
   DS3 and DS4: DS3 labels track the labs reliably (correlations up to
   |0.98|, class separation 3.6-5.2), while DS4's labels carry no clinical
   signal (max correlation 0.10), like DS2.
3. **DS3 as the main dataset** - switched `main_dataset` to DS3 and ran the
   data exploration notebooks on it. Its cleaned data is placed in
   `processed_data/` as the current feature-engineering stand-in, then
   split stratified 80/20 into `final_data/DS3_train.csv` and
   `DS3_test.csv` (new `data_split.ipynb` in Feature_Selection). Feature
   selection now runs on the final training data only, so no information
   leaks from test to train, and writes DS3's `selected_features` into the
   config. Added `training.test_size` and `feature_selection.top_k` to the
   config.
4. **Random Forest model** - added
   [Models/random_forest/Random_Forest.ipynb](src/notebooks/Models/random_forest/Random_Forest.ipynb):
   trains on the main dataset's final training split with the config's
   selected features and evaluates on the held-out test split. DS3
   results: accuracy and macro F1 of 1.000 (out-of-bag 0.977), a purely
   diagonal confusion matrix, feature importances dominated by the
   kidney-function markers, and identical scores with all 35 features -
   consistent with DS3's constructed labels.
5. **Main dataset switched from DS3 to DS1** - DS3 was tried as the main
   dataset because its features correlate very strongly with the target
   (up to |0.98|). But when the Random Forest ran on it, it scored a
   perfect 100% on the test data, which raised a red flag: real medical
   data is never that clean. Looking deeper explained it simply - DS3's
   stage labels were not measured independently; they were built from a
   handful of lab features themselves (eGFR, serum creatinine, blood urea,
   albumin and the like), so the model is just reading back the formula
   that produced the labels, leaving nothing to discover. DS1's labels are
   real patient outcomes, so DS1 is now the main dataset and went through
   the whole pipeline again: exploration and cleaning, a processed copy, a
   stratified 80/20 split into `final_data/` (320 train / 80 test),
   feature selection on the training part only, and the Random Forest on
   the selected features (0.950 accuracy, 0.946 macro F1; all 24 features
   score 0.975 / 0.973 - the small-sample trade-off). The misplaced empty
   `random_forest/Decision_Tree.ipynb` stub was removed.
