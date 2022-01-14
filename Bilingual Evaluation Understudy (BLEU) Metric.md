Tags: #metric #nlp 

Score in the range of $[0, 1]$ measuring the adequacy and fluency of a language translation.  Since the quality of a translation has some subjectivity in it, scores will not achieve $1$ unless they are identical.  A good BLEU score is $\gtrapprox 0.6$ since two people are unlikely to come up with the same translation.

Sometimes reported when scaled into the range $[0, 100]$ with two-digits of precision.

Proposed in ["BLEU: a Method for Automatic Evaluation of Machine Translation"](http://www.aclweb.org/anthology/P02-1040.pdf) by Papineni et al (2002).

Cannot measure translations for languages that lack word boundaries.

[Wikipedia](https://en.wikipedia.org/wiki/BLEU).