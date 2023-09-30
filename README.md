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

For french examples: 
```
examples, metadata = tfds.load('mtnt/fr-en',
                               with_info=True,
                               as_supervised=True)

train_examples, val_examples = examples['train'], examples['valid']
```

print few:

```
for fr_examples, en_examples in train_examples.batch(3).take(1):
  print('> Examples in French:')
  for fr in fr_examples.numpy():
    print(fr.decode('utf-8'))
  print()

  print('> Examples in English:')
  for en in en_examples.numpy():
    print(en.decode('utf-8'))
```


Tokenize:
```
encoded_fr = tokenizers.fr.tokenize(fr_examples)

print('> This is a padded-batch of token IDs:')
for row in encoded_fr.to_list():
  print(row)
```

To detokenize:

```
round_trip = tokenizers.fr.detokenize(encoded_fr)

print('> This is human-readable text:')
for line in round_trip.numpy():
  print(line.decode('utf-8'))
```

