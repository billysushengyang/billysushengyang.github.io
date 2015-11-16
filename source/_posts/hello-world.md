title: Sentiment Analysis
---
In this post I will try to give a very introductory view of some techniques that could be useful when you want to perform a basic analysis of opinions written in english.

## Quick Start

### Defining a structure for the text
``` bash
[[('All', 'All', ['DT']),
 ('that', 'that', ['DT']),
 ('is', 'is', ['VBZ']),
 ('gold', 'gold', ['NN']),
 ('does', 'does', ['VBZ']),
 ('not', 'not', ['RB']),
 ('glitter', 'glitter', ['VB']),
 ('.', '.', ['.'])],
[('Not', 'Not', ['RB']),
 ('all', 'all', ['DT']),
 ('those', 'those', ['DT']),
 ('who', 'who', ['WP']),
 ('wander', 'wander', ['NN']),
 ('are', 'are', ['VBP']),
 ('lost', 'lost', ['VBN'])]]
```



### Prepocessing the Text

``` bash
1 import nltk 
2 
 
3 class Splitter(object): 
4     def __init__(self): 
5         self.nltk_splitter = nltk.data.load('tokenizers/punkt/english.pickle') 
6         self.nltk_tokenizer = nltk.tokenize.TreebankWordTokenizer() 
7 
 
8     def split(self, text): 
9         """ 
10         input format: a paragraph of text 
11         output format: a list of lists of words. 
12             e.g.: [['this', 'is', 'a', 'sentence'], ['this', 'is', 'another', 'one']] 
13         """ 
14         sentences = self.nltk_splitter.tokenize(text) 
15         tokenized_sentences = [self.nltk_tokenizer.tokenize(sent) for sent in sentences] 
16         return tokenized_sentences 
17 
 
18 
 
19 class POSTagger(object): 
20     def __init__(self): 
21         pass 
22          
23     def pos_tag(self, sentences): 
24         """ 
25         input format: list of lists of words 
26             e.g.: [['this', 'is', 'a', 'sentence'], ['this', 'is', 'another', 'one']] 
27         output format: list of lists of tagged tokens. Each tagged tokens has a 
28         form, a lemma, and a list of tags 
29             e.g: [[('this', 'this', ['DT']), ('is', 'be', ['VB']), ('a', 'a', ['DT']), ('sentence', 'sentence', ['NN'])], 
30                     [('this', 'this', ['DT']), ('is', 'be', ['VB']), ('another', 'another', ['DT']), ('one', 'one', ['CARD'])]] 
31         """ 
32 
 
33         pos = [nltk.pos_tag(sentence) for sentence in sentences] 
34         #adapt format 
35         pos = [[(word, word, [postag]) for (word, postag) in sentence] for sentence in pos] 
36         return pos 

```

Now, using this two simple wrapper classes, I can perform a basic text preprocessing, where the input is the text as a string and the output is a collection of sentences, each of which is again a collection of tokens.
By the moment, our tokens are quite simple. Since we are using NLTK, and it does not lemmatize words, our forms and lemmas will be always identical. At this point of the process, the only tag associated to each word is its own POS Tag provided by NLTK.


### Defining a dictionary of positive and negative expressions

``` bash
$ hexo generate
```



### Tagging the text with dictionaries

``` bash
$ hexo deploy
```

### A simple sentiment measure


###Incrementers and decrementers

The previous "sentiment score" was very basic: it only counts positive and negative expressions and makes a sum, without taking into account that maybe some expressions are more positive or more negative than others.

A way of defining this "strength" could be using two new dictionaries. One for "incrementers" and another for "decrementers".

Let's define two tiny examples:


###Inverters and polarity flips


###Conclusion