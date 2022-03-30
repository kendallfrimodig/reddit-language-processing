# Project 3: Web APIs & NLP

## Summary

The following investigation is to demonstrate the apparent divide in content being served to respective political
identities, by showing that a model can use selected text to predict which subreddit the post would belong to. Reddit after all is a
social media format which is driven by 'upvotes' and their own algorithms.  <br>

The second hypothesis is that when ideological buzz words or posts are filtered, content on general policy might be harder
to differentiate between political subreddit, especially since the content is coming directly from citizens and not a media
organization. That is, buzz words such as trump, obamacare, socialism, communism, antifa, qanon, and much more will be excluded from data
extraction, and the hope is that the model will then be unable to predict which political thread the post came from, or
at least will be less efficient.


## Research

Building a model to predict whether a post came from either a republican or democrat subreddit should be fairly straight-forward.
Identity politics is often the result of each sides ideological extreme being the most vocal and represented in media.
The following [survey](https://www.pewresearch.org/politics/2021/11/09/beyond-red-vs-blue-the-political-typology-2/ )
found that political engagement was lowest among moderates

![](https://www.pewresearch.org/politics/wp-content/uploads/sites/4/2021/11/PP_2021.11.09_political-typology_00-04.png)

It has been shown that despite the sharp divisions portrayed by media, most americans agree with respect to everyday
policy issues.

> “Overall I think Americans want not to be divided as politics are forcing it to be, and that’s probably the biggest
message of this poll,” said John Shattuck, director of the Carr Center’s project on Reimagining Rights and
Responsibilities in the United States and a former U.S. assistant secretary of State for Democracy, Human Rights and
Labor. [source](https://www.politico.com/news/2020/09/15/election-season-americans-united-issues-poll-414687)

Though mainstream media has often focused on select issues that only a minority of US citizens deeply care about, the
internet has made this problem much worse in that far more aspects of society have been politicized, and algorithims
have misrepresented the average citizen, whether republican or democrat, by portraying extreme ideological content from
ones opposite party - since emotionally provocative material naturally comes to the surface as part of such algorithms.
This has the unfortunate effect of the average american believing their values differ more from societies values as
shown by the axios
[survey](https://www.axios.com/poll-political-illusions-bipartisanship-climate-77fc7a4d-95ca-46b7-a456-f591218a1098.html)

> Driving the news: Addressing climate change and preserving clean air and water landed in respondents' top 5 personal priorities for the future of the U.S. — but they believe those issues rank closer to the bottom for "most others."
>
> Meanwhile, most people said they care very little about the U.S. being the most powerful country in the world, even though they suspect it to be a middle-of-the-road priority for others.
>
> Priorities differed very little along gender, ethnicity, income and educational lines.


A harvard [survey](https://carrcenter.hks.harvard.edu/reimagining-rights-responsibilities-united-states)
of rights and responsibilities found a high degree of bipartisan agreement on 
expanded policy or constitutional issues. Most americans agreed that more action should be taken
with regards to ssues related to the environment, privacy, education, healthcare, and employment



![](https://hwpi.harvard.edu/files/styles/os_files_xxlarge/public/cchr/files/03_expansive_rights-01.png?m=1599853130&itok=cc2zsZfD)




Additionally the survey found that most americans beleive they have much in common, despite the suggestion
by media that our country is more ideologically polarized than anytime in recent history. 

![](https://hwpi.harvard.edu/files/styles/os_files_xxlarge/public/cchr/files/01_more-in-common-01.png?m=1599849883&itok=7gaqwp0U)

The surveys mentioned have a robust base of interview respondents, and are likely well designed as they are developed
from respected universities. In the modern information environment however, there is likely a survey or data-set, and
set of figures that could support any given viewpoint. One such example is the recent notion that americans beleive we
are nearing a breaking point, and that civil war is a possibility. Given the results described above, this is hard to
reconcile, but as political engagement is disproportionatly skewed towards the ideological exteme, it is not difficult
to understand the provokative results sometimes given by smaller or more informal surveys such as
this [survey](https://www.thewellnews.com/opinion-polls/poll-finds-majority-of-americans-worried-about-another-civil-war/)
conducted by the well news, with 491 participants

Sixty-one percent of Americans are worried that the U.S. could be on the verge of another Civil War, while 52% say they’ve 
already started stockpiling food and other essential in anticipation of social unrest, according to a new national poll.










___


## Layout

The project repository consists of two sets of notebooks, in order to show the processes which led up to the final seriies
of notebooks noted as 'final'. For each 10,000 posts requested, a csv was saved to both backup the data and index the timestamp
to retrieve the next request from. Since the sum of these files was large, the final data was included so that the final set 
of notebooks can run properly. There is much work however in the first set of notebooks for grading purposes.

**Hypothesis:**
1. Building a classification model to predict whether a post originated from either 'conservative' or 'democrat' 
subreddits should be relatively trivial.
2. After removing a set of words, particularly those associated with ideologically extreme views, the model will be less 
efficient at predicting the political subreddit


**Data Collection**
JSON data for reddit submissions was requested using the Pushshift Reddit API, utilizing two functions nested into one 
call to pull 10,000 additional posts for each subreddit

**Data Cleaning and EDA**
Data were filtered primarily on the basis of the post being removed. This cut the sample size in half but greatly reduced the 
possibility of outside actors or bots affecting community narrative. 


**Preprocessing and Modeling**

- two fields contained text for analysis, the selftext (longer preview body text for a post) and the title. 
- A small percentage of posts had a value for selftext so the title was analyzed. Using Sci-kit learns count vectorizer.
- Multiple gridsearches, for vectorizer hyperparameters were performed on top of a default Multi-nominal naive baeysian classifier. 
- Once optimal parameters were chosen for the vectorizer, 40,000 additional posts were pulled for each subreddit and the entire process was re-ran ('final' notebooks) with greater success in predictive scores. 
 **note** the updated models and visualizations can be seen in the 'final' notebooks but additional data and models were ran after presentation



---

## Conclusion


<br> Although the developed model was able to predict posts from a given subreddit with 90% specificity, Filtering out
commonly repeated words did not prove to significantly decrease the predictive scores of the model. For example, in one 
iteration, words were ignored from posts if they appeared in at least 20% of all other posts, with the model still resulting
in an accuracy above 80%.

<br>
Since the activity was far greater for r/Conservative, the date ranges differed quite significantly, and with the pace 
of the news-cycle this could give much more context to this subreddit.

More sophisticated classifiers such as the random forest, and extensive hyper-parameter grid-searches could likely fine 
tune the predictive ability, though requiring further processing time. 


As discussed earlier, political engagement is higher among more far leaning ideologies, so with respect to the initial 
hypothesis of finding common ground between subreddits, perhaps this was not the right forum for such an investigation
