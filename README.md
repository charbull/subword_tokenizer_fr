# subword_tokenizer_fr
Learning how to make a french tokenizer

## How to use

Download it
```
model_name = 'mtnt_fr_en_converter'
tf.keras.utils.get_file(
     f'{model_name}.zip',
    'https://github.com/charbull/subword_tokenizer_fr/raw/main/mtnt_fr_en_converter.zip',
    cache_dir='.', cache_subdir='', extract=True
```
Then:
```
tokenizers = tf.saved_model.load(model_name)
```

list the methods:

```
[item for item in dir(tokenizers.en) if not item.startswith('_')]
```

Tokenize:
```
encoded = tokenizers.en.tokenize(en_examples)
```

```

# Tokenize the examples -> (batch, word, word-piece)
token_batch_fr = fr_tokenizer.tokenize(fr_examples)
# Merge the word and word-piece axes -> (batch, tokens)
token_batch_fr = token_batch_fr.merge_dims(-2,-1)
```

To detokenize:

```
words = fr_tokenizer.detokenize(token_batch_fr)
fr_sentence = tf.strings.reduce_join(words, separator=' ', axis=-1)
print(fr_sentence)
```

