Create Table appleStore_description_combined AS 

Select * from appleStore_description1

union all 

select * From appleStore_description2

Union all 

select * From appleStore_description3

union all 

select * from appleStore_description4


**EXPLORATORY DATA ANALYSIS**

-- Check the number of unique apps in appleStore table by checking the count of unique ids

Select count(DISTINCT id) as UniqueAppsIDs 
From AppleStore 

-- Check the number of unique apps in appleStore_description_combined table by checking the count of unique ids

select Count(DISTINCT id) as uniqueAppsIDs
from appleStore_description_combined 

-- Check for any missing values in key fields

select count(*) as MissingValues 
from AppleStore
where track_name is null or user_rating is null or prime_genre is null 

select count(*) as MissingValues 
from appleStore_description_combined 
where app_desc is null 

-- Find out the number of apps per genre

select prime_genre, count(*) as genreCount
from AppleStore
group by prime_genre 
order by genreCount DESC

-- Get an overview of apps ratings

Select min(user_rating) as MinUserRating,
	   max(user_rating) as MaxUserRating,
       avg(user_rating) as AvgUserRating
From AppleStore

-- Determine whether paid apps have higher ratings than free appsAppleStore
Select CASE
	When price > 0 then 'Paid'
    ELSE 'Free'
End as AppType,
avg(user_rating) as AvgUserRatings
From AppleStore
Group by AppType
order by AvgUserRatings DESC

-- Check if apps with more supported languages have higher ratings 

Select case 
          When lang_num < 10 Then '<10 languages'
          When lang_num BETWEEN 10 and 30 Then '10-30 languages'
          ELSE '>30 languages'
	   end as language_bucket,
       avg(user_rating) as AvgUserRatings
From AppleStore
Group by language_bucket
order by AvgUserRatings DESC

select prime_genre,
	   avg(user_rating) as AvgUserRatings
From AppleStore
Group by prime_genre
order by AvgUserRatings ASC
LIMIT 10 

-- Check if there is correlation between the length of the app description and the user rating

Select 
	Case 
    	When length(B.app_desc) < 500 Then 'Short description'
        When length(B.app_desc) between 500 and 1000 Then 'Medium description'
        else 'Long description' 
    End as description_length_bucket,
    avg(user_rating) as AvgUserRatings
From 
	AppleStore as A 
Join 
	appleStore_description_combined as B 
On 
	A.id = B.id 
Group by description_length_bucket
Order by AvgUserRatings desc 

-- Find the average user ratings for each app prime_genre

select 
	track_name,
    prime_genre,
    user_rating,
	avg(user_rating) over(partition by prime_genre) as Avg_User_Ratings
From AppleStore

-- Check the top rated apps for each genre 

select 
	prime_genre,
    track_name,
    user_rating,
    rating_count_tot
From (
    select 
        prime_genre,
        track_name,
        user_rating,
        rating_count_tot,
        rank() over (partition by prime_genre order by user_rating DESC, rating_count_tot DESC) as rank 
    From AppleStore
  	) as x
Where x.rank = 1
  

-- Display a list of all 5 rated apps sorted by prime_genre

select 
	track_name,
    prime_genre,
    user_rating
From AppleStore
where 
	user_rating >= 5
order by prime_genre 

-- Assuming that apps added previously to the applestore have a lower app id than apps added later on, 
-- Find the first two apps that was added on each prime_genreAppleStore

select * from (
  select 
      id,
      track_name,
      prime_genre,
      user_rating,
      row_number() over(partition by prime_genre order by id) as rn
  From AppleStore a
) x 
where x.rn < 3


    
    
