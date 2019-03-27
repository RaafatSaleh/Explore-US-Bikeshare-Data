# Explore US Bikeshare Data

**Summary**

In this project, I used **Python** to explore data related to bikeshare systems for three major bikeshare systems in the United States. I  performed data wrangling to unify the format of data from the three systems and write code to compute descriptive statistics. I also used **&quot;matplotlib&quot;** library that a package that is not part of the standard Python library to help me visualize the data.

**Introduction**

Over the past decade, bicycle-sharing systems have been growing in number and popularity in cities across the world. Bicycle-sharing systems allow users to rent bicycles for short trips, typically 30 minutes or less. Thanks to the rise in information technologies, it is easy for a user of the system to access a dock within the system to unlock or return bicycles. These technologies also provide a wealth of data that can be used to explore how these bike-sharing systems are used.

In this project, I performed an exploratory analysis on data provided by [Motivate](https://www.motivateco.com/), a bike-share system provider for many major cities in the United States. I compared the system usage between three large cities: New York City, Chicago, and Washington, DC. I also saw if there are any differences within each system for those users that are registered, regular users and those users that are short-term, casual users.

**Posing Questions**

Before looking at the bike sharing data, I started by asking questions I wanted to understand about the bike share data. Consider, for example, if I were working for  Motivate. What kinds of information would I want to know about in order to make smarter business decisions? If I were a user of the bike-share service, what factors might influence how I would want to use the service?

**Q 1:** What the peak days, weekdays or weekends, people use bikeshare system? What the trip duration average in terms of Subscribers or Customers? All of three cities follow the same pattern?

**Q 2:** Which season has the more trips duration in average? All of three cities follow the same pattern also?

Answering these questions let Motivate rethink in the number of bicycles during days of the week or seasons, and give it a chance to put pricing policy to activate the both subscribers and customers markets.

**Data Collection and Wrangling**

It&#39;s time to collect and explore the data. In this project, I focused on the record of individual trips taken in 2016 from our selected cities: New York City, Chicago, and Washington, DC. Each of these cities has a page where I could freely download the trip data.:

- New York City (Citi Bike): [Link](https://www.citibikenyc.com/system-data)
- Chicago (Divvy): [Link](https://www.divvybikes.com/system-data)
- Washington, DC (Capital Bikeshare): [Link](https://www.capitalbikeshare.com/system-data)

If you visit these pages, you will notice that each city has a different way of delivering its data. Chicago updates with new data twice a year, Washington DC is quarterly, and New York City is monthly. However, you do not need to download the data yourself. The data has already been collected in the /data/ folder of the project files. While the original data for 2016 is spread among multiple files for each city, the files in the /data/ folder collect all of the trip data for the year into one file per city. Some data wrangling of inconsistencies in timestamp format within each city has already been performed for you. In addition, a random 2% sample of the original data is taken to make the exploration more manageable.

However, there is still a lot of data for me to investigate, so it&#39;s a good idea to start off by looking at one entry from each of the cities we&#39;re going to analyze. I ran the first code cell below to load some packages and functions that I&#39;ll be using in my analysis. Then, I completed the second code cell to print out the first trip recorded from each of the cities (the second line of each data file).

**Condensing the Trip Data**

I noticed in the printout that each city provides different information. Even where the information is the same, the column names and formats are sometimes different. To make things as simple as possible when I get to the actual exploration, I should trim and clean the data. Cleaning the data makes sure that the data formats across the cities are consistent, while trimming focuses only on the parts of the data I&#39;m most interested in to make the exploration easier to work with.

I generated new data files with five values of interest for each trip:

- trip duration, starting month, starting hour, day of the week, and user type. Each of these may require additional wrangling depending on the city:
- Duration: This has been given in seconds (New York, Chicago) or milliseconds (Washington). A more natural unit of analysis will be if all the trip durations are given in terms of minutes.
- Month, Hour, Day of Week: Ridership volume is likely to change based on the season, time of day, and whether it is a weekday or weekend. I used the start time of the trip to obtain these values. The New York City data includes the seconds in their timestamps, while Washington and Chicago do not. The datetime package will be very useful here to make the needed conversions.
- User Type: It is possible that users who are subscribed to a bike-share system will have different patterns of use compared to users who only have temporary passes. Washington divides its users into two types: &#39;Registered&#39; for users with annual, monthly, and other longer-term subscriptions, and &#39;Casual&#39;, for users with 24-hour, 3-day, and other short-term passes. The New York and Chicago data uses &#39;Subscriber&#39; and &#39;Customer&#39; for these groups, respectively. For consistency, I converted the Washington labels to match the other two.

Then, I answered  two questions.

**Question 3a** : Complete the helper functions in the code cells below to address each of the cleaning tasks described above.

**Question 3b** : Now, use the helper functions you wrote above to create a condensed data file for each city consisting only of the data fields indicated above. In the /examples/ folder, you will see an example datafile from the [Bay Area Bike Share](http://www.bayareabikeshare.com/open-data) before and after conversion. Make sure that your output is formatted to be consistent with the example file.

**Exploratory Data Analysis**

Now that I have the data collected and wrangled, I&#39;m ready to start exploring the data. In this section I wrote some code to compute descriptive statistics from the data. I also introduced to the matplotlib library to create some basic histograms of the data.

**Statistics**

First, let&#39;s compute some basic counts. The first cell contains a function that uses the csv module to iterate through a provided data file, returning the number of trips made by subscribers and customers. The second cell runs this function on the example Bay Area data in the /examples/ folder. Modify the cells to answer the question below.

**Question 4a:** Which city has the highest number of trips? Which city has the highest proportion of trips made by subscribers? Which city has the highest proportion of trips made by short-term customers?

**4a answer:**

1. New York City has the highest number of trips (276,798).
2. New York City has the highest proportion of trips taken by subscribers (89%).
3. Chicago has the highest proportion of trips taken by customers (24%).

I wrote my own code to continue investigating properties of the data.

**Question 4b:** Bike-share systems are designed for riders to take short trips. Most of the time, users are allowed to take trips of 30 minutes or less with no additional charges, with overage charges made for trips of longer than that duration. What is the average trip length for each city? What proportion of rides made in each city are longer than 30 minutes?

**4b answer:**

1.The average trip lengths are 16.6, 15.8 and 18.9 minutes for Chicago, NYC and Washington respectively.

2.The proportion of rides that are longer than 30 minutes are 8, 7 and 11 percent for Chicago, NYC and Washington, respectively.

**Question 4c** : Dig deeper into the question of trip duration based on ridership. Choose one city. Within that city, which type of user takes longer rides on average: Subscribers or Customers?

**4c Answer** :

**NYC** Subscribers rides are longer on average than Customers rides : 12.2 min

**Visualizations**

The last set of values that I computed have pulled up an interesting result. While the mean trip time for Subscribers is well under 30 minutes, the mean trip time for Customers is actually above 30 minutes! It will be interesting for us to look at how the trip times are distributed. In order to do this, a new library will be introduced here, matplotlib. I loaded the library and to generate an example plot.

I collected fifty trip times in a list, and passed this list as the first argument to the .hist() function. This function performs the computations and creates plotting objects for generating a histogram, but the plot is actually not rendered until the .show() function is executed. The .title() and .xlabel() functions provide some labeling for plot context.

I used these functions to create a histogram of the trip times for the city you selected in question 4c. Didn&#39;t separate the Subscribers and Customers for now: just collected all of the trip times and plot them.

If you followed the use of the .hist() and .show() functions exactly like in the example, you&#39;re probably looking at a plot that&#39;s completely unexpected. The plot consists of one extremely tall bar on the left, maybe a very short second bar, and a whole lot of empty space in the center and right. Take a look at the duration values on the x-axis. This suggests that there are some highly infrequent outliers in the data. Instead of reprocessing the data, I used additional parameters with the .hist() function to limit the range of data that is plotted. Documentation for the function can be found [[here]](https://matplotlib.org/devdocs/api/_as_gen/matplotlib.pyplot.hist.html#matplotlib.pyplot.hist).

**Question 5:** Use the parameters of the .hist() function to plot the distribution of trip times for the Subscribers in your selected city. Do the same thing for only the Customers. Add limits to the plots so that only trips of duration less than 75 minutes are plotted. As a bonus, set the plots up so that bars are in five-minute wide intervals. For each group, where is the peak of each distribution? How would you describe the shape of each distribution?

**Answer:**

1- For subscribers, the peak of the distribution is in the 5 to 10 minute &quot;bucket&quot;. For customers, the peak of the distribution is in the 20 to 25 minute &quot;bucket&quot; for NYC only. For each user type, the distribution is unimodal, with a positive (right) skew.

2- The shape of the histogram for subscribers is unimodal with a skew to the right. For customers, the mode is further to the right than for subscribers, but the shape still remains positively skewed. The tail is much fatter for customers than for subscribers, as well.

**Performing Your Own Analysis**

So far, I&#39;ve performed an initial exploration into the data available. I have compared the relative volume of trips made between three U.S. cities and the ratio of trips made by Subscribers and Customers. For one of these cities, I have investigated differences between Subscribers and Customers in terms of how long a typical trip lasts. I continued the exploration in a direction that I selected. Here are a few suggestions for questions to explore:

- How does ridership differ by month or season? Which month / season has the highest ridership? Does the ratio of Subscriber trips to Customer trips change depending on the month or season?
- Is the pattern of ridership different on the weekends versus weekdays? On what days are Subscribers most likely to use the system? What about Customers? Does the average duration of rides change depending on the day of the week?
- During what time of day is the system used the most? Is there a difference in usage patterns for Subscribers and Customers?

These questions which I posed in my answer to question 1 align with the bullet points above, this is a good opportunity to investigate one of them. As part of my investigation, for that,  I needed to create something other than a histogram, so I consulted the [Pyplot](https://matplotlib.org/devdocs/api/pyplot_summary.html)documentation. In particular, because I wanted to plot values across a categorical variable (e.g. city, user type), so a bar chart was useful. The [documentation page for](https://matplotlib.org/devdocs/api/_as_gen/matplotlib.pyplot.bar.html#matplotlib.pyplot.bar)[.bar()](https://matplotlib.org/devdocs/api/_as_gen/matplotlib.pyplot.bar.html#matplotlib.pyplot.bar) includes links at the bottom of the page with examples for you to build off of for your own use.

**Question 6:** Continue the investigation by exploring another question that could be answered by the data available. Document the question you want to explore below. Your investigation should involve at least two variables and should compare at least two groups. You should also use at least one visualization as part of your explorations.

**Question 6a:** How does ridership differ by season? Which season has the highest ridership? Does the ratio of Subscriber trips to Customer trips change depending on the season?

**6a: answer:**

1. The bars below aggregate number of trips for each city based on whether the rides occur in four seasons. The bars are qualitatively very similar in each city for the same season of trips, with summer season the most common types of trips, for the three cities.
2. It is reasonable to expect that the number of trips in summer is more trips than others for both user types and the three cities, and we find the winter in the all cities is less than other because the snow and the heavy rains are preventing the user ride the bikes.
3. the bars show the ratio of Subscriber trips to Customer trips is approximately constant in for seasons in the three cities, with small difference in NYC, that is reasonable to expect as explained above.

**Question 6b :**

Is the pattern of ridership different on **the weekends** versus **weekdays**? On what days are Subscribers most likely to use the system? What about Customers? Does the average duration of rides change depending on the day of the week?

**6b answer :**

1. The bars below show the number of trips on weekdays in the three cities. For the subscribers, note that all days of the week is more than others days (Saturday and Sunday) in three cities, that indicating most of them work (employee) in fixed places and times.
2. It is reasonable to expect that the number of trips by Customers in the weekends is more than others days in three cities, that indicating most of them are tourists.
3. The bars of trips duration in the three cities is opposite of number of trips, it is longer in all the days of week. The duration bigger than 30 minutes in NYC and Washington because the limit of normal trip is 45 mins in Washington and 3 hours in NYC, that explains the graph.

**Conclusions**

Question 7: Putting the bike share data aside, think of a topic or field of interest where you would like to be able to apply the techniques of data science. What would you like to be able to learn from your chosen subject?

**Answer:**

I recently conducted a study on the gaps between expectations and perceptions as part of my MBA studies. My analysis was somewhat limited about the services in my library, but it showed conclusively the extent to which data science is capable to measure the clients satisfaction clearly. Data analysis techniques helped me to analyze the questionnaire and abstracting the results.

I would like to delve into the data analysis to pursue it as a new field. It would be interesting to know where I would most likely find these jobs.
