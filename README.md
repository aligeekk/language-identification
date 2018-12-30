# Language identification in text

This repo includes a frequent word model and a char level n-gram based model implemented without any in-built NLP library to detect language of sentences out of 6 possible choices - French, English, German, Russian, Italian, Spanish. It has been trained on a relatively small dataset [DLI-32](https://github.com/xprogramer/DLI32-corpus), with 10 texts of 93 to 146 words each for each language. This is done so that the model is easily trainable on other languages for which large datasets are not present. The essence of both these approaches has been taken from [Comparison of Language Identification Techniques](https://dbs.cs.uni-duesseldorf.de/lehre/bmarbeit/barbeiten/ba_panich.pdf) by L Panich. Changes have been made in terms of designing matching scores. 

For char n-grams, I am using the average normalised n-gram distances for most frequent bigrams, trigrams and quadgrams as a 'similarity quotient' between 2 documents - the corpus for a given language, and the document to be tested. More weightage is given to those n-grams which do not have a underscore sign in them while assigning frequencies, as underscore is just a replacement for space and is a non-indicator for any language. If we find that a n-gram in a document matches with that of a given language, we take the absolute value of the difference of both its logprobs. We sum up all such absolute values to get the distance of the document from a given language. In case a n-gram of the document is not found in a given language, we penalize by adding a penalty term. Here, I have chosen the absolute value of that n-gram's logprob as the penalty term.

The model was originally built for language identification in documents. However, considering that language detection of shorter length texts poses a more challenging problem, it has instead been tested on random sentences from various translations of Universal Declaration of Human Rights. With this, it achieves an accuracy of 98.5%, with three unique examples being wrongly predicted. 

The idea behind this exercise is loosely based on Andrew Ng's course on Recurrent Neural Networks under Coursera's Deep Learning specialization.
