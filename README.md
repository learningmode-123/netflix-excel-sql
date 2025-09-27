Hi there\!  
This is my second project to enter the field of data analysis. I have recently finished my SQL studies and would like to answer some questions which could help me switch from Excel to SQL when necessary. 

This dataset was download from *kaggle*, and here is the link: [https://shorturl.at/dunsq](https://shorturl.at/dunsq)

It contains all the movies and TV shows added to the Netflix streaming service catalog since 2007 to 2021\. The dataset is divided by: show\_id, type, title, director, cast, country, date\_added, released\_year, rating and duration. In total, there are 8807 unique titles in this dataset. 

I used Power Query to clean the data before using Excel and SQL to analyze it. In the cleaning process I changed cats to actors, because the cast word would confuse SQL, and I split the duration column in duration\_season and duration\_minutes. That was the data I used on SQL.   
That was my schema for the SQL part:

CREATE TABLE netflix (  
    show\_id TEXT NULL,  
    type TEXT NULL,  
    title TEXT NULL,  
    director TEXT NULL,  
    actors TEXT NULL,  
    country TEXT NULL,  
    date\_added TEXT NULL,  
    release\_year INT NULL,  
    rating TEXT NULL,  
    listed\_in TEXT NULL,  
    description TEXT NULL,  
	Duration\_Minutes TEXT NULL,  
	Duration\_Season TEXT NULL  
);

The, I changed the date\_added to date instead of text.

ALTER TABLE netflix  
ALTER COLUMN date\_added TYPE DATE  
USING TO\_DATE(date\_added, 'YYYY-MM-DD');

\~\~\~

This project helped me develop more complex skills, specially in cleaning data, as this was more messy than the ones I were given during my studies. Furthermore, I used the following questions to guide my analysis:

\~ Content & Catalog Analysis

**What’s the yearly trend of titles added to Netflix?**

**What is the split between Movies and TV Shows?**

**Which countries have the most titles available?**

**Which genres dominate Netflix’s catalog?**

\~ Runtime & Format Insights

**What’s the distribution of movie runtimes (minutes)?**  

**What’s the average number of seasons for TV shows?**

\~ Diversity & Representation

**How many unique countries are represented each year?**

**What is the spread of ratings (e.g., PG, R, 16+, etc.) across movies and TV shows?**

\~ Audience & Market Proxy Questions  

**Which months/quarters see the most new releases added?**

**What is the relationship between ratings and runtime?**

\~ Advanced (Critical Thinking / Political Science Angle)

**Which regions dominate Netflix’s catalog vs underrepresented ones?**

**How does Netflix’s catalog reflect cultural diversity in genres?**
