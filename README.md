Download Link: https://assignmentchef.com/product/solved-clc-project-3-n-grams
<br>
Write a script called<strong> build_ngram_model.py</strong>, that takes in an input file and outputs a file with the probabilities for each unigram, bigram, and trigram of the input text.

The script should run with the following command:

./build_ngram_model.py &lt;input_file&gt; &lt;output_file&gt;

The input file format is 1 sentence per line, with spaces between every word.  (The files are pre-tokenized).

Add beginning of sentence (&lt;s&gt;) and end of sentence tags (&lt;/s&gt;) and make everything lowercase.

For example, if a sentence is:

Hello , my cat !

You will count as if the sentence is written:

&lt;s&gt; hello , my cat ! &lt;/s&gt;

The output file should have the following format: (see sample file: dickens_model.txt)

data

ngram 1: types=&lt;# of unique unigram types&gt; tokens=&lt;total # of unigram tokens&gt; ngram 2: types=&lt;# of unique bigram types&gt; tokens=&lt;total # of bigram tokens&gt; ngram 3: types=&lt;# of unique trigram types&gt; tokens=&lt;total # of trigram tokens&gt;

1-grams:

&lt;list of unigrams&gt;

2-grams:

&lt;list of bigrams&gt;

3-grams:

&lt;list of trigrams&gt;

The lists should include the following, in order, separated by spaces:

Count of n-gram

Probability of n-gram (P(wn | wn-1) for bigram and P(wn | wn-2 wn-1) for trigram)             Log-prob of n-gram (take the log base 10 of the probability above)

n-gram

Do not use smoothing for this!  Only include n-grams that exist in the training text.

<h1>Part 2 – Using NGram Models for Text Generation</h1>

Write a script,<strong> generate_from_ngram.py, </strong>that takes an ngram language model (output from the previous part, written to a file as described above), and outputs to a file 5 sentences generated from the unigram, bigram, and trigram models.

The script should run with the following command:

./generate_from_ngram.py &lt;input_file&gt; &lt;output_file&gt;

You will need to import <strong>random</strong> for this script.

Unigram:

Generate a random number from 0.0 to 1.0, and begin to count up the probabilities for the unigrams.  When you reach the unigram whose probability sends the probability total above the random number, add that unigram to the sentence.  Repeat.

Sentences should begin with &lt;s&gt; and end with &lt;/s&gt;, and not have any &lt;s&gt;s or &lt;/s&gt;s between the start and end.

Bigram:

Start with &lt;s&gt;.  Generate a random number from 0.0 to 1.0, and begin to count up the probabilities of the second word, given &lt;s&gt;.  When you reach the word whose probability sends the probability total above the random number, add that word to the sentence, and repeat with the bigrams that start with the word you generated.

Sentences should begin with &lt;s&gt; and end with &lt;/s&gt;, and not have any &lt;s&gt;s or

&lt;/s&gt;s between the start and end.

Trigram:

Same idea as above, adapted to trigrams.  Use the bigram generator to find the first word after the &lt;s&gt; of the sentence.

<h1>Part 3 – Perplexity – Level 3</h1>

Calculating the perplexity on a test set is one way of evaluating the effectiveness of the language model.  Write a script called<strong> ngram_perplexity.py</strong>, that takes in an ngram language model as input (output of Part 1), lambda values, a test file and and output file and calculates the perplexity of the test file.

The script should run with the following command:

./ngram_perplexity.py &lt;input_file&gt; &lt;lambda1&gt; &lt;lambda2&gt; &lt;lambda3&gt; &lt;test_file&gt; &lt;output_file&gt;

Perplexity can be calculated like this:

<table width="0">

 <tbody>

  <tr>

   <td width="645">for each sentence in the test data file:add the number of words in the sentence (excluding &lt;s&gt; and &lt;/s&gt;) to the total number of wordsfor each word(i) in the sentence (excluding &lt;s&gt;, but including &lt;/s&gt;:                         if the word(i) is unknown, increment an unknown word counter and continueCalculate the <strong>interpolated</strong> log-probability of the trigram as below:                                     log( P(word(i) | word(i-2) word (i-1)) )                    Add this log-prob to a running totaldivide the negative sum of the log-probs by the total number of words added to the number of sentences minus the number of unknown words.Raise this value to the power of 10</td>

  </tr>

 </tbody>

</table>

Build a model using dickens_training.txt. Calculate the perplexity for the following lambda values on dickens_test.txt:

<table width="0">

 <tbody>

  <tr>

   <td width="132"><strong>lambda 1  (unigram weight)</strong></td>

   <td width="24"> </td>

   <td width="132"><strong>lambda 2 (bigram weight)</strong></td>

   <td width="24"> </td>

   <td width="132"><strong>lambda 3 (trigram weight)</strong></td>

   <td width="24"> </td>

   <td width="156"><strong>Perplexity</strong></td>

  </tr>

  <tr>

   <td width="132"> </td>

   <td width="24">0.1</td>

   <td width="132"> </td>

   <td width="24">0.1</td>

   <td width="132"> </td>

   <td width="24">0.8</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="132"> </td>

   <td width="24">0.2</td>

   <td width="132"> </td>

   <td width="24">0.5</td>

   <td width="132"> </td>

   <td width="24">0.3</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="132"> </td>

   <td width="24">0.2</td>

   <td width="132"> </td>

   <td width="24">0.7</td>

   <td width="132"> </td>

   <td width="24">0.1</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="132"> </td>

   <td width="24">0.2</td>

   <td width="132"> </td>

   <td width="24">0.8</td>

   <td width="132"> </td>

   <td width="24">0</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="132"> </td>

   <td width="24">1.0</td>

   <td width="132"> </td>

   <td width="24">0</td>

   <td width="132"> </td>

   <td width="24">0</td>

   <td width="156"> </td>

  </tr>

 </tbody>

</table>

Submissions!

You submissions should include the following files, named precisely as outlined here:

<table width="0">

 <tbody>

  <tr>

   <td width="208"><strong>Level 1</strong></td>

   <td width="208"><strong>Level 2</strong></td>

   <td width="208"><strong>Level 3</strong></td>

  </tr>

  <tr>

   <td width="208">build_ngram_model.py</td>

   <td width="208">build_ngram_model.py</td>

   <td width="208">build_ngram_model.py</td>

  </tr>

  <tr>

   <td width="208">generate_from_ngram.py</td>

   <td width="208">generate_from_ngram.py</td>

   <td width="208">generate_from_ngram.py</td>

  </tr>

  <tr>

   <td width="208"> </td>

   <td width="208"> </td>

   <td width="208">ngram_perplexity.py</td>

  </tr>

  <tr>

   <td width="208">shakespeare_model.txt</td>

   <td width="208">shakespeare_model.txt</td>

   <td width="208">shakespeare_model.txt</td>

  </tr>

  <tr>

   <td width="208">dickens_generated.txt</td>

   <td width="208">dickens_generated.txt</td>

   <td width="208">dickens_generated.txt</td>

  </tr>

  <tr>

   <td width="208">readme.txt</td>

   <td width="208">readme.txt</td>

   <td width="208">readme.txt</td>

  </tr>

 </tbody>

</table>

readme.txt should include your favorite sentences from development, any general observations.  Also, commentary on where you got stuck/got help/gave up/ what you found easy!  And the perplexity calculations for level 3

I have provided dickens_model.txt so if you get stuck on Part 1, you can use this model to move on to Parts 2/3.