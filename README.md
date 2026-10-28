<h1 align="center">Glass Bottle Inspection</h1>
<p align="center"><strong>MACHINE VISION | CLASSIFICATION | AUTOMATION</strong></p>
<p align="center"><a href="https://github.com/Kaveesha229">Kaveesha Gunawardena | Engineering portfolio</a></p>

## Overview

Final year project work on automated glass bottle inspection. This repository currently documents image patch classification into good and crack classes, with training notebooks, saved experiment outputs and test samples.

## Body crack evaluation

Four model reports are now collected in the body crack section, including HOG with SVM. The collection follows the project owner's identification of the uploaded reports and preserves their original run identifiers.

<p><a href="body_crack/README.md"><strong>Explore body crack results and reports</strong></a> &nbsp; | &nbsp; <a href="body_crack/results/test_metrics.csv">Download test metrics CSV</a></p>

<table>
<tr><th>Model</th><th>Test accuracy</th><th>Crack precision</th><th>Crack recall</th><th>Crack F1</th></tr>
<tr><td>HOG with Logistic Regression</td><td>95.00%</td><td>87.50%</td><td>87.50%</td><td>0.8750</td></tr>
<tr><td>HOG with SVM</td><td>95.00%</td><td>87.50%</td><td>87.50%</td><td>0.8750</td></tr>
<tr><td>HOG with Random Forest</td><td>90.00%</td><td>75.00%</td><td>75.00%</td><td>0.7500</td></tr>
<tr><td>ResNet18</td><td>100.00%</td><td>100.00%</td><td>100.00%</td><td>1.0000</td></tr>
</table>

Results are taken from the supplied reports, each evaluated on 40 test patches comprising 32 good and 8 crack patches. These are patch classification results, not whole bottle inspection accuracy. The update adds report evidence rather than a new training run.

## Repository guide

<table>
<tr><th>File or folder</th><th>Purpose</th></tr>
<tr><td><a href="notebooks/LogisticRegression.ipynb">notebooks/LogisticRegression.ipynb</a></td><td>Readable notebook copy for the Logistic Regression experiment</td></tr>
<tr><td><a href="notebooks/RandomForest.ipynb">notebooks/RandomForest.ipynb</a></td><td>Readable notebook copy for the Random Forest experiment</td></tr>
<tr><td><a href="notebooks/ResNet18.ipynb">notebooks/ResNet18.ipynb</a></td><td>Readable notebook copy for the ResNet18 experiment</td></tr>
<tr><td><a href="https://github.com/Kaveesha229/Design%2DDevelopment%2Dof%2DVision%2DBased%2DBottle%2Dtype%2DCrack%2Didentification%2Dand%2Drejection%2Dfor%2DGlass%2Dbottles/tree/main/hog%20%2B%20logistic%20regression/20261003_153422">hog + logistic regression/20261003_153422</a></td><td>Saved Logistic Regression run</td></tr>
<tr><td><a href="https://github.com/Kaveesha229/Design%2DDevelopment%2Dof%2DVision%2DBased%2DBottle%2Dtype%2DCrack%2Didentification%2Dand%2Drejection%2Dfor%2DGlass%2Dbottles/tree/main/hog%20%2B%20random%20forest/20261003_155012">hog + random forest/20261003_155012</a></td><td>Saved Random Forest run</td></tr>
<tr><td><a href="https://github.com/Kaveesha229/Design%2DDevelopment%2Dof%2DVision%2DBased%2DBottle%2Dtype%2DCrack%2Didentification%2Dand%2Drejection%2Dfor%2DGlass%2Dbottles/tree/main/resnet18/20261003_155746">resnet18/20261003_155746</a></td><td>Saved ResNet18 run</td></tr>
<tr><td><a href="https://github.com/Kaveesha229/Design%2DDevelopment%2Dof%2DVision%2DBased%2DBottle%2Dtype%2DCrack%2Didentification%2Dand%2Drejection%2Dfor%2DGlass%2Dbottles/tree/main/test">test</a></td><td>Included test image patches</td></tr>
</table>

## Current scope

The repository contains notebooks and saved outputs for HOG with Logistic Regression, HOG with Random Forest and ResNet18. A HOG with SVM evaluation report is now available under `body_crack`; its source notebook and trained model have not been supplied. Bottle type recognition, conveyor integration and physical rejection are broader project goals rather than demonstrated capabilities of these classification files.

## Processing approach

The HOG experiments resize grayscale patches to 128 by 128 pixels before feature extraction and classification. ResNet18 uses RGB patches resized to 224 by 224 pixels. Both classes are mapped consistently: `good` is 0 and `crack` is 1.

## Reading the results

The <a href="body_crack/README.md">body crack evaluation</a> provides all four model results, confusion counts, model configurations, runtime context and links to the original reports. The existing experiment folders remain available as the original records. Logistic Regression and Random Forest reports in the new collection are byte identical to the existing PDFs.

The recorded training and validation counts are 385 and 119 respectively. Exact image duplicate checks do not verify physical bottle separation. A perfect score on 40 test patches does not establish performance on unseen production bottles.

## Getting started

1. Open a notebook from `notebooks` in Google Colab. These copies retain the original code cells while removing saved outputs and personal execution metadata.
2. Review the notebook setup cell, install its dependencies and follow any restart instruction.
3. Supply the complete dataset in `train`, `valid` and `test` directories, each containing `good` and `crack` folders.
4. Update `DATASET_ROOT` and `OUTPUT_ROOT` to your own working locations. The original notebooks use a Google Drive folder named `bottlecrackml`.
5. Run the cells in order. For ResNet18, a GPU runtime is useful.
6. Inspect the generated configuration, predictions and metrics before comparing runs.

## Reproducibility notes

The repository includes 40 test patches, but the complete training and validation images are not present. The root `train` entry is a small file rather than a dataset directory. The two HOG runs include saved `.joblib` models. A ResNet18 weights file is not present in the inspected tree. Full reproduction therefore requires the missing dataset and a new ResNet18 training run or the original weights.

## Software

The notebooks use Python, NumPy, pandas, Pillow, Matplotlib, joblib, scikit learn, scikit image and ReportLab as applicable. The neural network experiment additionally uses PyTorch and torchvision. Saved `configuration.json` files record selected settings and some package versions.

## Next engineering steps

Expand evaluation across bottle types and lighting conditions, verify inference latency on the deployment hardware, and document the connection between classification output and physical rejection. Add individual project responsibilities and hardware results from the original records.

## Project media

Photos and demonstration videos will be added here as the project presentation is updated.

<p align="center"><sub>Practical engineering through building, testing and refinement.</sub></p>
