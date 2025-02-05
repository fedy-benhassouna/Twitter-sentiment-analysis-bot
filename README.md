# Twitter sentiment analysis bot

## Project overview
This project uses Twitter API v2  with the Tweepy library to request tweet data based on a search keyword and a desired number of tweets both given by the user. the data is then put through an ETL process, and into Pandas dataframe, and then run through a transformer based NLP model for sentiment analysis "BERT". The sentiment result is then added to the tweets and the resulting dataframe is used for analysis to generate a report that details twitter's last sentiment about the given keyword.

#### PS : in order for the code to run you need to provide your own config.py file which is nothing but a simple python file where we're gonna store details about your Twitter API access details. also, make sure you have the following libraries installed in your working environment.

### Dependencies and Resources

* Python 3.9.0,
* Jupyter notebook 6.0.3,
* Twitter API v2
* Libraries: Tweepy, Pandas, Matplotlib.pyplot, WordCloud, Transofmers, re

## implementation

* We start by creating a config.py and storing our access keys and bearer token in variables that we will have access to after importing config, if you don't have Twitter API access credentials you can apply for them here : [apply for access](https://developer.twitter.com/en/apply-for-access)
* we import the necessary dependencies.

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/25c9e1bc-a8bf-4cb9-8550-e5b284ff437b)


* next we write a function that uses Tweepy Paginator to make a call to Twitter API using a number of tweets and a search keyword that is obtained from user input, the result is saved into the tweets list, for more information on how to use Paginator and Tweepy, in general, please refer to [Tweepy documentation](https://docs.tweepy.org/en/latest/).

* The next function takes the list from the previous function and turns it into a dataframe, we use a cleaning regex function to strip the tweet text from any attached mentions, hashtags, or links and store it in a column we name "clean_tweet".

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/00e26cb2-5af2-4995-b89e-78940d5c90ff)


* The next function uses a pretrained transformers NLP sentiment analysis model called "BERT" for more information about Bert please refer to the documentation here :  [BERT documentation](https://huggingface.co/transformers/model_doc/bert.html)

We create a tokenizer by loading a pretrained tokenizer from the library by giving its name in the string passed in as a parametre, a list of possible models can be found on the documentaion mentionned above, we create a model the same way, then we use a pipeline where we specify the type as "sentiment-analysis" and the tokenizer and model to be used.\
We run the model on each "clean tweet" text and store the output in a results list.\
the output from this model is a score from 0 to 1  and a 1 to 5 sentiment indicator, 1 being the worst sentiment and 5 being the best.

* Next we create a function that takes the last result list and unpacks it into the dataframe by storing the data in 3 new columns: score for the resulting score, stars which would indicate the result sentiement number and a sentiement column that takes neutral if the number of stars is 3 and negative or positive if the number is lower or higher respectevly, the result is a final dataframe that has the original tweets data in addtion to the sentiment analysis data.

* The next function we create is going to be reponsible for creating every WordCloud, it takes as parameters a dataframe and the column to generate the wordcloud based on, for more information about wordcloud you can refere to the documention here :  [WordCloud doc](https://amueller.github.io/word_cloud/)

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/64ace09d-f674-4c86-9ea5-8a699ac3652b)


* Next we build a function that creates a report using the final tweet dataframe, by grouping the data using the stars rate and the sentiment.\
 first, it gives out a general sentiment based on the sentiment most represented in the tweet list then it creates Pie charts to visually represent the breakdown.

* The next function uses the previous WordCloud function to create a wordcloud using tweets for each of the sentiments 

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/d055df80-4e40-4d6c-b1d2-461ebcb18c36)


* we create call functions to streamline the process

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/db9ca555-7b08-4b87-925f-26480c7295f4)




### twitter sentiment analysis bot demo

we run the process through the calling functions pipeline :

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/6b6f55a4-24f6-4b87-889a-90c53cc88bc2)


* We enter a search keyword and a number of tweets:

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/3687b5f7-617b-428c-968f-6e8058df22da)


## Result

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/aedb08f3-ddd6-45f0-8f32-f94d39ba63f4)

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/63253c6f-e579-496c-8fdf-a2aea04fa8a2)


#### More examples

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/74d2bc01-f2e6-413e-9bee-deff7e7093e8)

![image](https://github.com/MortadhaMannai/Twitter-sentiment-analysis-bot/assets/93622509/d766cb5a-a713-43bd-9c2c-803f64b630aa)



