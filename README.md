# yellowbrick -> matplotlib/sklearn plot comparison (issue #49)

`old/` = main (yellowbrick 1.5), `new/` = branch mnt/issue-49-replace-yellowbrick,
`side_by_side/` = OLD left | NEW right.

## How to read the comparison

The new plots are meant to look like the old ones. The table at the end lists
every plot that was rendered. A few pairs look different on purpose:

* **Threshold plot.** Both versions refit the model on 50 random splits and
  draw the median line with a shaded band. The random splits are not the same
  in the two versions, so the dashed "best threshold" line can sit at a slightly
  different x position.
* **Class prediction error.** The old plot had a bug: its bars were grouped by
  *predicted* class even though the x axis said "actual class", and the y axis
  was cut off so the tallest bar ran off the top. The new plot does what the
  axis label says: one bar per *actual* class, stacked by what the model
  predicted. The numbers are the same as in the confusion matrix.
* **Decision boundary.** The old code fit the scaler and PCA a second time on
  the test data, so the test points were drawn in a different coordinate system
  than the background. The new code reuses the transform fitted on the training
  data, so the points now line up with the regions.
* **Missing old images.** `cooks`, `distance`, and the hclust `silhouette` have
  no old image because yellowbrick crashed on them in this environment.
* **hclust elbow.** The circles in the old image are left over from the plot
  before it (`distance`), which crashed halfway. yellowbrick kept drawing into
  the same matplotlib axes, so the next plot landed on top of the leftovers.
  The new code creates and closes its own figure for every plot.

| experiment | plot | old | new |
|---|---|---|---|
| clf_iris_dt | AUC | yes | yes |
| clf_iris_dt | Class Report | yes | yes |
| clf_iris_dt | Confusion Matrix | yes | yes |
| clf_iris_dt | Decision Boundary | yes | yes |
| clf_iris_dt | Dimensions | yes | yes |
| clf_iris_dt | Learning Curve | yes | yes |
| clf_iris_dt | Precision Recall | yes | yes |
| clf_iris_dt | Prediction Error | yes | yes |
| clf_iris_dt | Validation Curve | yes | yes |
| clf_juice_lr | AUC | yes | yes |
| clf_juice_lr | Class Report | yes | yes |
| clf_juice_lr | Confusion Matrix | yes | yes |
| clf_juice_lr | Decision Boundary | yes | yes |
| clf_juice_lr | Dimensions | yes | yes |
| clf_juice_lr | Feature Selection | yes | yes |
| clf_juice_lr | Learning Curve | yes | yes |
| clf_juice_lr | Manifold Learning | yes | yes |
| clf_juice_lr | Precision Recall | yes | yes |
| clf_juice_lr | Prediction Error | yes | yes |
| clf_juice_lr | Threshold | yes | yes |
| clf_juice_lr | Validation Curve | yes | yes |
| clf_juice_rf | AUC | yes | yes |
| clf_juice_rf | Class Report | yes | yes |
| clf_juice_rf | Confusion Matrix | yes | yes |
| clf_juice_rf | Decision Boundary | yes | yes |
| clf_juice_rf | Dimensions | yes | yes |
| clf_juice_rf | Feature Selection | yes | yes |
| clf_juice_rf | Learning Curve | yes | yes |
| clf_juice_rf | Manifold Learning | yes | yes |
| clf_juice_rf | Precision Recall | yes | yes |
| clf_juice_rf | Prediction Error | yes | yes |
| clf_juice_rf | Threshold | yes | yes |
| clf_juice_rf | Validation Curve | yes | yes |
| clu_jewellery_hclust | Elbow Plot | yes | yes |
| clu_jewellery_hclust | Silhouette Plot | **missing** | yes |
| clu_jewellery_kmeans | Distance Plot | **missing** | yes |
| clu_jewellery_kmeans | Elbow Plot | yes | yes |
| clu_jewellery_kmeans | Silhouette Plot | yes | yes |
| reg_boston_lr | Cooks Distance | **missing** | yes |
| reg_boston_lr | Feature Selection | yes | yes |
| reg_boston_lr | Learning Curve | yes | yes |
| reg_boston_lr | Manifold Learning | yes | yes |
| reg_boston_lr | Prediction Error | yes | yes |
| reg_boston_lr | Residuals | yes | yes |
| reg_boston_rf | Cooks Distance | **missing** | yes |
| reg_boston_rf | Feature Selection | yes | yes |
| reg_boston_rf | Learning Curve | yes | yes |
| reg_boston_rf | Manifold Learning | yes | yes |
| reg_boston_rf | Prediction Error | yes | yes |
| reg_boston_rf | Residuals | yes | yes |
| reg_boston_rf | Validation Curve | yes | yes |
