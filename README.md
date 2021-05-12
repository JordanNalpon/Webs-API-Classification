#  Project 3:  Webs API & Classification
---
# Jordan David Nalpon

## __Executive Summary__


### __Executive Summary - Reddit__


Reddit is an American social news aggregation, web content rating, and discussion website. Registered members submit content to the site such as links, text posts, and images, which are then voted up or down by other members.

The website is made up of several smaller online discussion forums called subreddits. Subreddits are community driven with people looking for like-minded people around the world. They cover a wide number of interest groups like sports, films, literature, photography and several others.

I would group the subreddits into 2 groups; image driven and text driven subreddits. 

Image driven subreddits would have images as its main central theme in the group. These images can include photographs, memes or videos. Some examples of image driven subreddits include r/photograph, r/earthporn and r/PrequelMemes/.


Text driven subreddits have very little or no images in the subreddit at all as the main content are mostly texts. Some popular text driven subreddits are r/askreddit, r/nosleep and r/writingprompts.

### __Executive Summary - Problem Statement__

I hypothesis that by having two similar text-driven subreddits, NLP will have a difficult time spotting the difference between the 2 subreddits. If I select 2 subreddits with a relatively large and active community, the posted content in a subreddit will be written by various people with different writing styles. The only connecting factor is that they are in the same subreddit.

### __Executive Summary - Selected Subreddits__

The 2 subreddits I've selected are __r/tifu__ (today I fucked up) and __r/confessions__. Both subreddits are ideal for my problem statement as both normally have lengthy text posts with an active community. The writing style for both are normally a personal recount of the OP (original poster) as oppose to r/nosleep and r/writingpromts where posts are written as fictional narrative stories.

r/tifu is a subreddit that people normally share a funny story about how they fucked up on that day. The community is mostly light hearted and cheerful as the posters are willing to share a funny story at the expense of being laughed at. Below are some notable posts of r/tifu:

https://www.reddit.com/r/tifu/comments/2tdbig/tifu_by_enraging_the_parents_of_my_girlfriend_by/
https://www.reddit.com/r/tifu/comments/3im341/tifu_by_throwing_my_steak_out_a_window/

r/confessions is slightly different from r/tifu as it treats the posts seriously and its a place for people to confess something personal anonymously on the internet. The community are mostly supportive and give suggestions to help the OP. Below are some notable posts of r/confessions:

https://www.reddit.com/r/confessions/comments/bcxd98/i_kicked_all_my_friends_off_my_hbo_account/
https://www.reddit.com/r/confessions/comments/ax83tk/i_put_my_infant_daughter_in_the_closet_shut_the/


### Executive Summary - Steps

I will tackle the problem by doing the following:
1. Exploring Reddit's API to help understand how to unravel the data
2. Web scrap the posts from the subreddits
3. Clean and format the posts
4. EDA the data and pre-process it at the same time
5. Combine all the data into a single dataframe
6. Train/Test split the data
7. Grid Search
8. Analysis and Conclusion


### __Notebook 1 - Exploring Reddit API (Notes)__

Notebook 1 is used primary as a testing ground to poke around Reddit's API. There won't be any transfer of data except as a reference to find which columns are needed to unravel to find the relevant information.

### __Notebook 2: Web Scraping (Notes)__

Notebook 2 is used exclusively to scrape posts from r/tifu and r/confessions and export it out as a csv file. This is kept seperately from the rest as running the code again can result in a change of the entire dataframe and requiring cleaning and processing.

I've added a '_lock' to the export code to the csv in case you want to run the notebook. This won't affect the other notebooks unless you remove the '_lock'.

### __Notebook 3: EDA & Pre-Processing (Notes)__

Notebook 3 takes the data from Notebook 2 and processes it into a usable dataframe. Notebook 1 was used as a point of reference to unravel the data.

Once the dataframe is unravelled, I conducted an EDA and discovered that tldr (too long didn't read) is a very common word which I removed. This is due to r/tifu requring posts to contain a tldr as a subreddit format.

However strangely in r/confessions, 'Hitler' appeared quite frequently which was out of character of the subreddit.

I discovered that there were some spam posts in r/confessions that were spamming the word Hitler. I removed those posts entirely.

Then I added a lemming and stemming column of the text to assist with the NLP and grid search later on.

Now that the dataframe is completed, I did a train/test split and exported it as a csv for notebook 4.

### __Notebook 4: Model Selection (Notes)__

Notebook 4 is mainly doing a grid search to find the best ideal models. I've conducted 2 grid searches; 1 using Count Vectorize and the other TF-IDF.

Based on the results from the search these are the best ideal models:

1. __CountVectorizer LogisticRegression__ (Test Accuracy: 0.86)
    - cv__ngram_range': (1, 1)
    - cv__stop_words='english
    <br>
    <br>

2. __TF-IDF K-Nearest Neighbors__ (Test Accuracy: 0.88)
    - tf__ngram_range': (1, 1)
    - tf__stop_words='english
    
### __Conclusion__
We are able to find 2 ideal machine learning models using NLP and gridsearch. Despite having 2 similar styled subreddits and their formatting removed, we are able to use NLP and grid to find patterns in the words used in both subreddits.