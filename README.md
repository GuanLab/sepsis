# Sepsis
## Top-performing algorithm for DII National Data Science Challenge

## Installation

Clone this program to your local directory: 
``` r
git clone https://github.com/GuanLab/sepsis.git
```
## Dependency

* [python (3.7.4)](https://www.python.org/)
* [numpy (1.17.2)](https://numpy.org/)
* [pandas (0.25.1)](https://pandas.pydata.org/)
* [LightGBM (3.1.1)](https://pypi.org/project/lightgbm/)
* [scikit-learn (0.19.0)](https://scikit-learn.org/stable/) 
* [shap (0.38.1)](https://pypi.org/project/shap/)

For visualization:
* [boken (2.3.0)](https://docs.bokeh.org/en/latest/docs/first_steps/installation.html)

## Input data format

The example data in the data/ are randomly generated data for the demonstration of the algorithm.

Two types of data is requied for model training and prediction:
* `gs.file`: `.txt` file two columns. The first column is file name index. The second column is the gold standard (0/1), representing the final outbreak of sepsis

``` 
0.psv,1
1.psv,1
2.psv,0
3.psv,1
4.psv,0
5.psv,1
6.psv,1
``` 

* `*.psv`: `.psv` table files separated by `|`, which is the time-series feature records.
	The header of psv file are the feature names. To note, the first column is the time index.

``` 
HR|feature_1|feature_2|...|feature_n-1|feature_n
0.0|1|0.0|...|1.3|0.0 
1.0|NaN|0.0|...|0.0|0.0
3.5|NaN|2.3|...|0.0|0.0
```
## Model training and cross validation
``` r
python main.py -g [GS_FILE_PATH] -t [LAST_N_RECORDS] -f [EXTRA_FEATURES] --shap
```

* `GS_FILE_PATH`: the path to the gold-standard file; for example, `/data/gs.file`;
* `LAST_N_RECORDS`: last n records to use for prediction. default: 16;
* `EXTRA_FEATURES`: addtional features used for prediction. default: ['norm', 'std', 'missing_portion', 'baseline'], which are all features we used in DII Data challenge.

also use

```r
 python main.py --help
```
to get instructions on the usage of our program.


This will generate models, which will be saved under a new directory `./models`.

Evaluation results during five-fold cross validation will be stored in `eva.tsv`.


# Top feature evaluation

if `--shap` is indicated, SHAP analysis will be carried out to show top contributing measurements and last nth time points. This will generate an html report (`top_feature_report.html`) like the following:

<p align="center">
<img width="800", src ="https://github.com/GuanLab/sepsis/blob/master/top_feature_report_example.png">
</p>

The corresponding shap values will be stored in `shap_group_by_measurment.csv` and `shap_group_by_timeslot.csv`.

## Other applications of this method

This method can be generalized to be used on other hospitalization data. One application of this method is the [COVID-19 DREAM Challenge](https://www.synapse.org/#!Synapse:syn21849255/wiki/602411), where this method also achieves top performance.

## Reference
* For citation, please refer to our latest iScience paper: [Assessment of the timeliness and robustness for predicting adult sepsis](https://www.sciencedirect.com/science/article/pii/S2589004221000742).
* For protocol(TBD)
