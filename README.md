# whisper_normalizer

<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

## Installation of package

``` sh
pip install whisper_normalizer
```

or from github repository

``` sh
pip install git+https://github.com/kurianbenoy/whisper_normalizer.git
```

## Why should we normalize/standardize text?

- In ASR systems it’s important to normalize the text to reduce unintentional penalties in
  metrics like WER, CER etc.
- Text normalization/standardization is process of converting texts in
  different styles into a standardized form, which is a best-effort
  attempt to penalize only when a word error is caused by actually
  mistranscribing a word, and not by formatting or punctuation
  differences.(from [Whisper
  paper](https://cdn.openai.com/papers/whisper.pdf))

## Why use this python package?

This package is a python implementation of the text
standardisation/normalization approach which is being used in OpenAI
whisper text normalizer. If you want to use just text normalization
alone, it’s better to use this instead reimplementing the same thing.
OpenAI approach of text normalization is very helpful and is being used
as normalization step when evaluating competitive models like
[AssemblyAI Conformer-1
model](https://www.assemblyai.com/blog/conformer-1/).

## Models evaluated using Whisper normalization

- Massively Multilingual Speech (MMS) models by Meta
- Conformer 1 by AssemblyAI
- Conformer 2 by AssemblyAI

## How to use

OpenAI open source approach of text normalization/standardization is
mentioned in detail Appendix Section C pp.21 the paper [Robust Speech
Recognition via Large-Scale Weak
Supervision](https://cdn.openai.com/papers/whisper.pdf).

You can use the same thing in this package as follows:

``` python
from whisper_normalizer.basic import BasicTextNormalizer

normalizer = BasicTextNormalizer()
normalizer("I'm a little teapot, short and stout. Tip me over and pour me out!")
```

    'i m a little teapot short and stout tip me over and pour me out '

``` python
from whisper_normalizer.english import EnglishTextNormalizer

english_normalizer = EnglishTextNormalizer()
english_normalizer("I'm a little teapot, short and stout. Tip me over and pour me out!")
```

    'i am a little teapot short and stout tip me over and pour me out'

### This model extends Whisper_normalizer to support Indic languages as well. 

The logic for normalization in Indic languages is derived from [indic-nlp-library](https://github.com/anoopkunchukuttan/indic_nlp_library). The logic for Malayalam normalization is expanded beyond the Indic NLP library.

``` python
from whisper_normalizer.indic_normalizer import MalayalamNormalizer

normalizer = MalayalamNormalizer()
normalizer("എന്റെ കമ്പ്യൂട്ടറിന് എന്റെ ഭാഷ.")
```

    'എന്റെ കമ്പ്യൂട്ടറിന് എന്റെ ഭാഷ.'

### Malayalam Normalization unit test

``` bash
python ml_test.py
```


    Passes: 6
    Failures: 3
    Input: എൻറെ
    Expected Output: എന്റെ
    Actual Output: എൻറെ

    Input: എന്റെ കമ്പ്യൂട്ടറിനു് എന്റെ ഭാഷ.
    Expected Output: എന്റെ കമ്പ്യൂട്ടറിന് എന്റെ ഭാഷ.
    Actual Output: എന്റെ കമ്പ്യൂട്ടറിനു് എന്റെ ഭാഷ.
    
    Input: കാൺമാനില്ല
    Expected Output: കാണ്മാനില്ല
    Actual Output: കാൺമാനില്ല
    ----------------------------------------------------------------------
    Ran 1 test in 0.000s
    OK
