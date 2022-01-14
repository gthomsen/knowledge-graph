Tags: #machine-learning #nlp 

# Machine Translation
# English Constituency Parsing
Comparison of the constituency-based parse tree against ground truth using [[Part-of-Speech (POS) Tagging|part-of-speech tags]].

The sentence "Alice sees Bob" has a phrase structure grammar of:
```
             Sentence (S)
                 |
   +-------------+------------+
   |                          |
 Noun (N)                Verb Phrase (VP)
   |                          |
 Alice                +-------+--------+
                      |                |
                    Verb (V)         Noun (N)
                      |                |
                    sees              Bob
```
Training a model to map from "Alice sees Bob" to the linearized tree `(S (N) (VP V N))`  can be done via sequence-to-sequence translation.

# Reading Comprehension
# Abstract Summarization
# Textual Entailment