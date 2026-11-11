# Assignment 2 — Text Analytics & a Simple Recommender
## NorthStar Coffee
**Student:** Mahir Vahora  


## 1. Introduction

The goal of this project was to understand what customers were saying about NorthStar Coffee on social media and review websites. I wanted to find the main topics, understand customer feelings, identify unusual review activity, and help the social media team decide which customer posts need attention first.

The data covers April 1 to September 30, 2026. It includes posts from different platforms, a sample of 300 posts with human sentiment labels, and 10 new customer queries. I used data cleaning, text analysis, sentiment analysis, and a content-based recommender to answer the business question.

## 2. Data preparation

I started by checking the columns and converting dates and number fields into the correct types. I removed duplicate post IDs and posts that did not contain usable text. I also removed posts written by the official NorthStar Coffee account because the purpose was to understand customer opinions rather than the brand's own messages.

I removed **[number]** non-English posts using **[method]**. I made this choice because the sentiment and text models in this project were designed for English. The disadvantage is that the analysis does not represent customers who wrote in other languages.

The search also found posts that used “North Star” for something unrelated to the coffee company. I reviewed the flagged posts and found that they were mainly about **[actual topics from inspection]**. My rule removed **[number]** off-topic posts. I did not use only “mentions coffee” as the rule because a real customer may complain about delivery, refunds, or service without using the word coffee.

For text preprocessing, I changed text to lowercase, removed links and account handles, kept the words from hashtags, and removed common stop words. I kept negation words such as “not” because they can change the meaning of a sentence. I compared normal words with Porter stemming. The vocabulary sizes were **[normal vocabulary]** without stemming and **[stemmed vocabulary]** with stemming. I used **[chosen option]** because **[reason]**.

**Cleaning summary:** [rows before] rows before cleaning and [rows after] after the cleaning steps. The detailed counts are in the notebook.

## 3. Themes and customer topics

I used both raw term frequency and TF-IDF with unigrams and bigrams. Raw frequency shows which words appear most often. TF-IDF gives more weight to terms that help identify a particular post or topic. One difference I noticed was **[explain one real difference from your results]**.

I used K-means on TF-IDF vectors to group posts with similar wording. I compared theme counts from 4 to 10 using silhouette scores and then checked the top terms in each group. I selected **[number]** themes because **[reason based on the chart and terms]**.

| Theme | Human name | Main words/phrases |
|---|---|---|
| 0 | [name] | [top terms] |
| 1 | [name] | [top terms] |
| 2 | [name] | [top terms] |
| [add rows] | [name] | [top terms] |

The weekly chart shows how the share of each theme changed over time. The theme that increased most clearly was **[theme name]**. It started around **[date/week]**. The posts suggest that the reason was **[cause supported by actual post wording]**.

In the last six weeks, this complaint represented **[X]%** of all negative posts. This makes it important because it is not only a topic that customers mention; it is also a noticeable part of the negative feedback.

## 4. Sentiment analysis and suspicious activity

I used VADER as the required baseline. It labels a post positive when the compound score is at least 0.05, negative when it is at most -0.05, and neutral otherwise. Its accuracy on the 300-post gold sample was **[X]%**. The confusion matrix is included in the notebook.

I also trained a logistic regression classifier using TF-IDF features and Trustpilot star ratings. I treated ratings 4–5 as positive, 3 as neutral, and 1–2 as negative. I removed the gold sample IDs from the training data before fitting the model. This is important because the model should not be tested on posts it has already seen. The second model's accuracy was **[Y]%**.

VADER incorrectly labelled **[number]** gold negative posts as positive. After reading the examples, the main reason appeared to be **[sarcasm / mixed opinions / positive words used in a complaint / other reason shown by the posts]**. This shows that a simple word-based sentiment tool can miss the full meaning of a sentence.

I investigated the June Trustpilot reviews because the assignment indicated that there may be an unusual increase in positive reviews. I checked the review dates, account patterns, star ratings, repeated wording, and TF-IDF cosine similarity. The suspicious activity appeared on **[platforms]**, between **[start and end dates]**, with **[number]** posts from **[number]** accounts. The June average rating was **[rating]** with the flagged reviews and **[rating]** after removing them.

I treated these as suspicious candidates rather than automatically calling them fake. Similar wording is a warning sign, but it is not proof by itself. I removed the reviewed burst candidates from the later analysis, as required.

## 5. Content-based recommender

I built a recommender using TF-IDF and cosine similarity. A customer post is used as the query, and the system returns the ten posts with the closest text.

I tested all ten queries. I judged each result as relevant or not relevant and calculated Precision@10 by dividing the number of relevant results by ten.

| Query | Relevant results | Precision@10 |
|---|---:|---:|
| Q01 | [ ] | [ ] |
| Q02 | [ ] | [ ] |
| Q03 | [ ] | [ ] |
| Q04 | [ ] | [ ] |
| Q05 | [ ] | [ ] |
| Q06 | [ ] | [ ] |
| Q07 | [ ] | [ ] |
| Q08 | [ ] | [ ] |
| Q09 | [ ] | [ ] |
| Q10 | [ ] | [ ] |

For Q01, **[number]** of the top ten results came from the suspicious burst before it was removed. After removal, the results changed to **[brief description]**. This matters because a customer could otherwise see repeated or misleading review content.

Q06 returned posts that were textually relevant, but **[explain why they were not useful, such as repeated posts or posts from one account]**. One improvement would be to add diversity so that the results do not all come from the same author or contain almost identical wording.

## 6. Recommendations

The first issue I would ask NorthStar Coffee to fix is **[issue]**. It represented **[X]%** of negative posts in the last six weeks and was still appearing at about **[Z] posts per day/week]**. The company should investigate the cause, review the affected customer orders, and communicate a clear solution to customers.

For the reply queue, I searched the last 14 days of the dataset for phrases such as “cancel,” “switch,” “not ordering again,” and “stop buying.” I ranked the matching posts by likes, replies, and shares. The ten highest-engagement posts are listed in the notebook. These customers should receive a personal response because they are showing signs that they may leave.

For monitoring, I recommend an automatic weekly check of the share of posts belonging to each theme. If a theme rises by at least 50% compared with its average share over the previous four weeks, the system should alert the social care lead and analytics team. The alert should include example posts and the change in the theme's share. This could help the team notice a growing complaint within two days rather than waiting for customers to contact support.

## 7. Ethics and limitations

One privacy risk is that social posts can contain usernames and other information that identifies real people. NorthStar should collect only what it needs, restrict access, and hide usernames in reports. The company should also consider Canadian privacy requirements, including PIPEDA and applicable Quebec privacy rules. Customer text should not be sent to an external AI service unless the company has approved the service and its data-handling terms.

This project also has limitations. A keyword search may miss posts that do not use the searched terms. Sentiment tools can misunderstand sarcasm, slang, or mixed feelings. Similar reviews do not prove fraud. Finally, a recommender finds similar wording, but similar wording does not always mean that a post is useful to a customer.

## 8. Conclusion

This project provides NorthStar Coffee with a way to organize customer feedback, monitor changing topics, compare sentiment methods, and find posts that deserve a response. The most important next step is to investigate **[main issue]**, because **[number/percentage]** of the recent negative feedback was connected to it. The results should be reviewed regularly and combined with human judgement before the company takes action.
