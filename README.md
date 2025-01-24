# Punctuation restoration using Transformer model
Project to train fast and accurate punctuation restoration neural network model for production on website.

## Prerequirements
* Python 3.9 for training

## Installation
```
python -m venv venv;
venv\Scripts\activate;
pip install pipenv;
pipenv install --dev;
```

## Demo RU
https://tool-tube.com/punctuation

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
Project using Named Entity Recognition from library [Spacy](https://spacy.io)
- For RU [ru_core_news_lg](https://spacy.io/models/ru)
- For EN [en_core_news_lg](https://spacy.io/models/en)
- For FR [fr_core_news_lg](https://spacy.io/models/fr)
- For DE [de_core_news_lg](https://spacy.io/models/de)

## Credits
Our article on [habr.ru](https://habr.ru)

Project is written based on code from repositories: 
- [sviperm/neuro-comma](https://github.com/sviperm/neuro-comma)
- [xashru/punctuation-restoration](https://github.com/xashru/punctuation-restoration)
- [vlomme/Bert-Russian-punctuation](https://github.com/vlomme/Bert-Russian-punctuation)
