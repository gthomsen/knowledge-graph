Tags: #nlp 

# Greedy Search
TL;DR: Outputs are made with locally optimal choices.

With a table of vocabulary probabilities for each output position, greedy search takes the highest probability symbol at each position.  This may produce a valid sequence of outputs, but may not be the most good as a whole.

# Beam Search
TL;DR: Outputs are optimal across a search window.

With a table of vocabulary probabilities for each output position, the top N choices (the "beam width") are explored for each position.  The resulting N outputs are then ranked ordered and the best is chosen.