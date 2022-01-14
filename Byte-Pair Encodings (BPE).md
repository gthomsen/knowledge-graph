Tags: #nlp 

Technique developed to address issues arising from rare words in NLP corpuses.  When a model's vocabulary is set by size or frequency, rare words often are omitted and are replaced with the `<UNK>` token.

German NLP tasks greatly benefit from this as their compound word structures generate a lot of "rare" words.

# Technique
Until the vocabulary size threshold is reached, iterate through the corpus and compute the frequency of character-pairs (byte-pairs).  Replace the most frequency pair with a symbol and add it into the vocabulary.  Repeat.

This allows words like "oblitophobia" to be encoded and incorporated in models as individual character-pairs (naively e.g. "ob", "li", "to", "ph", "ob", and "ia").