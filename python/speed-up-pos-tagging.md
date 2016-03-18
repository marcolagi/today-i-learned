# Speed up POS tagging

NLTK 3.1's default tagger is good enough for most applications, but it's fairly
slow. Running

    tokens = nltk.word_tokenize('Colorless green ideas sleep furiously')
    tags = nltk.pos_tag(tokens)

takes about 1.5s on my machine. Subsequent requests are not faster than the
first one. The `pos_tag_sents` method is available for batch processing, but
not really the best solution for on line parsing. A workaround is to initialize
the tagger:

    tagger = nltk.tag.perceptron.PerceptronTagger()
    tokens = nltk.word_tokenize('Colorless green ideas sleep furiously')
    tags = nltk.tag._pos_tag(tokens, None, tagger)

The one-time cost of loading the tagger (1.5s) is offset by a 1000x increase
in tagging speed (1.5ms).


