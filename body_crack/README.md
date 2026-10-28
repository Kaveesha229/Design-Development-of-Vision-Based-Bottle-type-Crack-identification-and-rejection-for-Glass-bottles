<h1 align="center">Body Crack Classification</h1>
<p align="center"><strong>GLASS BOTTLE INSPECTION | MODEL EVALUATION</strong></p>
<p align="center"><a href="../README.md">Project overview</a> &nbsp; | &nbsp; <a href="results/test_metrics.csv">Test metrics CSV</a></p>

## Overview

Four evaluation reports document classification of image patches as good or crack. This collection is labelled body crack following the project owner's identification of the uploaded files. The reports themselves use the general title bottle crack patch classification.

This update organises existing experiment evidence. It does not represent retraining, a new dataset release or a new test run.

## Evaluation reports

<table>
<tr><th>Model</th><th>Report</th><th>Original run</th></tr>
<tr><td>HOG with Logistic Regression</td><td><a href="reports/HOG_Logistic_Regression_Report.pdf">View PDF</a></td><td>20261003_153422</td></tr>
<tr><td>HOG with SVM</td><td><a href="reports/HOG_SVM_Report.pdf">View PDF</a></td><td>20261003_154339</td></tr>
<tr><td>HOG with Random Forest</td><td><a href="reports/HOG_Random_Forest_Report.pdf">View PDF</a></td><td>20261003_155012</td></tr>
<tr><td>ResNet18</td><td><a href="reports/ResNet18_Report.pdf">View PDF</a></td><td>20261003_155746</td></tr>
</table>

Each original PDF is preserved without modification. Reports contain the dataset split, model settings, validation selection procedure, evaluation metrics and diagnostic figures.

## Dataset and labels

<table>
<tr><th>Split</th><th>Good patches</th><th>Crack patches</th><th>Total</th></tr>
<tr><td>Training</td><td>315</td><td>70</td><td>385</td></tr>
<tr><td>Validation</td><td>105</td><td>14</td><td>119</td></tr>
<tr><td>Test</td><td>32</td><td>8</td><td>40</td></tr>
<tr><td>All splits</td><td>452</td><td>92</td><td>544</td></tr>
</table>

The class labels are `good = 0` and `crack = 1`. All four reports retain the existing split assignments and state that exact duplicate image pixels across splits were checked. That check does not establish separation of physical bottles or capture sessions.

## Recorded test performance

<table>
<tr><th>Model</th><th>Test accuracy</th><th>Crack precision</th><th>Crack recall</th><th>Crack F1</th></tr>
<tr><td>HOG with Logistic Regression</td><td>95.00%</td><td>87.50%</td><td>87.50%</td><td>0.8750</td></tr>
<tr><td>HOG with SVM</td><td>95.00%</td><td>87.50%</td><td>87.50%</td><td>0.8750</td></tr>
<tr><td>HOG with Random Forest</td><td>90.00%</td><td>75.00%</td><td>75.00%</td><td>0.7500</td></tr>
<tr><td>ResNet18</td><td>100.00%</td><td>100.00%</td><td>100.00%</td><td>1.0000</td></tr>
</table>

<table>
<tr><th>Model</th><th>Balanced accuracy</th><th>ROC AUC</th><th>Average precision</th></tr>
<tr><td>HOG with Logistic Regression</td><td>92.19%</td><td>0.9922</td><td>0.9705</td></tr>
<tr><td>HOG with SVM</td><td>92.19%</td><td>0.9922</td><td>0.9705</td></tr>
<tr><td>HOG with Random Forest</td><td>84.38%</td><td>0.9727</td><td>0.8979</td></tr>
<tr><td>ResNet18</td><td>100.00%</td><td>1.0000</td><td>1.0000</td></tr>
</table>

Values are transcribed from page 2 of each report. They are reported patch classification results, not a fresh evaluation. Precision and recall refer to the crack class.

## Confusion counts

<table>
<tr><th>Model</th><th>TP</th><th>TN</th><th>FP</th><th>FN</th></tr>
<tr><td>HOG with Logistic Regression</td><td>7</td><td>31</td><td>1</td><td>1</td></tr>
<tr><td>HOG with SVM</td><td>7</td><td>31</td><td>1</td><td>1</td></tr>
<tr><td>HOG with Random Forest</td><td>6</td><td>30</td><td>2</td><td>2</td></tr>
<tr><td>ResNet18</td><td>8</td><td>32</td><td>0</td><td>0</td></tr>
</table>

TP means a crack patch correctly detected. TN means a good patch correctly accepted. FP means a good patch classified as crack. FN means a crack patch missed.

ResNet18 correctly classified all 40 test patches in its recorded run. Logistic Regression and SVM each missed one crack patch and rejected one good patch. Random Forest missed two crack patches and rejected two good patches. With only eight crack patches in the test split, one missed crack changes recall by 12.5 percentage points.

## Model configurations

<table>
<tr><th>Model</th><th>Input and features</th><th>Selection details</th></tr>
<tr><td>HOG with Logistic Regression</td><td>Grayscale, 128 by 128 pixels, 8100 HOG features and StandardScaler</td><td>C 0.01, no class weighting, probability threshold 0.40</td></tr>
<tr><td>HOG with SVM</td><td>Grayscale, 128 by 128 pixels, 8100 HOG features and StandardScaler</td><td>Linear kernel, C 0.01, 136 support vectors, decision score threshold minus 0.006273</td></tr>
<tr><td>HOG with Random Forest</td><td>Grayscale, 128 by 128 pixels, 8100 HOG features without scaling</td><td>200 trees, balanced class weighting, minimum leaf size 1, probability threshold 0.29</td></tr>
<tr><td>ResNet18</td><td>RGB, 224 by 224 pixels, ImageNet pretrained features and horizontal flip augmentation</td><td>All layers fine tuned with AdamW, best epoch 20 of 35 completed, probability threshold 0.50</td></tr>
</table>

The HOG models were fitted on training data, with model settings and thresholds chosen using validation crack F1. ResNet18 selected its checkpoint using validation loss and then its threshold using validation crack F1. The reports state that test data were not used for selection.

The SVM threshold applies to a decision score, not a probability. ResNet18 uses pretraining, a larger RGB input and augmentation, so the comparison is not a controlled change of classifier alone.

## Reported runtime and model size

<table>
<tr><th>Model</th><th>Tuning or training time in seconds</th><th>Mean patch pipeline time in ms</th><th>Model size in MB</th></tr>
<tr><td>HOG with Logistic Regression</td><td>6.81</td><td>10.37</td><td>0.25</td></tr>
<tr><td>HOG with SVM</td><td>10.12</td><td>19.70</td><td>8.60</td></tr>
<tr><td>HOG with Random Forest</td><td>32.31</td><td>57.77</td><td>0.61</td></tr>
<tr><td>ResNet18</td><td>135.45</td><td>10.52</td><td>42.71</td></tr>
</table>

Times come from page 2 of each report. HOG times describe tuning; the ResNet18 time describes training. Pipeline timing includes image reading, preprocessing and prediction, plus feature extraction and scaling where applicable. Warmup is excluded. ResNet18 reports a Tesla T4 GPU. Hardware and storage access affect these values, so they should not be treated as a controlled hardware benchmark or conveyor throughput.

## Available materials

The four PDFs and a CSV transcription of their test metrics are included here. Existing notebooks, HOG model files and test samples remain in their original locations in the repository.

The supplied update does not contain a raw body image dataset, an SVM notebook or model file, or ResNet18 weights. The matching run identifiers and identical Logistic Regression and Random Forest PDF contents connect this collection to the existing experiment records; they do not establish a separate new dataset.

## Interpretation and next evaluation

The recorded results favour ResNet18 on this small test split. A production decision still needs evaluation on unseen physical bottles, varied lighting, additional crack appearances and the complete scanning and rejection pipeline. Patch accuracy alone does not establish whole bottle inspection performance.

## Project media

Body inspection photographs and demonstration videos can be added here when available.

<p align="center"><sub>Practical engineering through building, testing and refinement.</sub></p>
