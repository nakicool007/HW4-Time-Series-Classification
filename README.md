# Homework 4 - Time Series Classification

**Name:** Nakul Kumbria  
**GitHub:** nakicool007

I used the AReM dataset to study time series classification. The notebook includes the feature extraction from Question 1 and my work on Question 2(a)(i) through (iv), comparing bending with the other activities.

## Current work

- Extract minimum, maximum, mean, median, sample standard deviation, and quartiles from the six sensor series.
- Calculate standard deviations and 90% bootstrap confidence intervals for the features.
- Plot mean, standard deviation, and maximum from series 1, 2, and 6 using only the training instances.
- Split each series into two halves, extract the features again, and compare the scatter plots with the whole-series results.
- Adapt the professor's RFE example to unregularized logistic regression and use stratified 5-fold cross-validation to choose the number of segments and retained features.
- Report the selected model's training confusion matrix, ROC, AUC, coefficients, and p-value limitations under complete separation.

For Question 2(a)(iii), I compared all 8,820 pairs of segment and feature counts using mean balanced accuracy. The selected pair is **(l, p) = (1, 10)**, with 99.17% mean CV balanced accuracy and 98.57% mean CV ordinary accuracy. These are model-selection scores; the 19 test instances were kept out of the search.

For Question 2(a)(iv), the selected model correctly classifies all 60 other-activity and 9 bending training instances, with training AUC 1.00. The training classes are completely separable. I report the stopped-fit coefficients and numerical Wald diagnostics, but conventional MLE p-values are unavailable in this case. These training results are not a test-set evaluation.

## Files

- `notebook/Kumbria_Nakul_HW4.ipynb`: code, saved plots, and written answers.
- `data/AReM/`: original dataset.
- `data/train/` and `data/test/`: activity folders containing the assignment's training and test splits.
- `data/processed/`: extracted features, instance metadata, bootstrap results, training features from the two halves, RFE results, and the training predictions and coefficient report.
- `figures/`: saved scatterplot matrices, the cross-validation model-selection plot, and the training confusion matrix and ROC for Question 2(a).
- `requirements.txt`: Python dependencies.

## Dataset and split

There are 88 instances across seven activities. I used datasets 1 and 2 from bending1 and bending2 for testing, and datasets 1, 2, and 3 from each other activity for testing. This leaves **69 training instances and 19 test instances**.

For the binary plots, I grouped bending1 and bending2 together, giving 9 bending and 60 other training instances. The plots do not use the test instances.

Most instances have 480 observations. `sitting/dataset8.csv` has 479, so I kept the original observations. When splitting this instance, I used 239 observations in the first half and 240 in the second half.

## Running the notebook

Use Python 3.11 or newer. From this folder, run:

```powershell
python -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m jupyterlab
```

Open `notebook/Kumbria_Nakul_HW4.ipynb` and run the cells in order. The bootstrap uses 10,000 repetitions with seed 42 and may take some time. The RFE search checks all feature counts for l=1 through 20 and uses five worker processes. The notebook supports launching Jupyter from either the repository root or the notebook folder.

## Dataset source

Palumbo, F., Gallicchio, C., Pucci, R., & Micheli, A. (2016). *Activity Recognition system based on Multisensor data fusion (AReM)* [Dataset]. UCI Machine Learning Repository. [DOI: 10.24432/C5SS33](https://doi.org/10.24432/C5SS33).

The dataset is available on the [UCI AReM page](https://archive.ics.uci.edu/dataset/366/activity+recognition+system+based+on+multisensor+data+fusion) under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
