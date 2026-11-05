# kNN on DS1: Conclusion

**Headline:** kNN with its own feature selection (15 features, k = 5, Manhattan distance, distance weights) reaches a repeated 5-fold macro F1 of 0.993 on the training set and classifies all 80 test patients correctly.

## Results

| Version | 5-fold macro F1 | Repeated 5-fold macro F1 | Test accuracy | Test macro F1 |
|---|---|---|---|---|
| Baseline (k = 5, all 30 features) | 0.977 | 0.974 | 0.988 | 0.987 |
| Tuned, all 30 features (k = 3, Euclidean) | 0.980 | 0.976 | 1.000 | 1.000 |
| **Tuned, own feature selection (final)** | **0.997** | **0.993** | **1.000** | **1.000** |
| Tuned, selection + hierarchical cluster | 0.993 | 0.988 | 1.000 | 1.000 |

Input is only the preprocessed train/test split (320/80 patients, 30 features). Every choice was made with cross-validation on the training set; the test set was used once, at the end.

## Final model and why

- The final model keeps 15 of the 30 features, ranked with the ANOVA F-test inside each fold, then uses k = 5, Manhattan distance and distance weights.
- It has the highest score and the smallest spread in repeated cross-validation (0.993, std 0.012), so the choice does not rest on one lucky split.
- The test set cannot separate the tuned versions (all 1.000), which is why the choice was made on repeated cross-validation.

## What each step showed

- **Tuning:** with all 30 features, every setting scores between 0.958 and 0.980, so k, weights and distance matter little on their own.
- **Feature selection:** the biggest gain. Every feature count from 5 to 25 beats all 30 features, because features that do not help add noise to the distance. The kept features are the kidney markers (creatinine and its engineered versions, specific gravity, albumin), blood markers (hemoglobin, packed cell volume, red cell count, sodium), the comorbidity and urine scores, and hypertension, diabetes and appetite.
- **Clustering:** the hierarchical cluster is kept by the feature ranking, so it does separate the classes, but it lowers the score slightly (0.988 vs 0.993 in repeated cross-validation). It mostly repeats what the kidney and blood markers already show.

## Errors

- Out of fold, the final model gets 319 of 320 training patients right.
- The one error is a CKD patient predicted as not CKD, with a CKD probability of 0.38, so the vote was close.
- This patient is in the hierarchical cluster where only 22% of patients have CKD, so clustering also places them with the healthy patients. Clustering does not improve kNN, but it helps explain its error.

## Limitations

- With 80 test patients, one error moves accuracy by 0.0125, so a perfect test score is a weak signal on its own; repeated cross-validation is the better guide.
- Results come from one train/test split of a small dataset (400 patients).
- Missing values were filled during preprocessing, so patients with many gaps look more like the typical patient than they really are.
- A missed CKD patient is the costly error in screening, and the one out-of-fold error is of this kind.
