# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

## Background
Twitch is an American interactive livestreaming service for content spanning gaming, entertainment, sports, music, and more ([*source*](https://www.twitch.tv/p/en/about/)).

Similar to many other online social platforms, we are always looking for new ways to better engage our users, expands our products and service offerings, thereby increasing customer stickiness through greater user experience and improving both top and bottom lines.

_**Why Gaming?**_<br>
- **Video Gaming Industry**: ~$178.73 Billion in 2021 (increase of 14.4% from 2020) ([*source*](https://www.wepc.com/news/video-game-statistics/))

- **Global eSports market**: ~$1.08 Billion in 2021 (increase of ~50% from 2020) ([*source*](https://www.statista.com/statistics/490522/global-esports-market-revenue/))

- **eSports industry's global market revenue**: Forecasted to grow to as much as $1.62 Billion in 2024. 

- China alone accounts for almost 1/5 of this market. 

In recent months, we started a pilot program with a subset of our most active users by availing them to a new beta forum that has sparked many discussions amongst our gaming users.

This has resulted in hightened traffic with frequent posts and comments updates daily. Our business development and marketing counterparts also realised these gaming users are predominantly focusing on 2 games, namely Dota 2 ([*source*](https://www.dota2.com/home)) and League of Legends (LoL) ([*source*](https://leagueoflegends.com)). 

Our business development and marketing colleagues see great potential in tapping on this group of active gamers and the associated data. However, since there is merely 1 single beta gaming forum thread, users have to sieve through multiple posts to find topics that interest or are relevant to them, resulting in potential poor user experience. Additionally, it would be more effective and efficient to target each game's user base separately by designing sales and marketing campaigns that better meet the corresponding user base's needs.

## Problem Statement

- Our business development and marketing colleagues have requested for us, the Data Science team, to design an **AI model** that **correctly classifies posts** in the 1 single beta gaming forum thread into 2 separate threads, 1 for Dota 2 and another for League of Legends (LoL), with an **accuracy of at least 85%** and **Top 10 Predictors for each subreddit** thereby improving user experience and increasing ease of designing more targeted sales and marketing campaigns that better meet the corresponding user base's needs.

**Datasets scraped:** _(Refer to **Part 1 — Subreddit Posts Extraction** for Data Scraping code)_
 - dota2_raw.csv: Dota 2 dataset
 - lol_raw.csv: League of Legends (LoL) dataset
<br>

**Brief Description of Datasets selected:** 
- The 2 datasets above, each comprising 4,000 records, were scrapped using the pushshift API ([*source*](https://github.com/pushshift/api)) from subreddits: 
  - **r/DotA2** ([*source*](https://www.reddit.com/r/DotA2/)); and 
  - **r/leagueoflegends** ([*source*](https://www.reddit.com/r/leagueoflegends/))


In this project, I scraped data from 2 subreddits, cleaned and preprocessed them for visualisation. Subsequently, I tested 3 models using 2 vectorizers and determined that Multinomial Naive Bayes using TF-IDF vectorizer produces the highest accuracy.


### Baseline Score for Accuracy: 0.5868

With reference to our earlier discussion on Baseline Score above during data cleaning, we established **0.5868** as the **baseline score** for our best model to beat.

This baseline score was derived by adopting a highly simplistic approach of predicting every post to be a Dota2 post. Since there are **3414** Dota2 posts and **2404** League of Legends posts, corresponding to **58.68%** and **41.32%** of total posts respectively after removing duplicates and moderated/deleted posts, we would have scored **0.5868** (i.e. **58.68%**) in terms of **Accuracy**.


### Summary Table of Model Performance
| **Model**              | **Logistic<br>Regression** | **Logistic<br>Regression** | **Multinomial<br>Naive Bayes** | **Multinomial<br>Naive Bayes** | **Random Forest<br>Classifier** | **Random Forest<br>Classifier** |
|------------------------|----------------------------|----------------------------|--------------------------------|--------------------------------|---------------------------------|---------------------------------|
| **Vectorizer**         | **Count**                  | **TF-IDF**                 | **Count**                      | **TF-IDF**                     | **Count**                       | **TF-IDF**                      |
| Grid Search Best Score | 0.949473161                | 0.958785745                | 0.962992280                     | 0.964983686                    | 0.932471005                     | 0.936600343                     |
| Train AUC Score        | 0.989201224                | 0.994598560                 | 0.984728232                    | 0.993496758                    | 0.998315089                     | 0.998971196                     |
| Test AUC Score         | 0.948869118                | 0.958722641                | 0.962233348                    | 0.963496499                    | 0.936894557                     | 0.943955888                     |
| Train Accuracy Score   | 0.904715128                | 0.942534381                | 0.938605108                    | 0.960707269                    | 0.994842829                     | 0.994842829                     |
| **Test Accuracy Score**    | 0.860824742                | 0.882016037                | 0.891752577                    | **0.902061856**                | 0.875715922                     | 0.891179840                      |
| Precision              | 0.818403909                | 0.855160451                | 0.917165669                    | 0.896840149                    | 0.885496183                     | 0.865907099                     |
| Recall or Sensitivity  | 0.980487805                | 0.961951220                 | 0.896585366                    | 0.941463415                    | 0.905365854                     | 0.963902439                     |
| Specificity            | 0.690707351                | 0.768377254                | 0.884882108                    | 0.846047157                    | 0.833564494                     | 0.787794730                      |
| F1-Score               | 0.892143808                | 0.905417815                | 0.906758757                    | 0.918610186                    | 0.895320791                     | 0.912280702                     |
| True Negative (TN)     | 498                        | 554                        | 638                            | 610                            | 601                             | 568                             |
| False Positive (FP)    | 223                        | 167                        | 83                             | 111                            | 120                             | 153                             |
| False Negative (FN)    | 20                         | 39                         | 106                            | 60                             | 97                              | 37                              |
| True Positive (TP)     | 1005                       | 986                        | 919                            | 965                            | 928                             | 988                             |


### Multinomial Naive Bayes' (TF-IDF vectorizer) Score for Accuracy: 0.9021
Referencing the summary table of model performance above, **Multinomial Naive Bayes using TF-IDF vectorizer** yields the highest **Test Accuracy Score** of **0.902061856** which decisively beats the Baseline Score of **0.5868**. Additionally, since the Test Accuracy Score is worse than the Train Accuracy Score by merely 0.058645413, there is likely no over-fitting issues.

Thus, Multinomial Naive Bayes' (TF-IDF vectorizer) is chosen as the best model for our dataset.

### Limitations and Future Plans

**1) Model Accuracy Improvement**
 - Better data cleaning steps e.g. remove additional Character Entities
 - Further hyperparameter tuning to enhance accuracy, while balancing 
 - Identify and rectify cause(s) for model's post misclassifications (i.e. False Positives and False Negatives)

**2) Include New Model Features**
 - Analyse moderated posts to implement auto regulation of potential user rogue behaviour e.g. profanities, spams, scams, etc.
 - Sentiment analysis

### Recommendations and Conclusion

_**Internal**_
1) Roll out AI model classification to split posts into 2 separate threads
  - Multinomial Naive Bayes' (TF-IDF vectorizer) Model accuracy > 85% and Top 10 Predictors for each subreddit have been identified
  
2) Establish timeline for future model features roll-out, e.g. auto Twitch forum moderation, sentiment analysis, etc.

3) Tease out campaign specific insights e.g. new users acquisition, advertising, etc.

<br>

_**External**_
1) **Developers**:
 - Data Insights as a Service on sentiments, new games &/or features, etc.
 - Explore potential advertising, partnership, sponsorship opportunities, etc.
 
2) **Esports/Events**:
 - Data Insights as a Service on game interests, event/tournament mechanics, etc.
 - Explore potential advertising, partnership, sponsorship opportunities, etc.

3) **Gaming Streamers**:
 - Insights on peak online user activities, etc.

 In conclusion, I developed a Multinomial Naive Bayes' (TF-IDF vectorizer) Model with accuracy > 85% and Top 10 Predictors for each subreddit have been identified, thereby meeting the objectives set out by the Problem Statement.

With the blessings from the business development and marketing stakeholders, I shall proceed to implement the items set out above in the limitations, future plans and recommendations sections. I am confident that we could potentially further enhance user experience when the posts are eventually split into 2 distinct threads. I also look forward to partnering all of you in teasing out campaign specific insights to improve both top and bottom lines for the organisation!