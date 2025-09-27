\~ Content & Catalog Analysis

**What’s the yearly trend of titles added to Netflix?**

The biggest growth of added titles to the Netflix catalog happened between 2016 and 2017, with an increase of 758 new titles from one year to another. In 2016 the company expanded to 190 countries and announced it would increase its original production to 50% of its catalogue. Its fast expansion and desire to create original content can explain the higher number of titles being added in the pointed period. 

The company saw a growth of titles being added up until 2019, when 2016 new titles were added to the catalogue. However, the following years saw a decrease in the count of titles added. From ​​2019 to 2020, 1879 new titles were added, and from 2020 to 2021 the number was 1498\. This could be possibly explained by the pandemic that forced a global quarantine, interrupting countless productions. 

\~ Solution: Pivot Table\> added\_year as row, count of title as value.



**What is the split between Movies and TV Shows?**

There were added a total of 6131 movies, and 2676 series to the catalogue between 2006 and 2021\.

\~Solution: Pivot Table\> type as row, count of titles as value.

**Which countries have the most titles available?**

The top 3 countries with the most titles available are: The United States, with 3698 titles, followed by India, with 1046, and the United Kingdom with 806\. As the country column shows more than one country per cell, I first opened the table on power query, split the country column in rows using comma as the delimiter, then I trimmed it. Finally, I grouped by country, and it gave me the count of titles per country. 

**![][image2]**

**Which genres dominate Netflix’s catalog?**  
These are the top 5 genres. (Found it using the same rationale I used to find the country’s list).

![][image3]

Even when the genres are not split using a comma as the delimiter, the list is still similar. Dramas and international movies are the most added genres.

![][image4]

---

 \~Runtime & Format Insights

**What’s the distribution of movie runtimes (minutes)?**

Runtime below 90 is 4515, between 90 and 120 is 2936, and higher than 120 is 1144\. Therefore, the majority of movies are of short length. This is an interesting result, it would be nice to understand if this trend increased in the past years, considering that plenty of studies have been showing that the average attention span of social media users is decreasing, which could result in people preference of shorter movies. 

I used these standards because the trend of past decades is that the average runtime of movies falls between 90 and 120 minutes. 

I used a pivot table in which rows were titles and values were sum of duration per minutes, and I used the countif function to calculate the number of titles per duration.

**What’s the average number of seasons for TV shows?**

The average number of seasons for TV shows is around 2 seasons. Using a pivot table in which the duration by season is the value, I applied the average function to calculate the average season per show and the result was 1,69 which I rounded to 2 seasons. However, it could mean the majority of TV shows fall between 1 and 2 seasons. Therefore, Netflix prefers to add shorter series to its catalogue. In fact, there are 1810 titles with 1 season, against 425 with 2 seasons. The production of additional seasons cost more, considering that 50% of its content is original, it is understandable that the company would prefer to cut costs when it is not necessary. Indeed, the company has a policy of TV shows cancellation that considers viewership metrics and completion rates. When a series doesn’t reach the company’s standards, it is cancelled in the first season.   
---

\~ Diversity & Representation

**How many unique countries are represented each year?**


The increasing number of unique countries represented per year shows the company’s commitment to diversity in its catalogue.

**What is the spread of ratings (e.g., PG, R, 16+, etc.) across movies and TV shows?**


The dataset used the US standard movie ratings for movies produced primarily to the cinemas. The rating are: 

G (General Audiences), 

PG (Parental Guidance Suggested), 

PG-13 (Parents Strongly Cautioned), 

R (Restricted, under 17 requires accompanying adult)

NC-17 (No one 17 and under admitted).  

According to the results of this present analysis, the majority of movies added were designed for more mature audiences, with little over 5 movies rating G, and more than the majority falling on ratings that require parental guidance. 

The standard used for content produced primarily for the TV was the following: 

TV-Y7: Directed to Older Children. 

TV-Y7 FV: Directed to Older Children \- Fantasy Violence. 

TV-G: General Audience. 

TV-PG: Parental Guidance Suggested.

TV-14: Parents Strongly Cautioned. 

TV-MA: Mature Audience Only.

According to the analysis, similarly to the case with the movies, most of the TV shows added are rated for mature audiences or require parental guidance, almost 2000 titles. A small fraction of the TV shows added were designed for children, below 500 titles. This points to adults and viewers in between 14 and 17 years old being the strongest audience of Netflix content. 

\~Solution: Pivot Table\> rows: ratings, value:count of titles.

\~ Audience & Market Proxy Questions

Since the values in this data are a bit messy, I decided to use SQL to answer the next questions. 

**Which months/quarters see the most new releases added?**

This is the command I used to answer this question:

SELECT EXTRACT(MONTH FROM date\_added) AS month,

       COUNT(\*) AS releases

FROM netflix

GROUP BY month

ORDER BY releases DESC;

Most titles are added in July, December, and January. These dates match the holidays in the south and north hemisphere, with summer/winter releases depending on the side of the world.

**What is the relationship between ratings and runtime?**

SELECT rating,

       AVG(duration\_minutes) AS avg\_runtime\_minutes

FROM netflix

WHERE duration\_minutes LIKE '%min'

GROUP BY rating

ORDER BY avg\_runtime\_minutes DESC;

The average runtime of movies designed specifically for children aged equal or under 7, is mostly under 80 minutes. On the other extreme, NC-17, which are movies to which no one under 17 years old is allowed in cinema sessions, are the longest in the dataset, with an average runtime that falls between 140 and 160 minutes.  

\~Solution: applied the command to SQL, which was more suited to answer this questions because of its complexity, and then transferred the result to Excel to create a pivot chart that could present me with a more clear vision of the results. 

---

\~ Advanced (Critical Thinking / Political Science Angle)

**Which regions dominate Netflix’s catalog vs underrepresented ones?**

As the dataset is not divided by region, I decided to use another route that was more aligned with my current skills. First, I checked the list of which countries have the most titles available. Then, I checked the genre per country using the following command on SQL:

**WITH country\_split AS (**

  **SELECT** 

    **show\_id,**

    **title,**

    **type,**

    **listed\_in,**

    **trim(unnest(string\_to\_array(country, ','))) AS country\_clean**

  **FROM netflix**

  **WHERE country IS NOT NULL**

**)**

**SELECT** 

    **listed\_in AS genre,**

    **COUNT(\*) AS num\_titles**

**FROM country\_split**

**WHERE country\_clean \= 'Japan'**

**GROUP BY listed\_in**

**ORDER BY num\_titles DESC;**

Movies from the US, or that have the US cited in their production, count for more than 50% of the titles in the catalogue. The most represented region is Europe, because it has 5 countries in the top 10 most represented titles. Also in this list we can see India, in the second place, with 2805 titles, Canada with 877, Japan with 733, and South Korea with 632\. 

When we look closer, the majority of titles produced by Japan are listed in international TV show, anime series, international movies, and anime features. Indeed, animes are the most produced genre by this country. India produces mostly drama and comedy. It is not specified whether these productions come from Bollywood, however, titles listed as independent movies comes in third place, which points to the possibility of a growth in the number of Indian movies being produced outside Bollywood. South Korea produces mostly Korean TV shows, and romantic TV shows. Canada in the other hand produces mostly drama, comedy, and Children and family movies. 

The countries that have up to only 3 titles in the catalogue mostly belong to Africa, South Caucasus region of the Caucasus, and Central Asia. 

**How does Netflix’s catalog reflect cultural diversity in genres?**

Using this-\> SELECT listed\_in,

       COUNT(DISTINCT country) AS num\_countries

FROM netflix

WHERE listed\_in IS NOT NULL AND country IS NOT NULL

GROUP BY listed\_in

ORDER BY num\_countries DESC;

I check which genres are more geographically diverse, and it gives me that the top 3 are: International movies (100 countries), drama (92) and documentaries (73). The data has a total of 122 countries. This means that more than the majority are producing their own movies, also dramas and documentaries. This is very good, and it indicates that there is the intention of balancing local productions with the top 2 producer on the data that are the US and India. 

