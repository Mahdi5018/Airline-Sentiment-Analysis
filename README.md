Airline Tweet Sentiment Analysis

An academic text-mining project that classifies airline-related tweets as negative, neutral or positive and explores the complaint categories associated with negative sentiment.

Selected model: Linear SVC. The report records test-set recall of 88.2% for negative, 63.7% for neutral and 74.2% for positive tweets. Neutral sentiment is the main classification challenge.

Research questions

How well can text-mining models classify the sentiment of airline tweets?

Which of Logistic Regression, Complement Naive Bayes and Linear SVC offers the best balance across the three sentiment classes?

Which words, airlines and complaint categories are associated with negative sentiment in the dataset?

The business motivation is to explore how social media text could help teams identify recurring customer concerns and prioritize further investigation.

Dataset

The project uses Tweets.csv, containing tweets directed at major U.S. airlines. Each observation represents one tweet.

Variable

Role in the analysis

airline_sentiment

Target label: negative, neutral or positive

text

Tweet text used for sentiment prediction

airline_sentiment_confidence

Label-confidence score used for filtering

airline

Airline-level exploration

negativereason

Exploration of complaint categories

tweet_created, retweet_count

Contextual variables retained for exploration

The report's exploratory distribution is 62.7% negative, 21.2% neutral and 16.1% positive. This imbalance matters when comparing model performance: aggregate accuracy alone would obscure differences between classes.

The report does not specify the original dataset URL, collection period or final sample sizes after filtering.

Methods

1. Data preparation

Inspect missing values and retain relevant columns.

Filter out tweets with sentiment-label confidence below 0.60.

Lowercase text and remove URLs, mentions, punctuation, HTML entities and numbers.

Expand contractions and remove stopwords while preserving negations such as not and never.

Lemmatize words and remove tweets that become empty after cleaning.

Encode sentiment labels and create stratified training, validation and test splits.

2. Feature engineering

TF-IDF: represent text using unigrams and bigrams, with vocabulary filtering to exclude overly rare or common terms.

Additional text features: character count, word count, punctuation counts, emoji presence, hashtag count, mention count and a negation indicator, extracted from raw tweets.

Standardize the additional features before combining them with TF-IDF features.

3. Model comparison

Model

Purpose

Logistic Regression

Linear classifier for sparse text features

Complement Naive Bayes

Text-classification baseline

Linear SVC

Linear support vector classifier for high-dimensional text features

Logistic Regression and Linear SVC use class_weight="balanced" to account for class imbalance. The report describes 5-fold cross-validation on the training data, followed by validation-set comparison and final test-set evaluation of the selected model.

Models are assessed using confusion matrices and per-class precision, recall and F1-score. Linear SVC was selected for the most balanced behavior across the three classes in the reported comparison.

Findings

Customer sentiment and complaint patterns

Negative sentiment dominates this sample. Negative tweets also tend to be longer than neutral and positive tweets.

Customer Service Issue is the most frequent negative-reason category, followed by Late Flight, Can't Tell and Cancelled Flight. These patterns point to customer service and operational disruptions as recurring concerns in the sample; Can't Tell is an unspecified category.

US Airways has the highest negative share in the reported airline comparison. Virgin America has the largest positive share. These are descriptive findings from the sampled tweets, not a representative ranking of airline service quality.

Negative tweets frequently include words such as cancelled, service, hours, help and delayed. Positive tweets commonly include thanks, great, love and awesome.

Model performance

In the validation comparison, Logistic Regression achieved the highest neutral recall, while Linear SVC offered the most balanced behavior across classes. Complement Naive Bayes was stronger on negative tweets than on neutral tweets.

Final Linear SVC test-set results:

Sentiment

Precision

Recall

F1-score

Negative

0.86

0.88

0.87

Neutral

0.66

0.64

0.65

Positive

0.78

0.74

0.76

Values above follow the report's rounded classification table. Its confusion-matrix discussion gives more precise recall values of 88.2%, 63.7% and 74.2%, respectively.

30.3% of neutral tweets were classified as negative. This is the clearest remaining weakness: neutral messages can contain vocabulary that also appears in complaints.

Business interpretation

The findings suggest a potential use for sentiment analysis in reviewing incoming social media messages and monitoring recurring complaint themes. Customer service issues, delays and cancellations would be useful categories to investigate further.

These are potential applications. The project does not demonstrate deployment, changes to service operations or measured business impact.

Limitations

Sample representativeness: people who tweet at airlines are not necessarily representative of all passengers. Tweet volumes also differ by airline, so findings should not be generalized directly to overall customer satisfaction.

Class imbalance: negative tweets dominate the data. Balanced class weights help address this during training, but neutral and positive performance still require separate attention.

Label filtering: removing low-confidence labels may improve label quality while excluding ambiguous examples that a real system would encounter.

Limited context: TF-IDF captures words and short phrases, but can miss sarcasm, implicit meaning and conversational context. Cleaning may also discard useful sentiment signals, even though some raw-text features are retained.

Neutral-class errors: the model frequently confuses neutral and negative tweets, which could inflate complaint counts in an operational setting.

Reproducibility gaps: the report does not provide exact split proportions, random seeds, complete hyperparameters, dependency versions or sample counts after filtering. It also does not document enough implementation detail to verify that preprocessing was fitted only on training data within each cross-validation fold.

Generalization is untested: no evaluation on newer tweets, other industries or a separate external dataset is reported.

Scope of evidence: this README summarizes the submitted report; the reported results have not been independently reproduced here.

Possible next steps

Publish the notebook or scripts, dependency versions, dataset source and exact split configuration.

Use a reproducible pipeline that fits text transformations and scaling only on training data within each fold.

Inspect neutral-to-negative errors to understand recurring ambiguity and labeling issues.

Report macro-F1, class support and a simple baseline alongside the per-class metrics.

Evaluate on a time-based holdout or an external dataset to test generalization.

Project context and contributors

Course: Data Mining
Institution: Tunis Business School, University of Tunis
Academic year: 2025–2026

Source: Airline Tweet Sentiment Analysis Using Text Mining and Machine Learning, the team's project report. The report notes that artificial intelligence was used in generating the code.
