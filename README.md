# subword_tokenizer_fr
Learning how to make a french tokenizer

## How to use

Pass the filename below.
```
fr_lookup = tf.lookup.StaticVocabularyTable(
    num_oov_buckets=1,
    initializer=tf.lookup.TextFileInitializer(
        filename='fr_vocab.txt',
        key_dtype=tf.string,
        key_index = tf.lookup.TextFileIndex.WHOLE_LINE,
        value_dtype = tf.int64,
        value_index=tf.lookup.TextFileIndex.LINE_NUMBER)) 
fr_tokenizer = text.BertTokenizer(fr_lookup)
```
Then:
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

