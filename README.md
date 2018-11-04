# Trade Publication Topic Analysis
Using natural language processing (NLP) to identify new market development opportunities from a trade publication.

## Summary
Building the market knowledge needed to identify new market development opportunities can be costly and time consuming for industrial companies.  There is a large amount of information available at no or little cost on the internet.  Reading through all of it to gather needed insights is time consuming.  It often must be done by costly experts that understand specific technology to be effective.  A method to reduce the volume of information that needs to be read by experts could make this process more efficient.

It is reasonable to assume that topics important to a market will appear more frequently in various platforms on the internet.  Natural language processing (NLP) works well to measure the frequency with which specific combinations of words ("topics") appear in a selection of text ("corpus").  NLP is also effective at identifying changes over time in the frequency of appearance of topics by comparing topic frequency in a particular corpus at different times.  This can be used to determine which topics are new, and which topics are growing in their appearance frequency.  These capabilities allow NLP to be used to identify selections of text that are most important to a market so that these can be focused on to identify insights for development.

Trade publications focus on specific industrial markets and selecting those focused on a market that is thought to be promising for development can be an initial step in choosing text likely to provide insights.  I have some experience/expertise in the industrial adhesives market so I chose this industrial market for the focus of this project.  To support proof of concept, I chose a trade magazine titled "Adhesive & Sealants Industry" as the corpus for the project and decided to use issues (the magazine is published monthly) from the last five years (August 2013 - August 2018).  The goal for the project was to identify topics from the corpus with strong importance (high, consistent frequency) or that are new (appeared only recently) using NLP.

Python code for the project can be found in Jupyter Notebooks in the **Notebooks** folder.  Two notebooks are included, **trade_topic_scraping.ipynb** containing code for scraping text from the internet and storing it in a Mongo NoSQL database to serve as the corpus for the project, and **trade_topic_analysis.ipynb** containing code for the NLP analysis.

Presentation slides of the findings from the project can be found in the **Presentation** folder in pdf format.

## Findings
A range of text preprocessing options from NLTK and SpaCy, a count vectorizer and tfidf vectorizer, and LDA and NMF models were evaluated on the corpus via the topic optimization process shown below.

![image](Images/topic_optimization.png)

Using SpaCy to change upper case words to lower case, remove punctuation and remove stop words and then tokenizing the text, followed by vectorizing using the tfidf vectorizer for text preprocessing, followed by topic modeling using a non-negative matrix factorization (NMF) model produced the most meaningful and best differentiated topics.

Topic "importances" over time were determined by plotting the topic probabilities output by the NMF model after normalizing for individual articles from the trade magazine versus article publication dates.  These plots were visualized by creating Pandas dataframes of the probabilities grouped by month for each topic with a column for each topic and a row for each month and importing the data into Tableau.

Plots for four example topics can be seen below.

![image](Images/topic_examples.png)

Topic 3 showed strong importance until 2016 when importance fell away.  Topic 4 showed weak importance throughout the five year period from which data was taken.  These are examples of topics that would not be good to consider for exploration for market development.

Topic 1 showed consistently strong importance throughout the five year period from which the data was taken.  Topic 2 showed very strong importance in August 2018 indicating that it may represent a newly developing topic important to the market.  These two topics would be good for further exploration for market development.

Subject matter for the two topics identified as good for exploration was identified using the topic vocabulary from the NMF model and from the article titles and text for the articles in which the topic was important.  Some of this information can be seen for each  of these two topics below.

![image](Images/consistently_important_topic.png)

![image](Images/newly_important_topic.png)

Subjects identified for these two topics are:
* Topic 1 - Adhesives and inks with functionality from exposure to UV or visible light.
* Topic 2 - Reducing the weight of automobiles by replacing metal fasteners with adhesives.

This information can be used to target specific market development exploration activities.  Authors of the articles that produce the strong importance for these topics are included in the Mongo database.  They are likely to be good expert contacts for further information as part of this exploration.
