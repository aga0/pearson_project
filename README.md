# pearson_project

- original instructions & dataset: https://www.kaggle.com/c/competitive-data-science-predict-future-sales/data
- additional instructions in "MLD Pre-interview exercise description" file sent by KŁ

Files you can find in this repository rather than a full pipline, they reflect my approach to the problem I defined when I read instructions and went through data:
- I was used to use R for data wrangling, analyses & visualization
- I had experience with other types of data, but not with time-series
- I had experience with other groups of algorythms than those useful for TS analyses

So I decided to divide this project into three steps:
1. Data exploration with refreshing Python skills and developing them by diving into testing different methods
2. Test "simple" approach, i.e. linear one such as SARIMA to explore typical for TS issues like trends, seasonality, autoregression, etc.
3. Test more complex and state-of-the art solution, i.e. rNNs such as LSTM

It was quite hard to decide based on a literature would be the best for first attempts, so I decided to focus more on looking for most optimized parameters than gathering data for complex cross-validation.

ad. 1
Most steps of data exploration are described by #comments. 

I decided to use univariate approach first to make sure that I know how data "behave" in SARIMA and LSTM architecture. Data aggregation and visualization gave me an insight in effect which could be expected in SARIMA results.

Actually, when I was looking for description of exemplary results interpretation I realized that I should had group the input data for steps 2 and 3 like it was prepared for test data, to increase the power of prediction (and not asses NNs performance based on quite new data structure than used for learning).

ad. 2
I'm attaching copy of the notebook files, because I decided to change the way of data sampling and serializing (finally I grouped them by month, shop and item_id) and analysis is in progress. It seems that I focused on parameters too much - I chosed an approach provided by Jason Brownlee in his tutorials and I didn't run a simple model by guessing parameters. The code provided in notebook files with input >1mln observations was running for few hours. I decided to implement it on EC2 instance, thinking that my computer has too poor parameters. Even though I used p2.xlarge type, after 1h there are only few first iteration of configs printed:
" > Model[[(0, 0, 0), (0, 0, 0, 9), 'n']] 2.102
 > Model[[(0, 0, 0), (0, 0, 0, 12), 'n']] 2.102
 > Model[[(0, 0, 0), (0, 0, 0, 3), 'n']] 2.102
 > Model[[(0, 0, 0), (0, 0, 0, 0), 'n']] 2.102"
 It means that I can't provide you implementation with final prediction.
 
 ad. 3
The same problem I met implementing LSTM (but I knew it would be even slower, so I let it run for whole night locally and few hours on EC2 for later trials). What is strange the code is executed printing "Total configs: 2" which are found, but there are not shown neither any further parameters configurations nor the top 3 of them, which could be used for final NNs. What is problematicm there is no error message. I was chatting with Jason on this issue, but he also doesn't have a clue and suggests the data size problem (I would agree if it did not happen on AWS as well).

Making a long story short, if I had another attemts to this problem, I would start from more architectural perspective, that is building small network step by step and then modify it by increasing its complexity and parameters.

There were many steps of this puzzle, so it's not my final clash with this dataset.
