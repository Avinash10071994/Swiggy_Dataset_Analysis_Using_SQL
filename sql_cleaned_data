create database swiggy_analysis

use swiggy_analysis

select * from dbo.swiggy

select count(*) as total_records from swiggy

select distinct(city) from swiggy

-- finding out null values present in the features

select
sum(case when name is null then 1 else 0 end) as null_name,
sum(case when city is null then 1 else 0 end) as null_city,
sum(case when rating is null then 1 else 0 end) as null_rating
from
swiggy


select cost from swiggy where cost like 'NA%'

select * from swiggy where rating>4


/* As Data is very messy we clean the data */
 --Start Cleaning 

  -- NULL Value Handling

 select name from swiggy where lic_no is null or rating is null or rating_count is null
 delete from swiggy where lic_no is null or rating is null or rating_count is null;
 delete  from swiggy  where cost like 'NA%';
 delete  from swiggy where cuisine like 'NA%';

 -- check type of cousines

 select distinct(cuisine) from swiggy
 select distinct(city) from swiggy

 update swiggy
 set rating_count =replace(
                      replace(
                     replace(
                      replace(rating_count, '+', ''), 
                        'K', '000'), 
                      'Too Few Ratings', '0'), 
                    'ratings', '');

select * from dbo.swiggy

--2. replace rupee sign to space
update swiggy
set cost=replace(cost,NCHAR(8377),'');

-- 3.replace -- to 0
update  swiggy
set rating = replace(rating, '--', '0');

--Change the datatype
--1.Converting ‘rating_count’ column datatype in ‘int’
alter table swiggy
alter column rating_count INT;

--2.Converting ‘rating’ column datatype in ‘float’
alter table swiggy
alter column cost INT;

--3.Converting ‘rating’ column datatype in ‘float’
alter table swiggy
alter column rating float;

--1.What are the most Popular Cuisines served throughout the dataset ?


select top 10 trim(value) as  Popular_cuisine, count(*) AS Cuisine_count
from swiggy
cross apply string_split (cuisine,',')
group by trim (value)
order by Cuisine_count desc;

--2.What are the top 5 most popular restaurant chains in India in terms of ratings given?


select top 5 name, avg(rating) as Avg_rating
from swiggy
where rating_count>=100
group by name 
order by Avg_rating desc;

--3. Which are those Restaurants that has maximum number of branches ?

select top 5 name, count(city) as total from swiggy
group by name
order by total desc

--4. What are the top 10 cities as per the number of restaurants listed?

select top 10 city, count(name) as total_restaurant from swiggy
group by city order by total_restaurant desc;


--5. What are the Top 5 most popular restaurant chains in India?

select top 5 name, avg(rating) as average_rating from swiggy
group by name
order by average_rating desc

--6.Which city is having the least expensive restaurant in terms of cost?

select top 1 city,  name,
sum(case when cost is null then 0 else cost end) as least_expensive
from swiggy
where cost !=0
group by name,city
order by
least_expensive asc

--7.Number of cities (including subregions) where swiggy is having their restaurants listed? 

select count(distinct(city)) as total_cities from swiggy

--8. Restaurant chain with maximum number of branches?

select top 1 name,count(*) as total_rest
from swiggy
group by name
order by
total_rest desc

