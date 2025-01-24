# Punctuation restoration using Transformer model
Project to train fast and accurate punctuation restoration neural network model for production on website. Project code works for all languages ​​and punctuations. Each language will have a separate model. Commas and dots will have a separate model to best accuracy.
## Prerequirements
* Python 3.9 for training
## Installation
```
python -m venv venv;
venv\Scripts\activate;
pip install pipenv;
pipenv install --dev;
```
## Main.py
#### Dataset processing
```
    parse_datasets(dataset_dir) # Преобразовать датасеты *.csv, *.json в файлы *.txt
    normalize_datasets(dataset_dir) # Обработать тексты датасетов  *.txt в текстовые файлы *.normalized
    merge_train_datasets(dataset_dir, language) # Объединить датасеты *.normalized в файл summary_train.dataset
```
#### Training
```
    fit(language, PUNCTUATION_TYPES['COMMA']) # Чем больше гигабайт ОБРАБОТАННЫЙ датасет, тем лучше результат расстановка запятых, иначе результат будет плохой
```
#### Inference
```
    predict = inference(language, 'Привет как дела друг', PUNCTUATION_TYPES['COMMA'])
    print('Результат: ' + predict[0])
```
## Model architecture
1) Pre-trained model FacebookAI/xlm-roberta-base
2) Bi-LSTM layer
3) Linear layer
## Comparison transformers
#### xlm-roberta-base
Multilingual model.
The model weighs weighs 1.2 GB on the hard drive and 2.4 GB in RAM.
Training is 2x faster, so you can experiment with the dataset and input data for the neural network. Quickly places punctuation and puts less load on production server CPU.
#### xlm-roberta-large
Multilingual model.
The model weighs weighs 2.4 GB on the hard drive and 4.8 GB in RAM.
Long waiting time for neural network training. Possible overtraining and accuracy will be worse than xlm-roberta-base.
#### Conclusion
Use xlm-roberta-base. The accuracy is more influenced by dataset and input data than size of neural network.
## Recommended datasets
#### RU
Gazeta dataset; Lenta.ru news dataset; mc4 clean dataset; MLSUM dataset; MuSeRC dataset; WikiLingua dataset;
#### EN
AG News dataset; CC-News dataset; CNN/Daily Mail dataset; Multi-News dataset; XL-Sum dataset; yelp_review_full dataset;
#### FR
MLSUM dataset;
#### DE
MLSUM dataset;
## Dataset improvement
Project using Named Entity Recognition from library [Spacy](https://spacy.io) for best accuracy. Download pipeline for desired language to folder /nmodels/spacy/YOUR LANGUAGE/. Pipelines:
- [ru_core_news_lg](https://spacy.io/models/ru)
- [en_core_web_lg](https://spacy.io/models/en)
- [fr_core_news_lg](https://spacy.io/models/fr)
- [de_core_news_lg](https://spacy.io/models/de)
## Demo
#### Website RU
https://tool-tube.com/punctuation
#### Description website
The neural network COMMA and DOT models is always in RAM for high speed.
#### Server specifications
CPU cores 3; RAM 8 GB
## Credits
My article on [habr.ru](https://habr.ru). Project is written based on code from repositories: 
- [sviperm/neuro-comma](https://github.com/sviperm/neuro-comma)
- [xashru/punctuation-restoration](https://github.com/xashru/punctuation-restoration)
- [vlomme/Bert-Russian-punctuation](https://github.com/vlomme/Bert-Russian-punctuation)
