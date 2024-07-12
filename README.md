# Reddit Topic Telescope

Group members: Oksana Kalytenko, Mariia Pyvovar, Alisea Stroligo

## Abstract

This project analyses topics in the “ExplainLikeImFive” subreddit to understand community interests and sentiments through topic extraction and sentiment evaluation. It then combines findings from the previous two text-analysis techniques (Topic Modeling and Sentiment Analysis) to infer also non-textual properties of the dataset (e.g. general behaviors of users online).

## Introduction

With the provided dataset we were looking for inspirations on what to achieve with this kind of data. After some research we found commercial dashboard tools that analyse topics and sentiment in documents.
We liked the idea of visualising topics together with sentiment to show hidden meaning inside texts written by different users.
This served as our main inspiration and analysis was split into three different parts:

- Topic Modeling
- Sentiment Analysis
- Network Analysis (combining topics with sentiment)

With these analyses it is our goal to get some summarised insights into a large number of documents, with the prospect to make conclusions for actions in the real world.

For topic modeling we decided to use BERTopic. As a starting point we used the original paper by Grootendorst M. (2022) [1] as well as a short write-up on the usage of the model by the original author on towardsdatascience.com [2]. With this model we are able to extract topics by leveraging clustering, while keeping the most important words inside each topic. This allows us to manually create best fitting names for each topic.

Inspired by the foundational work of Hutto and Gilbert (2014) on VADER: A Parsimonious Rule-Based Model for Sentiment Analysis of Social Media Text [3], which introduced VADER as an effective tool for analyzing sentiment in social media content, we chose to conduct our analysis specifically using VADER. Additionally, our exploration was informed by the comparative analysis presented in the paper 'Comparative Analysis of Lexicon and Machine Learning Approach for Sentiment Analysis' [4]. This study discussed the strengths and weaknesses of two prominent models, VADER and Afinn.

Additionally, we took inspiration from the paper by Buntain et al. (2014) [5] and from the following project on Reddit Network Analysis https://github.com/samridhprasad/reddit-analysis [6], both of which are concerned with the distribution of posts by users between different subreddits and find Reddit-specific properties in the users' activity. We were therefore motivated to try to find similar features in our dataset. In the absence of complete information on the user interactions and given the choice of reducing the dataset to a single subreddit, we challenged ourselves to find similar non-textual properties (i.e., users' behavior on the specific online platform) by exploiting the results of computational linguistics tools (i.e. Topic Modeling and Sentiment Analysis on text).


## Dataset

The dataset used for analyses consists of a corpus containing preprocessed posts from the Reddit dataset (Webis-TLDR-17), available at https://huggingface.co/datasets/webis/tldr-17. From this dataset, after preprocessing, for all further analyses (Topic Modeling, Sentiment Analysis and Network Analysis) only a subset of the data was used, i.e., all content from subreddit 'explainlikeimfive'. 
This particular subreddit was chosen due to content (we expected a variety of different topics mentioned in this particular subreddit, optimal for Topic Modeling), size (after preprocessing, this subreddit appeared among the 20 most visited subreddits, but not among the first ten, so that it provided a large amount of content but would also not be among the most computationally expensive for analyses) and finally it presented similar characteristics to other subreddits in terms of number of posts, number of authors and frequency of posts per author (i.e. important features for Network Analysis), therefore this subreddit also seemed to be a representative sample for the whole original dataset.
The complete data from the subreddit 'explainlikeimfive' can be found in a .zip file in the code folder of our GitHub repository.

## Methods

### Setup 

All the notebooks are in the [/code](https://github.com/OksanaKalytenko/docana-project-Reddit-Topic-Telescope/tree/main/code) folder with their requirements.txt files. After installing the requirements the notebooks can be run in any compatible environment.

#### Data Preprocessing Setup

To install Python libraries for Data Preprocessing with the correct version run the following command in the terminal:
```bash
pip install -r requirements_preprocessing.txt
```

#### Topic Modeling Setup

- Used environment: Google Colab with Python Version 3 and T4 accelerator

To install Python libraries for Topic Modeling using BERTopic with the correct version run the following command in the terminal:
```bash
pip install -r requirements_topic.txt
```

#### Sentiment Analysis Setup 

Operating System: Darwin Darwin Kernel Version 23.5.0
To install Python libraries with the correct version run the following command in the terminal:
```bash
pip install -r requirements_sentiment.txt  
```

#### Network Analysis Setup
- Software: Microsoft Windows Version 22H2 (OS Build 19045.4529), Visual Studio Code 1.91.0     
- Hardware environment: 
CPU: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz, 2592 Mhz, 6 Core(s), 12 Logical Processors; 
GPU: Intel(R) UHD Graphics 
- Python version: Python 3.9.13   
All analyses for Network Analysis were written in .ipynb files, coded and run in Visual Studio Code 1.91.0

To install Python libraries for Network Analysis with the correct version run the following command in terminal:
```bash
pip install -r requirements_networkanalysis.txt  
```

### Experiments

#### Initial Preprocessing Steps
- Subreddit Selection: We reduced our dataset to only include posts from the "explainlikeiamfive" subreddit.
- Identified and removed rows that were empty, null, or contained only punctuation.
- Identified and removed exact duplicate texts.
- Outcome: The dataset was cleaned by removing all non-useful texts and exact duplicates, resulting in a more refined and relevant collection of data for further analysis.

#### Summary of Topic Modeling Workflow

- ##### Pre-calculating Embeddings
First, embeddings for the content were pre-calculated using the SentenceTransformer model "all-MiniLM-L6-v2". This step ensures efficient handling of text data in subsequent processes.

- ##### Preventing Stochastic Behavior
To ensure reproducibility in topic modeling results, the UMAP dimensionality reduction algorithm was configured with a fixed random state. This setup mitigates the stochastic nature of UMAP, providing consistent results across multiple runs.

- ##### Controlling Number of Topics
The number of topics was controlled using HDBSCAN's `min_cluster_size` parameter. Adjusting this parameter influences the number of clusters formed: a higher value results in fewer topics, while a lower value generates more topics.

- ##### Vectorization
A `CountVectorizer` was employed to transform the text data into a numerical format, removing English stop words and considering both unigrams and bigrams.

- ##### Topic Representation Models
Various models inspired by KeyBERT, SpaCy's Part-of-Speech tagging, and Maximal Marginal Relevance (MMR) were used to diversify and enhance the topic words. These models were combined into a representation model for BERTopic.

- ##### BERTopic Configuration
The BERTopic model was configured with the pre-calculated embedding model, UMAP model, HDBSCAN model, vectorizer model, and the combined representation models. The model was set to identify the top 10 words per topic and was run in verbose mode to provide detailed outputs.

- ##### Topic Modeling Execution
The BERTopic model was fitted and transformed on the content data, using the pre-calculated embeddings to generate topics and their probabilities.

- ##### Outlier Reduction
To ensure that all documents were assigned to a topic, outliers generated by HDBSCAN were mapped to existing topics. This step helps in creating accurate topic representations and reduces unassigned data points.

#### Summary of Sentiment Analysis Workflow

In our sentiment analysis experiments, we explored two different models: VADER and the lexicon-based text analyzer Afinn. Both VADER and Afinn operate using pre-defined sentiment lexicons rather than requiring training data. However, they excel in different aspects of sentiment analysis.

However, without access to human-labeled data for direct accuracy comparisons, it is challenging to definitively assess which model performed more accurately.

VADER is known for handling informal language, emojis, nuanced sentiments, and sarcasm interpretation. This capability makes VADER particularly well-suited for analyzing social media content and informal text data. Despite not having access to human-labeled data for direct accuracy comparisons during our experiments, VADER consistently showed superior performance in these areas.

#### Summary of Network Analysis Workflow

- ##### Exploration and Preprocessing of Data
The data used in the first step of the Network Analysis part of the project consisted initially of the complete provided Reddit dataset. This data then underwent the same general filtering and preprocessing criteria enlisted at the beginning of this section, and a sample of 10000 posts was then used for further analysis, this data can be found in our .zip data folder as a .csv file 'webis_tldr_clean'.
Firstly, we explored the possibility of using all subreddit data for the network analysis, this implied understanding the number of authors (nodes of our graph) and number of posts (node sizes) per subreddit (each same-colored edge connecting all authors active in a specific subreddit).  
We subsequently plotted a Network Graph to visualize the properties of the dataset and confirm the suitability of the 'explainlikeimfive' subreddit selection also on the dimensions important for further network analysis.
For this part of analysis we relied on a sub-sample (100 most visited subreddits) of the dataset for visualization.
These analyses can be found in the following file: AllData_Network_Analysis.ipynb

- ##### Network Analysis on selected Subreddit
This part of the analysis was conducted on the resulting data of the previous two analysis steps (Topic+Sentiment Analysiss) on the subreddit data stored in in our .zip data folder as a .csv file 'explainlikeimfive'. The combined results are stored instead in the file 'webis_tldr_subreddit(topic+sentiment).csv'. This data underwent the same general filtering and preprocessing criteria enlisted at the beginning of this section.
We plotted the Network Graph, similarly to the previous plot, in which nodes represent different users and node size represents the number of posts per user, however, in this case edges represented different topics (not subreddits, as above) and nodes were colored on the basis of the average sentiment of each user's overall posts.
Also, for this part of analysis we relied on a sample (1000 posts) of the dataset for visualization.
These analyses can be found in the following file: Subreddit_Network_Analysis.ipynb


## Results and Discussion

Our result as a dashboard can be found [here](https://oksanakalytenko.github.io/docana-project-Reddit-Topic-Telescope/dashboard/).

### Topic Modeling

A total of 30 different topics were identified in the dataset. "Economic and Financial Systems" is the largest topic in our subreddit. The next popular topics are "Genetics and Human Evolution", "Physics and Cosmology", "Gaming and Software Development", "Nutrition and Dietary Health".

Some topics may overlap like "Mathematical Concepts and Number Theory" and "Gaming and Software Development". "Genetics and Human Evolution" topic contains a lot of posts on sexuality and women rights? Maybe this topic can be split further into 2 topics. It looks like more manual inspection is needed.

Next steps:
*   Validate and adjust topics manually where necessary, based on domain knowledge and understanding of the dataset.
*   Adjust parameters (n_topics, min_topic_size)

### Sentiment Analysis

Our analysis reveals that topics such as Cultural Diversity and Ethnic Background, Firearms Public Safety, Human Anatomy and Health, Immunology and Diseases, Law Enforcement, Affairs and Religious Extremism, Welfare, and Diplomatic Relations tend to have more negative sentiment on average.

### Network Analysis

Our main findings in this conclusive part of our project were that most users only participated in the subreddit with one post and (therefore) were also interested in only one topic on average. There do seem to exist however few users which are very active and participanting in conversations on multiple topics, these might be the "answer-persons" [5], a well-known role present in many other online platforms. Overall there seemed to be little interaction between users and a focus by each user on a specific select topic, potentially indicating that Reddit is not mainly used to connect with people but to retrieve information and opinions without extensive and repeated discussion among users.
Therefore the distribution of user activity seems to be in line with our chosen reference paper [5] and project [6], which show similar results.
A few questions emerged from the network analysis:
- Do the few "macro-users" or so-called "answer-persons" (less than ten on average in our samples) influence the vast majority of other users (in the order of thousands)? If so, to what degree and in which modality, both sentiment and topic?
- Could many users actually be bots? Considering our reference paper [5] this does not seem to be the case, however it might be interesting to explore this possibility through models that might distinguish human-generated text and artificially created text.
- Do the properties observed in the timeframe of our dataset (2006-2016) still apply today, or has the use of this platform changed?
- Does the distribution of activity among users on Reddit differ from other online platforms?

These findings and related questions provide insights into potential further analyses.


## Conclusion

### Topic Modeling

This analysis shows how natural language processing helps uncover what interests the community. "Economic and Financial Systems" stood out as the most discussed topic, indicating a strong interest in simplified explanations of complex financial concepts. Other popular topics included "Genetics and Human Evolution", "Physics and Cosmology", "Gaming and Software Development", and "Nutrition and Dietary Health", showing the community's diverse interests in science, technology, and health. These insights might be helpful for governments and other creators of educational content to focus their efforts towards the topics outlined in this project and create more accessible content in these rather complex areas.

### Sentiment analysis

Topics like Cultural Diversity, Firearms Public Safety, and Law Enforcement tend to have more negative feelings due to the controversial nature of these discussions, which often touch on sensitive and polarizing issues. These discussions often cause strong negative emotions and frustrations in the community, showing bigger societal issues like discrimination, racism, politics, and religion. Understanding these feelings helps us track public opinion and predict how the community might react.

### Network Analysis

In this conclusive part of our analyses we were able to combine Topic Modeling and Sentiment Analysis through Network Analysis in order to find non-textual properties of our dataset starting from the users' posts only. Our results, discussed in the previous section, also seem to be in line with the findings of our reference paper [5] and project [6]. 

Overall, we were able to test in our chosen subreddit the effectiveness of computational linguistic tools in providing insights on a dataset on a variety of dimensions, including non strictly-textual properties.

## Contributions

| Team Member  | Contributions                                             |
|--------------|-----------------------------------------------------------|
| Oksana Kalytenko | Data Preprocessing, Topic Modeling, Dashboard Creation&Design|                                                       |
| Mariia Pyvovar  | Data Preprocessing, Sentiment Analysis                                                       |
| Alisea Stroligo       | Data Preprocessing, Network Analysis                                                    |

## References

- [1] Grootendorst, M., 2022. BERTopic: Neural topic modeling with a class-based TF-IDF procedure. arXiv preprint arXiv:2203.05794.

- [2] Grootendorst, M., 2021. Interactive Topic Modeling with BERTopic. https://towardsdatascience.com/interactive-topic-modeling-with-bertopic-1ea55e7d73d8
  
- [3] Hutto, C., & Gilbert, E. (2014). VADER: A Parsimonious Rule-Based Model for Sentiment Analysis of Social Media Text. Proceedings of the International AAAI Conference on Web and Social Media, 8(1), 216-225.

- [4] Roopam Srivastava, Prof. (Dr.) P.K. Bharti, Dr. Parul Verma, (2022). Comparative Analysis of Lexicon and Machine Learning Approach for Sentiment Analysis. (IJACSA) International Journal of Advanced Computer Science and Applications

- [5] Buntain, C.; Golbeck, J. Identifying social roles in reddit using network structure. In Proceedings of the 23rd International Conference on World Wide Web, Seoul, Republic of Korea, 7–11 April 2014; pp. 615–620. **doi:10.1145/2567948.2579231**

- [6] Samridh Prasad, reddit-analysis, (2019), GitHub repository, https://github.com/samridhprasad/reddit-analysis
