# Google-Apps-on-Playstore
The project contains analysis on Google apps that are on playstore. The project was done using Excel, Power BI, and SQL.

## PROJECT TITLE

Google Apps on Playstore 

## PROJECT OVERVIEW

The data analysis project centers on Google  applications on Play Store, aiming to uncover trends and insights within the app ecosystem. By analyzing diverse app attributes like category, ratings, reviews, and downloads, the project seeks to identify factors contributing to app success. It involves exploring correlations between app size, price, and user engagement metrics to understand user preferences and market trends. Additionally, the project aims to categorize apps based on their performance, identifying key characteristics shared by top-rated or most downloaded apps. Ultimately, this analysis endeavors to offer valuable insights for app developers and stakeholders to make informed decisions in enhancing app performance and market competitiveness within the Google Play Store ecosystem

## DATA SOURCE(S)
[Kaggle](https://www.kaggle.com/datasets/tiquasar/playstore-reviews-google-apps?select=app_details.csv)

## TOOLS
- Microsoft Excel
- Microsoft Power BI 
  - [LINK TO DASHBOARD](https://app.powerbi.com/view?r=eyJrIjoiYzJhYTNlMmQtNzc5Ni00ZjgwLWIyZjQtMWY1NmJkOGMzMmEzIiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9)
- Tableau 
  - [LINK TO DASHBOARD](https://public.tableau.com/app/profile/kehinde.alamutu/viz/GoogleappsonPlaystore/Dashboard1?publish=yes)
- SQL

## TYPE OF ANALYSIS DONE

The analysis of Google Play Store app data encompasses various types of analyses, including:

- Descriptive Analysis:This involves summarizing and describing the dataset's characteristics, such as the distribution of app categories, average ratings, and download counts. Descriptive statistics provide an initial understanding of the data's features and allow for easy interpretation.

- Correlation Analysis: Exploring relationships between different app attributes like ratings, reviews, app size, and price involves correlation analysis. Determining if certain attributes are positively, negatively, or neutrally correlated helps identify patterns and dependencies within the dataset.

- Segmentation Analysis: Grouping apps based on specific criteria, such as high-rated apps, most downloaded apps, or apps within certain categories, involves segmentation analysis. This helps in understanding distinct characteristics or commonalities among different app groups.

- Trend Analysis: Examining changes and patterns over time in app ratings, downloads, or user reviews allows for trend analysis. This analysis can identify emerging trends or shifts in user preferences within the Google Play Store ecosystem.

Overall, the project involves a comprehensive approach combining descriptive, correlation, segmentation, and trend analyses to extract meaningful insights crucial for understanding app performance factors and aiding decision-making for app developers and stakeholders in the competitive Google Play Store market.

## DATA ANALYSIS
```SQL
--What are the most installed Google apps?
SELECT TOP 5 title, installs, price, androidversion, size, containsAds FROM app_details
ORDER BY installs DESC;

--What is the average rating,score and review of Google apps?
SELECT AVG(ratings) AS AverageRating,ROUND(AVG(score),2) AS AverageScore,AVG(reviews) AS AverageReview FROM app_details;

--Which Google app has the most review?
SELECT TOP 1 * FROM app_details
ORDER BY reviews DESC;

--Which android version install Google apps the most?
SELECT androidversion, COUNT(installs) AS NumberOfInstalls FROM app_details
GROUP BY androidVersion
ORDER BY NumberOfInstalls DESC;

--Give details about the developers of Google apps and the number of apps they develop
SELECT developer,developeraddress,COUNT(title) AS NumberOfAppsDeveloped FROM app_details
GROUP BY developer,developerAddress;

--Which years were Google apps released?
SELECT title,YEAR(released) AS ReleaseYear  FROM app_details
ORDER BY ReleaseYear;


--What is the ratio of Google apps that support ads to those that do not?
SELECT 
	CASE adSupported
		WHEN 1 THEN 'Supports ads'
	ELSE 'Ads not supported'
	END adsupported,
COUNT(title) AS apps FROM app_details
GROUP BY adsupported;

--What are the categories of content rating in Google apps?
SELECT contentRatingDescription,title AS apps FROM app_details
GROUP BY contentRatingDescription,title;

--Are Google apps free or paid?
SELECT free,COUNT(title) AS apps FROM app_details
GROUP BY free;

--What are the genres of Google apps and which of them is most installed?
SELECT genre,COUNT(installs) As install FROM app_details
GROUP BY genre
ORDER BY install DESC;

--What are the apps with good user reviews?
SELECT title,thumbsUpCount FROM app_details
JOIN User_reviews ON app_details.appid=User_reviews.appid
ORDER BY thumbsUpCount DESC;

--What is average score given to Google apps from users' review?
SELECT AVG(u.score) AS AverageScore,a.title 
FROM User_reviews u
JOIN app_details a
ON u.appid=a.appid
GROUP BY a.title
ORDER BY AverageScore DESC;

--How many Google app users replied in users' review?
SELECT COUNT(replycontent) FROM User_reviews;
```
## RESULTS
Upon analyzing the Google Play Store app data, several key insights emerged.The analysis revealed that popular Google Play Store apps tend to focus on specific features or categories, leading to higher installations. Users highly rate apps with better experiences and functionality, emphasizing the importance of user satisfaction. Apps compatible with prevalent Android versions tend to attract more installations, highlighting the significance of adapting to users' devices. Understanding user preferences in content categories and maintaining adherence to ratings are crucial for broader audience reach. The findings underline the need for continuous improvement and diversity in app offerings to meet varying user demands within the Google app ecosystem.

## RECOMMENDATIONS
To capitalize on these insights, it is recommended to focus on enhancing user engagement by leveraging attributes positively correlated with app success. Implementing strategies aligned with percieved insights could potentially boost app downloads and ratings. Category-specific strategies tailored to the characteristics identified in segmentation analysis might significantly impact app performance. Continuous monitoring and adaptation to evolving trends are advised to ensure alignment with changing user preferences.
Based on the analysis of Google apps' data, understanding top-installed apps' success factors should be prioritized. User experience based on average ratings and reviews should also be enhanced. Actively engage with user feedback, optimize app compatibility for prevalent Android versions, and diversify app offerings in popular genres while maintaining adherence to content ratings. Continuously monitor user feedback, recognize high-quality apps, and iterate on development strategies for sustained competitiveness and user satisfaction within the Google app ecosystem.

## LIMITATIONS
Several limitations must be acknowledged in this analysis. Incomplete and missing data entries have potentially influenced the accuracy of the findings. Additionally, some of the apps do not include date in which they had to be researched for and replaced. 

## REFERENCES
The analysis was based on two datasets obtained from Kaggle. Furthermore, insights were drawn by viewing the datasets on Microsoft Excel and SQL while visualisations where done on Power BI.






