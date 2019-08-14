Beijing Housing Price Analysis
==============================

Introduction
------------

The topic of our project is to analyze the housing price in Beijing. The first reason why we chose the topic is that it’s related people’s everyday life. Since buying a place to live is a big deal for Chinese people who have their own families. Second, the dataset we downloaded from Kaggle is structured data, different from semi-structured data, there is not much preprocessing works to do. Third, this is a very large dataset that contains 318,851 entries and 28 attributes. The attributes includes CommunityID, TradeTime, Square, Renovation time, Districts, and Price. The place has been sold was distributed in 12 district of Beijing, they are Chaoyang, Changping, Dongcheng, Shunyi, Xicheng, Fengtai, Haidian, Yizhuang, Shijingshan, Mentougou, Tongzhou, and Daxing. After read in the dataset with python, we select several attributes, TradeTime, Construction time, Price, and District to answer data question.

Data question
-------------
1.	What is the average price of each district in Beijing?
2.	What is the average price of housing price in Beijing each year?
3.	Does the construction time will influence the housing price?
4.	What is the public opinion on China’s housing price?

Methodology
-----------
#1.1	Data Extraction<br>
We downloaded dataset from Kaggle: https://www.kaggle.com/ruiqurm/lianjia. Originally, the format of dataset is Excel file. We use pandas.read_excel function to read the dataset. 


#1.2	Data Cleaning and Preparation<br>
In this procedure, firstly, we replace all the Chinese characters with English. In this step, I used re.sub function to locate each phase in this column and replace them. However, we found there are some null values in our key attributes. So, we use following codes to mark all the null values row number first, replace Chinese characters with English, and then drop those rows.  
 
#1.3	Data Analyzing<br>
##1.3.1	Average housing price in each district of Beijing<br>
Above is the coding part for this data question. Firstly, we created many empty lists to store the housing prices. Then, we used .str.cotains function to position the rows that contain the name of each district in column “District”. After storing those housing prices by district, we calculated the average housing price by each district.<br>

##1.3.2	Average housing price in each year<br>
The screenshot above is the codes that we used to calculate the average housing price for each year. The logic of this codes is the same as the first data question. However, one big difference is that the function we use to classify the rows are a conditional statement. If in this row, the value in column “year” is equal to 2016, then store the housing price of this row into list Price_2016.<br>

##1.3.3	Relationship between construction time and housing price<br>
For this data question, the most effort we put is on visualization. So, I will describe how we did it detailedly in data visualization part.<br>

##1.3.4	Public opinion on China’s housing price<br>
This is the most complex one in our final project. Basically, we want to analyze people’s attitude to China’s housing price. So, we scraped 3 news from internet about this topic. Secondly, we split all the articles by sentence level. The train set we used to train our machine learning algorithm is movie reviews. I extracted the top2000 most common words in word list as feature set.
The first classifier is also the easiest one. By Naïve Bayes machine learning algorithm, we got all the positive and negative sentences from 3 news successfully. However, all the sentences are tagged as negative.
We wondered that if there is something wrong with our algorithm. So, we modified our machine learning method, and used the second classifier, which is called SL. After running the function that reads the ‘tff’ file. It creates a subjectivity lexicon that is represented here as a dictionary, where each word is mapped to a list. By looking up to this dictionary, we can count up the presence of positive, negative and neutral words in a document easily.  But the results of this classifier are the same. We will discuss this results more detailed in results part and further conclusion.

#1.4	Data Visualization
That’s all the codes that we used to visualize our analysis results for the first 3 data questions. Generally, we use matplotlib package to draw a line chart, a bar chart and a scatter plot with trend line to make it more straightforward. The reason we choose these plot type is: 1) We want to show the change with timestamp of housing price, so we choose line chart at first. 2) We want to show the difference of housing prices in different districts in Beijing, bar chart is the best option for us to show the gap. 3) We want to show the distribution with every entry with two dimension: price and construction time, that’s why we choose scatter plot to see if there is some strong relationship between construction time and price.

Results
-------
1.	Average housing price in each district of Beijing
 
It’s very clear that housing price of Xicheng, Dongcheng and Haidian are the top 3 in Beijing. The reason is reasonable because these districts are located in the center of Beijing. Also, the housing prices have huge difference from district to district, housing price in Xicheng is almost 4 times of price in Mentougou. We can see the location of house is a very important factor that has huge influence of price.

2.	Average housing price in each year
 
As you can see in this line chart, from 2011 to 2017, the main trend of housing price in Beijing is increasing, especially from 2015, the uptrend line is even steeper. To make it clear, since the units of measurement that we use in China are different from those in US, this means 20 thousand yuan per square of meters. For you guys can better understanding, it’s equal to 315 dollar per square of foot. So, in the past 7 years, the price of housing in Beijing boosted from 315 dollar per square foot to around 1100 dollar per square foot.

3.	Relationship between construction time and housing price
 
In this scatter plot, we want to solve the problem that does the construction time will influence the housing price. Firstly, we drew a scatter plot. You may not see it very clearly cause we have so many entries and we adjusted the size of pints so we can see the distribution of house that constructed in different years by density of points. So, from this diagram, we can see the most of apartments are built around 1980s to 2010s. Furthermore, we add a trend line into the plot to see what’s the relationship between construction time and housing price. So, follow the trend line here, we can know that the more recent construction time, the lower its housing price. At the first glance we may think it’s not reasonable, but after more analysis, we found the most old buildings and apartments that built in old time are likely to locate in the center of Beijing. Also, since the pace of urbanization in Beijing is very fast, there are more and more newly built buildings that are located in the outskirt of city, which is respectively cheaper, that explains the reason why in this plot the more recent construction time, the lower its housing price.

4.	Public opinion on China’s housing price
 
Finally, to have a deeper understanding of China’s housing price. We use nltk package in python to analyze the public opinion on this social issue. We collect three news articles about China’s housing price from some official agencies. We tokenize those news by sentence level and find all the sentences in these three articles are negative. The reason for that is: maybe most of people are pessimistic on this issue. Also, we found our training dataset is from movie reviews and the writing styles and content for reviews are different from news articles, which may lead to the situation that they cannot classify those sentences correctly.

Conclusion
---------
In our project, we answered total four questions and get the result based on our analysis. From our program result, Beijing’s housing price become more and more expensive and is declining with newer buildings. In addition, the public opinion towards Beijing housing price tend to be negative. However, there is still a huge development space in our project, since the prediction of Beijing housing price after 2020 will be less and less, which is at odds with the reality. Moreover, the sentiment analysis we did has a problem, since we used movie review dataset to train our model, which is a different genre. 
Further Work
Our further work can be divided into two section. First, find a best function that could make a better prediction on future housing price. Second, using another dataset to train and test the accuracy of our model, which could make our result more reasonable. Also, we will use some machine learning functions like KNN, SVM or Naïve Bayes to make simple forecast of housing price in future. 
Reference

Data Source: https://www.kaggle.com/ruiqurm/lianjia
https://www.nytimes.com/2018/01/22/business/china-housing-property-tax.html
http://www.xinhuanet.com/english/2018-01/29/c_136933533.htm
https://therealdeal.com/2018/01/17/is-the-chinese-housing-market-about-to-crash/


