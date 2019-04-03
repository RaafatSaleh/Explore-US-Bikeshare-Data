**Explore US Bikeshare Data**

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

