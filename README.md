# sepsis
## Top-performing algorithm for DII National Data Science Challenge

## Installation

## dependency

* [@python (3.6.5)](https://www.python.org/)
* [@numpy (1.13.3)](https://numpy.org/)
* [@pandas](https://pandas.pydata.org/)
* [@LightGBM(3.1.1)](https://pypi.org/project/lightgbm/)
* [@scikit-learn (0.19.0)](https://scikit-learn.org/stable/) 

## Input data format

The example data in the data/ are randomly generated data for the demonstration of the algorithm.

Two types of data is requied for model training and prediction:
`gs.file`: `.txt` file two columns. The first column if file name index. The second column is the gold standard (0/1), representing the final outbreak of sepsis

``` r
0.psv,1
1.psv,1
2.psv,0
3.psv,1
4.psv,0
5.psv,1
6.psv,1
``` 

`*.psv`: `.psv` table file separated by '|', which is the time-series feature records.
	The header of psv file are the feature names. To note, the first column is the time index.

``` r
HR feature_1 featuyre_2 ... feature_n-1 feature_n
0.0 1 0.0 ... 1.3 0.0 
1.0 NaN 0.0 ... 0.0 0.0
3.5 NaN 2.3 ... 0.0 0.0
```
## model training and cross validation
``` r
python main.py -g [PATH]
```
This will generate models, which will be saved under a new directory `./models`



