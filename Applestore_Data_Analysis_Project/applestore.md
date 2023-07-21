**APPLESTORE APPS DATA ANALYSIS**

- Check the number of unique apps in appleStore table table by checking the count of unique ids

```sql
SELECT 
	COUNT(DISTINCT id) AS UniqueIds
FROM PortfolioProject..AppleStore
```

---

- Check the number of unique apps in appleStore_description table by checking the count of unique ids

```sql
SELECT 
	COUNT(DISTINCT id) AS UniqueIds
FROM PortfolioProject..appleStore_description
```

---

-- Check for missing values in key fields of AppleStore table

```sql
SELECT COUNT(*) AS MissingValues 
FROM PortfolioProject..AppleStore
WHERE track_name IS NULL OR user_rating IS NULL OR prime_genre IS null
```
---

-- Check for missing values in key fields of appleStore_description table

```sql
SELECT
	COUNT(*) AS MissingValues 
FROM PortfolioProject..appleStore_description 
WHERE app_desc IS NULL
```
---

- Find out the number of apps per genre

```sql
SELECT
	prime_genre,
	COUNT(prime_genre) AS genreCount
FROM PortfolioProject..AppleStore
GROUP BY prime_genre
ORDER BY genreCount desc
```

---

- Get an overview of apps ratings

```sql
SELECT 
	MIN(user_rating) AS MinUserRating,
	MAX(user_rating) AS MaxUserRating,
	AVG(user_rating) AS AvgUserRating
FROM PortfolioProject..AppleStore
```

---

- Determine whether paid apps have higher ratings than free appsAppleStore

```sql
SELECT 
	AppType,
	COUNT(AppType) AS AppTypeCount,
	AVG(user_rating) AS AvgUserRatings
FROM (
	SELECT 
		user_rating,
		Case
			WHEN price > 0 THEN 'Paid'
			ELSE 'Free'
		END AS AppType
	FROM PortfolioProject..AppleStore
) AS AppTypeTableCount
GROUP BY AppType
Order BY AvgUserRatings DESC
```

---

- Check if apps with more supported languages have higher ratings 

```sql
SELECT 
	LanguageBucket,
	COUNT(LanguageBucket) AS LanguageBucketCount,
	AVG(user_rating) AS AvgUserRatings
FROM (
	SELECT 
		user_rating,
		Case 
			WHEN lang_num < 10 Then '<10 Languages'
			WHEN lang_num Between 10 and 30 Then '10-30 Languages'
			ELSE '>30 Languages'
		END AS LanguageBucket 
	FROM PortfolioProject..AppleStore 
	) AS LanguageBucketTable 
GROUP BY LanguageBucket
Order BY AvgUserRatings DESC

```
---

-- Check genre with low user rating

```sql
SELECT prime_genre,
	   AVG(user_rating) AS AvgUserRatings
FROM AppleStore
GROUP BY prime_genre
ORDER BY AvgUserRatings ASC
LIMIT 10
```

---
- Check if there is correlation between the length of the app description and the user rating

```sql
SELECT 
	description_length_bucket,
	COUNT(description_length_bucket) AS DescLenCount,
	AVG(user_rating) AS AvgUserRatings
FROM (
	SELECT
		user_rating,
		Case
			WHEN len(app_desc) < 500 Then 'Short description'
			WHEN len(app_desc) Between 500 and 1000 Then 'Medium description'
			ELSE 'Long Description'
		END AS description_length_bucket
	FROM PortfolioProject..AppleStore A 
	JOIN 
	PortfolioProject..appleStore_description B
	ON 
	A.id = B.id
) AS DescriptionLength
GROUP By description_length_bucket
Order BY AvgUserRatings DESC
```
---

- Find the average user ratings for each app prime_genre

```sql
SELECT 
	prime_genre,
	AVG(user_rating) AS AvgUserRatings
FROM PortfolioProject..AppleStore 
GROUP BY prime_genre
Order BY AvgUserRatings
```
---

- Find the average user ratings for each app genre with the app names

```sql
SELECT 
	track_name,
	prime_genre
	user_rating,
	AVG(user_rating) over(Partition BY prime_genre) AS AvgUserRatings
FROM PortfolioProject.. AppleStore 
```
---

-- Find out the top rated apps for each app genre

```sql
SELECT 
	track_name,
	user_rating,
	prime_genre,
	rating_count_tot
FROM (
	SELECT 
		track_name,
		user_rating,
		prime_genre,
		rating_count_tot,
		rank() over(Partition BY prime_genre ORDER BY user_rating desc, rating_count_tot desc) AS Rank
	FROM PortfolioProject..AppleStore
) AS X
WHERE X.Rank = 1
Order BY rating_count_tot desc
```
---

- Display a list of all 5 rated apps sorted by prime_genre

```sql
SELECT 
    track_name,
    prime_genre,
    user_rating
FROM PortfolioProject..AppleStore
WHERE user_rating >= 5
ORDER BY prime_genre 
```


    
    
