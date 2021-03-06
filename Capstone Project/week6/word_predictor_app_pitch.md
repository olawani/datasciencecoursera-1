
Next Word Predictor Shiny App
========================================================
author: Marco Pasin
date: 26 November 2017

<small>App link:</small>
<br>
<small><https://mcpasincoursera.shinyapps.io/next_word_predictor/></small>
<br>
<small>Code:</small>
<br>
<small><https://goo.gl/SH4ncB></small>

Product background
========================================================
class: small-code

<small>The app is designed to predict the next word based on a incomplete sentence typed by the user. 
Although this is only a proof of concept, the idea is to emulate other more sophisticated predictive text applications like [Swiftkey] (https://swiftkey.com/en), which help users typing on their mobile devices.</small>

<small>The predictive model behind the app relies on [Natural Language Processing (NLP)] (https://en.wikipedia.org/wiki/Natural_language_processing) techniques which allowed us to analyse and learn from large amount of text. A corpora of three files with text coming from twitter, blogs and news was processed in order to provide predictions.</small>

<small>Example of prediction:
<br>
tex typed:  **I have to**
<br>
prediction:  **go**</small>
<br>
<br>
<small>*Please note the app works with only english language*</small>


Operations performed
========================================================

<small>1. A set of ngrams were previously generated using NLP techniques. Mor specifically, 5 tables were prepared and loaded within the app: onegram, bigrams, trigrams, fougrams and fivegrams.</small>
<small>2. In each table, the last word in each gram represents a possible prediction.</small>
<small>3. The user type in some text in the app dedicated box.</small>
<small>4. Prediction model search in the tables to find a possible next word to suggest.</small>
<small>5. Next word is suggested (only one option is returned, the most frequent one according to our model).</small>
<small>6. The user can keep writing and the prediction model will return new outputs on the fly (no need to click on any submit button).</small>

<small>Please note the app might require sometime to load (from our tests less than 15 seconds). Once loaded, the prediction experience will be real-time.</small>


How the prediction model works
========================================================

<small>The model is based on [**Back-Off algorithm**] (https://lagunita.stanford.edu/c4x/Engineering/CS-224N/asset/slp4.pdf). Let's call our model "Naive Back-Off" as it simply takes the most frequent gram on each back-off and doesn't use any discount or smoothing.</small>

<small>1. Count number of words entered by the user. Lets define this as "n_words".</small>
<small>2. If n_words is more or equal than 4, then start search from the fivegram table.</small>
  <small> > If there is no match, back-off to lower order ngram until finding a match</small>
  <small> > Return match with highest frequency (ngrams tables are already sorted from highest to lowest frequency for each sequence of words)</small>
<small>3. If n_words is equal to 3, start search from fourgram table.</small>
  <small> > Back-off if no match, etc.</small>
<small>4. If n_words is equal to 2, start search from trigram table.</small>
<small>5. If n_words is equal to 1, start search from biigram table. </small>
<small>6. If no match is found on any back-off iteration, then suggest most 3 frequent words from unigram table.</small>



A snapshot of the product
========================================================

<small>The idea is to have a **clean and minimal design** to help the user experiencing the prediction model and play with it as much as possible. Type/erase/add new words to your sentence and get the prediction. Enjoy :)</small>

![plot of chunk unnamed-chunk-1](./Cattura.jpg)
