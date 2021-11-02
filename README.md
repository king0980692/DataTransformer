# encoderder

Encode the csv-like file to sparse format for FM auxiliary feature input.


Factorization machine using the libsvm for input, and for experiment more conveniently, this repo is created !

## Sparse format for FM

![](https://i.imgur.com/qDhSPV5.png)
(ref:https://towardsdatascience.com/factorization-machines-for-item-recommendation-with-implicit-feedback-data-5655a7c749db)

As you can see the FM's input for user and item using the One-Hot encode to generate a huge sparse matrix . The scikit-learn [OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html) can't afford this kind task.

Furthermore, we also want to add the short-text feature or other auxiliary feature into FM, and those feature can be all kinds of type, e.g. categorical data, numerical data, we want to encode them all, so develope this tool is necessary !


## Usage

```bash
python3 encoderder.py -c [config]
```

## Config
encoderder support json config format, which look like : 

```json=
{
    "train": {
        "input": "./ml.csv",
        "output": "./train.txt",
        "cached": true,
        "seperator": ",",
        "header": true,
        "sparse": true,
        "target_columns": [
            {
                "index": 0,
                "type": "cat"
            },
            {
                "index": 1,
                "type": "cat"
            },
            {
                "index": 2,
                "type": "truth"
            }
        ]
    }
}
```

#### Config attributes


##### INPUT/OUTPUT:
* input : input file
* output : output file for sparse format

##### TARGET COLUMNS:
* target column : the intersted column you want to encode, support some kinds of feature type
    * cat : (categorical data)
    * num : (numerical data)
    * truth : (labled data)

##### OTHER CONFIG
* cache : turn it on to will cached some data in memory, which cost more memory
* seperator : the symbol seperate the columns 
* header : skip first line if the dataset contains the header
* sparse : turn it on to generate the scipy's coo matrix in npz format output
