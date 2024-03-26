# CQE Evaluation 
## Main repo [CQE](https://github.com/vivkaz/CQE).

A Framework for Comprehensive Quantity Extraction. This repository contains evaluation code for the paper:

[CQE: A Framework for Comprehensive Quantity Extraction
](https://arxiv.org/pdf/2305.08853v1.pdf)
 
Satya Almasian*, Vivian Kazakova*, Philipp Göldner, Michael Gertz  
Institute of Computer Science, Heidelberg University  
(`*` indicates equal contribution)  
If you found this useful, consider citing us:
```
@inproceedings{DBLP:conf/emnlp/AlmasianKG023,
  author       = {Satya Almasian and
                  Vivian Kazakova and
                  Philip G{\"{o}}ldner and
                  Michael Gertz},
  editor       = {Houda Bouamor and
                  Juan Pino and
                  Kalika Bali},
  title        = {{CQE:} {A} Comprehensive Quantity Extractor},
  booktitle    = {Proceedings of the 2023 Conference on Empirical Methods in Natural
                  Language Processing, {EMNLP} 2023, Singapore, December 6-10, 2023},
  pages        = {12845--12859},
  publisher    = {Association for Computational Linguistics},
  year         = {2023},
  url          = {https://aclanthology.org/2023.emnlp-main.793},
  timestamp    = {Wed, 13 Dec 2023 17:20:20 +0100},
  biburl       = {https://dblp.org/rec/conf/emnlp/AlmasianKG023.bib},
  bibsource    = {dblp computer science bibliography, https://dblp.org}
}
```
### Prerequisites
Make sure you have Python 3.9 and spaCy 3.0.9 installed. 
Visit the [CQE](https://github.com/vivkaz/CQE) repository for instructions to install CQE. 
You also need to install some additional python packages for the evaluation. Run
```
pip install -r requirements.txt
```

### File and folder structure
To replicate the results from the paper and significance testing, use the following scripts.
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

The predictions from GPT-3 for the test datasets above can be found in  `/data/gpt_3_output`.

To train and test the unit classifier, we generated data using ChatGPT. For the prompts used please refer to the paper.
The generated sentences and their classes are under `/data/units/train` (1,827 samples) and `/data/units/test` (180 samples).

