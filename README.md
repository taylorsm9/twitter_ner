# Twitter NER
An NER model trained using Bertweet, a pretrained model created by using the roberta training procedure on a large twitter corpus. 

## Project Description  
There has been interest in training BERT models with large amounts of twitter data (see: bertweet). Our interest was to test the performance of such a model for NER tasks against other pretrained models, both on tweet and non-tweet datasets.

We ensured that our twitter dataset used POS tags, as the improvement in accuracy of twitter POS taggers has made it possible to tag tweets fairly accurately using a model (but we used gold tags for training). 
## Installation Instructions 

	This code was developed to be run from within colab. 
	This direct link will open a copy of "Twitter.ipynb" within colab
	https://colab.research.google.com/github/taylorsm9/twitter_ner/blob/main/NERColab.ipynb
## Usage instructions 
Run the first cell within colab (press the play button!). This cell contains dependencies that need to be installed, along with !git clone, this will clone the github project into colab's /content/ folder,
allowing you to use the datasets and edit the config file. 

The config file now resides at: 

/content/twitter_ner/config.ini

To navigate here, read about the ini settings, and edit the ini file: 
	Click the folder icon on the left side of the screen 
	Click the drop down arrow on the left of the twitter_sentiment folder we cloned from github in an earlier step 
	Click the drop down arrow on the left side of the src folder to expand its contents 
	Double click the file 'config.ini'. this will open an editing pane on the right side of your browser window 

If you don't see the folder or the ini files in colab's file system after running the first cell in your web browser, try hitting the built-in refresh button (folder icon with arrow circle) near the top of colab's file system GUI.


Within the ini there are comments (lines beginning with #) that explain what changing a value will do. By default, the program is set to quickly make a Naieve Bayes model. Be aware, the BERT and ROBERTA 
models may take a long time to train with colab! Google would prefer you pay them a monthly fee to train your models quickly. If you're just testing the program out for fun or to see its functionality, 
try turning your epochs down to 1. The model won't perform well but you'll see that it's working. 

When the config file is to your liking, run the second cell (contains imports and full code). The specified model will be trained with and tested against the dataset you picked out. Available models are BERT and BERTWEET, available datasets are the Kaggle News dataset and an NER annotated TB2 dataset (description below). 

## Method 
Our method is standard. We split the tweets into train, test and dev sets (80, 10, 10). We normalize the tweets for things like contractions and emoji use, tokenize them (with BERT or BERTWEET's built-in tokenizers), and feed them into a pretrained BERT model of our choice.

## Data 
We use two different datasets: 
 
The Kaggle news headlines dataset (information found here: https://www.kaggle.com/datasets/namanj27/ner-dataset)

A version of the TB2 dataset, NER tagged by the tweebank team this year (https://github.com/mit-ccc/TweebankNLP)
This is a small dataset, changes were made to improve training. IoB tags were removed to improve class imbalance. 
The datasets use different POS tagging standards, the TB2 dataset's being simpler (and possible to generate using a state of the art twitter POS tagger). 
## Results:
Test Accuracy: 0.9623201644211007
Test F1-Score:               precision    recall  f1-score   support

         LOC     0.0000    0.0000    0.0000         8
        MISC     0.4727    0.5909    0.5253        88
           O     0.9838    0.9819    0.9829      4151
         ORG     0.6444    0.4754    0.5472        61
         PER     0.7037    0.8028    0.7500        71

    accuracy                         0.9623      4379
   macro avg     0.5609    0.5702    0.5611      4379
weighted avg     0.9625    0.9623    0.9620      4379


## Future work: 
Implementing a Roberta method would allow us to compare the effectiveness of a corpus more effectively than comparing results of the Roberta-based BERTWEET with a BERT model. Because RoBERTa and BERT models train differently, controlling for training would be necessary for a real comparison. 

We would also like to see the cases in which named entities are miscategorized, but still categorized as a type of named entity. For many applications, we don't actually need to know whether someone is talking about a person or an organization, we only need to know which words correspond to entities. Generating these results would be a simple matter of changing the testing code and could only show a performance improvement.

## References: 
D. Q. Nguyen, T. Vu, and A. T. Nguyen, “BERTweet: A pre-trained language model for English Tweets,” arXiv:2005.10200 [cs], Oct. 2020, Accessed: May 08, 2021. [Online]. Available: https://arxiv.org/abs/2005.10200
Nguyen DQ, Vu T, Nguyen AT. BERTweet: A pre-trained language model for English Tweets. arXiv preprint arXiv:2005.10200. 2020 May 20.
Sang EF, De Meulder F. Introduction to the CoNLL-2003 shared task: Language-independent named entity recognition. arXiv preprint cs/0306050. 2003 Jun 12.
Jiang, Hang, Yining Hua, Doug Beeferman and Dwaipayan Roy. “Annotating the Tweebank Corpus on Named Entity Recognition and Building NLP Models for Social Media Analysis.” LREC (2022).
Alan Ritter, Sam Clark, Mausam, and Oren Etzioni. 2011. Named Entity Recognition in Tweets: An Experimental Study. In Proceedings of the 2011 Conference on Empirical Methods in Natural Language Processing, pages 1524–1534, Edinburgh, Scotland, UK.. Association for Computational Linguistics.
