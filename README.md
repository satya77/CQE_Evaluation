# CQE Evaluation 
A Framework for Comprehensive Quantity Extraction. This repository contains evaluation code for the paper:

[CQE: A Framework for Comprehensive Quantity Extraction
]()
 
Satya Almasian*, Vivian Kazakova*, Philipp Göldner, Michael Gertz  
Institute of Computer Science, Heidelberg University  
(`*` indicates equal contribution)

### Prerequisites
Make sure you have Python 3.9 and spaCy 3.0.9 installed. 
Visit the [CQE](https://github.com/vivkaz/CQE) repository for instruction to install CEQ. 
You also need to install some python packages. Run
```
pip install -r requirements.txt
```

### File and folder structure
To replicated the results from the paper and significance testing, use the following scripts.
Significance testing scripts are under `significance_testing` package.
The computed results are also present under `data/evaluation_output`.

| File                                                                                                    | Description                                                                                                                 |
|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| [gpt-3/gpt3-tag.py](gpt-3/gpt3-tag.py)                                              | Uses open ai API to tag the test set.                                                                                       |
| [tagger.py](tagger.py)                                                             | Creates a unified representation for different models, by adding normalization and text cleaning to prepare for evaluation. |
| [evaluate_models.py](evaluate_models.py)                                           | Evaluation script for CQE and other baselines                                                                               |
| [test_unit_classifier.py](test_unit_classifier.py)                                | Evaluation code for unit disambiguator                                                                                      |                                        |
| [significance_test/significance_test.py](evaluation/significance_test.py)                                      | Computing P values based on the F1 scores for different systems.                                                            |
| [significance_test/permutation_significance_test.py](significance_test/permutation_significance_test.py)              | Code for permutation based significance testing for the specific output of CQE                                              |                       |
| [significance_test/significance_testing_for_arrary_input.py](significance_test/significance_testing_for_arrary_input.py) | Code for permutation based significance testing for normal  array input, used for the classification of unit disambiguator  |                                        |


### Data
The evaluation data can be found in `/data/formatted_test_set` and consists of 5 evaluation sets. 

| Dataset                                         | #Sentences | #Quantities | Source                                                                                                                                                      |
|-------------------------------------------------|------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------
| [NewsQuant.json](data/NewsQuant.json)           | 590        | 906         | tagged by the authors                                                                                                                                       |
| [age-model.json](data/age-model.json)           | 19         | 22          | [Microsoft.Recognizers.Text Test Cases Specs](https://github.com/microsoft/Recognizers-Text/blob/master/Specs/NumberWithUnit/English/AgeModel.json)         |
| [currency-model.json](data/currency-model.json) | 180        | 255         | [Microsoft.Recognizers.Text Test Cases Specs](https://github.com/microsoft/Recognizers-Text/blob/master/Specs/NumberWithUnit/English/CurrencyModel.json)    |
| [dimension-model.json](data/dimension-model.json) | 93         | 121         | [Microsoft.Recognizers.Text Test Cases Specs](https://github.com/microsoft/Recognizers-Text/blob/master/Specs/NumberWithUnit/English/DimensionModel.json)   |
| [temperature-model.json](data/recognizers-text/temperature-model.json) | 36         | 34          | [Microsoft.Recognizers.Text Test Cases Specs](https://github.com/microsoft/Recognizers-Text/blob/master/Specs/NumberWithUnit/English/TemperatureModel.json) |

The predictions from GPT-3 for the test datasets above can be found in  `/data/gpt_3_ouput`.

To train and test the unit classifier we generated data using ChatGPT, for the prompts used refer to the paper.
The generated sentences and their classes are under `/data/units/train` (1,827 samples) and `/data/units/test` (180 samples).
