# udemy_sql_questions_queries
## I created these questions and answered them using SQL queries based on metric data from Udemy courses, originally published through Kaggle.com
## https://www.kaggle.com/jilkothari/finance-accounting-courses-udemy-13k-course
	
--What is the total number of courses offered?	

	SELECT COUNT(*) 
	FROM udemy_raw_data 

--How many courses are paid vs. free?	

	﻿SELECT is_paid, COUNT(*) 
	FROM udemy_raw_data 
	GROUP BY 1
	
--How many subscriptions have been made?

	SELECT sum(num_subscribers)
	FROM udemy_raw_data
	
--How many subscriptions are sold vs. free?	

	﻿SELECT is_paid, sum(num_subscribers)
	FROM udemy_raw_data
	GROUP BY 1
	
--How many courses have ratings vs. no ratings?	

	﻿SELECT 
	  CASE 
	    WHEN num_reviews > 0 THEN '> 0' 
	    ELSE '0' 
	    END as '0 COUNT',
	  COUNT(*)
	FROM udemy_raw_data
	GROUP BY 1

--How many courses have lectures vs. no lectures?	

	﻿SELECT 
	  CASE 
	    WHEN num_published_lectures > 0 THEN '> 0' 
	    ELSE '0' 
	    END as '0 COUNT',
	  COUNT(*)
	FROM udemy_raw_data
	GROUP BY 1
	
--How many courses have tests vs. no tests?	

	﻿SELECT 
	  CASE 
	    WHEN num_published_practice_tests > 0 THEN '> 0' 
	    ELSE '0' 
	    END as '0 COUNT',
	  COUNT(*)
	FROM udemy_raw_data
	GROUP BY 1
	
--How many courses have a discount vs. no discount?	

	﻿SELECT 
	  CASE 
	    WHEN discount_price__amount> 0 THEN '> 0' 
	    ELSE '0' 
	    END as '0 COUNT',
	  COUNT(*)
	FROM udemy_raw_data
	GROUP BY 1
	
--What is the highest price for a course (USD)?	

	﻿SELECT MAX(price_detail__amount)*0.014
	FROM udemy_raw_data

--What is the most number of lectures in one course?	

	﻿SELECT MAX(num_published_lectures)
	FROM udemy_raw_data

--What is the most number of tests in one course?
	
	﻿SELECT MAX(num_published_practice_tests)
	FROM udemy_raw_data

--What is the highest average rating for a course?
	
	﻿SELECT MAX(avg_rating)
	FROM udemy_raw_data

--What is highest number of subscriptions for one course?	

	﻿SELECT MAX(num_subscribers)
	FROM udemy_raw_data

--What is highest number of reviews for one course?	

	﻿SELECT MAX(num_reviews)
	FROM udemy_raw_data

--What is the highest course value?	

	﻿SELECT (price_detail__amount*num_subscribers*.014) as course_value
	FROM udemy_raw_data
	ORDER BY 1
	DESC
	LIMIT 1
	
--What is the average & total number of subscriptions each year?	
		
	SELECT 
	COUNT(title) as courses_created_per_year, 
	round(AVG(num_subscribers), 2)
	sum(num_subscribers), 2)
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 4
	
--What is the total number of courses offered each year?	

	SELECT 
	COUNT(title) as courses_created_per_year, 
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 2
	
--What is the average number of subscriptions made a year?	

	SELECT 
	COUNT(title)
	AVG(num_subscribers)
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 2
	
--What is the average number of subscriptions made per course?	

	﻿SELECT AVG(num_subscribers)
	FROM udemy_raw_data

--What is the average number of subscriptions made per course per year?	

	SELECT (sum(num_subscribers/10.5)
	FROM udemy_raw_data
	
--What is the average rating for paid vs. free courses?	

	﻿SELECT is_paid, AVG(avg_rating)
	FROM udemy_raw_data
	WHERE num_reviews>0
	GROUP BY 1
	
--What is the average rating per course in price category?	

	﻿SELECT
	CASE
	WHEN (price_detail__amount*0.014) = 0 THEN 'free'
	WHEN (price_detail__amount*0.014) > 0 AND (price_detail__amount*0.014)  < 15 THEN '0' 
	WHEN (price_detail__amount*0.014) >= 15 AND (price_detail__amount*0.014) < 30 THEN 15 
	WHEN (price_detail__amount*0.014) >= 30 AND (price_detail__amount*0.014) < 45 THEN 30 
	WHEN (price_detail__amount*0.014) >= 45 AND (price_detail__amount*0.014) < 60 THEN 45 
	WHEN (price_detail__amount*0.014) >= 60 AND (price_detail__amount*0.014) < 75 THEN 60
	WHEN (price_detail__amount*0.014) >= 75 AND (price_detail__amount*0.014) < 90 THEN 75 
	WHEN (price_detail__amount*0.014) >= 90 AND (price_detail__amount*0.014) < 105 THEN 90 
	WHEN (price_detail__amount*0.014) >= 105 AND (price_detail__amount*0.014) < 120 THEN 105
	WHEN (price_detail__amount*0.014) >= 120 AND (price_detail__amount*0.014) < 135 THEN 120 
	WHEN (price_detail__amount*0.014) >= 135 AND (price_detail__amount*0.014) < 150 THEN 135 
	WHEN (price_detail__amount*0.014) >= 150 AND (price_detail__amount*0.014) < 165 THEN 150 
	WHEN (price_detail__amount*0.014) >= 165 AND (price_detail__amount*0.014) < 180 THEN 165
	WHEN (price_detail__amount*0.014) >= 180 THEN 180
	ELSE 'null'
	END as price_category,
	COUNT(title),
	AVG(avg_rating)
	FROM udemy_raw_data
	GROUP BY 1
	ORDER BY 1
	
--What is the average rating for the course value?
	
	﻿SELECT 
	CASE 
	WHEN (price_detail__amount*num_subscribers*0.014) = 0 THEN '0'
	WHEN (price_detail__amount*num_subscribers*0.014) > 0 AND (price_detail__amount*num_subscribers*0.014) <= 50000 THEN 0
	WHEN (price_detail__amount*num_subscribers*0.014) > 50000 AND (price_detail__amount*num_subscribers*0.014) <= 100000 THEN 50000
	WHEN (price_detail__amount*num_subscribers*0.014) > 100000 AND (price_detail__amount*num_subscribers*0.014)<= 500000 THEN 100000
	WHEN (price_detail__amount*num_subscribers*0.014) > 500000 AND (price_detail__amount*num_subscribers*0.014)<= 1000000 THEN 500000
	WHEN (price_detail__amount*num_subscribers*0.014) > 1000000 AND (price_detail__amount*num_subscribers*0.014) <= 5000000 THEN 1000000
	WHEN (price_detail__amount*num_subscribers*0.014) > 5000000 AND (price_detail__amount*num_subscribers*0.014)<= 10000000 THEN 5000000
	WHEN (price_detail__amount*num_subscribers*0.014) > 10000000 AND (price_detail__amount*num_subscribers*0.014)<= 50000000 THEN 10000000
	WHEN (price_detail__amount*num_subscribers*0.014) > 50000000 AND (price_detail__amount*num_subscribers*0.014)<= 100000000 THEN 50000000
	WHEN (price_detail__amount*num_subscribers*0.014) > 100000000 AND (price_detail__amount*num_subscribers*0.014)<= 500000000 THEN 100000000
	ELSE 'null'
	END as course_value_cat, round(AVG(avg_rating), 2), COUNT(title)
	FROM udemy_raw_data
	WHERE num_reviews>0 AND is_paid like 'TRUE'
	GROUP BY 1
	ORDER BY 1 ASC
	
--What is the average rating of a course per year?
	
	SELECT 
	COUNT(title) as courses_created_per_year, 
	round(AVG(avg_rating), 2)
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 4

--What is the average rating of a course for number of tests?	

	﻿SELECT num_published_practice_tests, COUNT(num_published_practice_tests), AVG(avg_rating)
	FROM udemy_raw_data
	WHERE num_reviews>0
	GROUP BY 1
	
--What is the average rating of a course for number of lectures?	

	﻿SELECT num_published_lectures, COUNT(num_published_lectures), AVG(avg_rating)
	FROM udemy_raw_data
	WHERE num_reviews>0
	GROUP BY 1
	
	
	
--What is the average number of subscribers per price category	

	﻿SELECT
	CASE
	WHEN (price_detail__amount*0.014) = 0 THEN 'free'
	WHEN (price_detail__amount*0.014) > 0 AND (price_detail__amount*0.014)  < 15 THEN '0' 
	WHEN (price_detail__amount*0.014) >= 15 AND (price_detail__amount*0.014) < 30 THEN 15 
	WHEN (price_detail__amount*0.014) >= 30 AND (price_detail__amount*0.014) < 45 THEN 30 
	WHEN (price_detail__amount*0.014) >= 45 AND (price_detail__amount*0.014) < 60 THEN 45 
	WHEN (price_detail__amount*0.014) >= 60 AND (price_detail__amount*0.014) < 75 THEN 60
	WHEN (price_detail__amount*0.014) >= 75 AND (price_detail__amount*0.014) < 90 THEN 75 
	WHEN (price_detail__amount*0.014) >= 90 AND (price_detail__amount*0.014) < 105 THEN 90 
	WHEN (price_detail__amount*0.014) >= 105 AND (price_detail__amount*0.014) < 120 THEN 105
	WHEN (price_detail__amount*0.014) >= 120 AND (price_detail__amount*0.014) < 135 THEN 120 
	WHEN (price_detail__amount*0.014) >= 135 AND (price_detail__amount*0.014) < 150 THEN 135 
	WHEN (price_detail__amount*0.014) >= 150 AND (price_detail__amount*0.014) < 165 THEN 150 
	WHEN (price_detail__amount*0.014) >= 165 AND (price_detail__amount*0.014) < 180 THEN 165
	WHEN (price_detail__amount*0.014) >= 180 THEN 180
	ELSE 'null'
	END as price_category,
	COUNT(title),
	AVG(num_subscribers)
	FROM udemy_raw_data
	GROUP BY 1
	ORDER BY 1
	
--What is the total number of subscriptions in each price category?	

	﻿SELECT
	CASE
	WHEN (price_detail__amount*0.014) = 0 THEN 'free'
	WHEN (price_detail__amount*0.014) > 0 AND (price_detail__amount*0.014)  < 15 THEN '0' 
	WHEN (price_detail__amount*0.014) >= 15 AND (price_detail__amount*0.014) < 30 THEN 15 
	WHEN (price_detail__amount*0.014) >= 30 AND (price_detail__amount*0.014) < 45 THEN 30 
	WHEN (price_detail__amount*0.014) >= 45 AND (price_detail__amount*0.014) < 60 THEN 45 
	WHEN (price_detail__amount*0.014) >= 60 AND (price_detail__amount*0.014) < 75 THEN 60
	WHEN (price_detail__amount*0.014) >= 75 AND (price_detail__amount*0.014) < 90 THEN 75 
	WHEN (price_detail__amount*0.014) >= 90 AND (price_detail__amount*0.014) < 105 THEN 90 
	WHEN (price_detail__amount*0.014) >= 105 AND (price_detail__amount*0.014) < 120 THEN 105
	WHEN (price_detail__amount*0.014) >= 120 AND (price_detail__amount*0.014) < 135 THEN 120 
	WHEN (price_detail__amount*0.014) >= 135 AND (price_detail__amount*0.014) < 150 THEN 135 
	WHEN (price_detail__amount*0.014) >= 150 AND (price_detail__amount*0.014) < 165 THEN 150 
	WHEN (price_detail__amount*0.014) >= 165 AND (price_detail__amount*0.014) < 180 THEN 165
	WHEN (price_detail__amount*0.014) >= 180 THEN 180
	ELSE 'null'
	END as price_category,
	COUNT(title),
	sum(num_subscribers)
	FROM udemy_raw_data
	GROUP BY 1
	ORDER BY 1
	ASC
	
--What is the total number of courses offered in each price category?	

	﻿SELECT
	CASE
	WHEN (price_detail__amount*0.014) = 0 THEN 'free'
	WHEN (price_detail__amount*0.014) > 0 AND (price_detail__amount*0.014)  < 15 THEN '0' 
	WHEN (price_detail__amount*0.014) >= 15 AND (price_detail__amount*0.014) < 30 THEN 15 
	WHEN (price_detail__amount*0.014) >= 30 AND (price_detail__amount*0.014) < 45 THEN 30 
	WHEN (price_detail__amount*0.014) >= 45 AND (price_detail__amount*0.014) < 60 THEN 45 
	WHEN (price_detail__amount*0.014) >= 60 AND (price_detail__amount*0.014) < 75 THEN 60
	WHEN (price_detail__amount*0.014) >= 75 AND (price_detail__amount*0.014) < 90 THEN 75 
	WHEN (price_detail__amount*0.014) >= 90 AND (price_detail__amount*0.014) < 105 THEN 90 
	WHEN (price_detail__amount*0.014) >= 105 AND (price_detail__amount*0.014) < 120 THEN 105
	WHEN (price_detail__amount*0.014) >= 120 AND (price_detail__amount*0.014) < 135 THEN 120 
	WHEN (price_detail__amount*0.014) >= 135 AND (price_detail__amount*0.014) < 150 THEN 135 
	WHEN (price_detail__amount*0.014) >= 150 AND (price_detail__amount*0.014) < 165 THEN 150 
	WHEN (price_detail__amount*0.014) >= 165 AND (price_detail__amount*0.014) < 180 THEN 165
	WHEN (price_detail__amount*0.014) >= 180 THEN 180
	ELSE 'null'
	END as price_category,
	COUNT(title)
	FROM udemy_raw_data
	GROUP BY 1
	ORDER BY 1
	
	
	
--What is the average number of subscribers for a paid course vs. free?	

	﻿SELECT is_paid, AVG(num_subscribers)
	FROM udemy_raw_data
	GROUP BY 1

--What is the average number of free courses created per year	

	SELECT 
	COUNT(title) as courses_created_per_year, 
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 2
	
--What is the average price of a course	
	
	﻿SELECT AVG(price_detail__amount*0.014)
	FROM udemy_raw_data
	WHERE is_paid like 'TRUE'

--What is the average number of lectures per course?
	
	﻿SELECT AVG(num_published_lectures)
	FROM udemy_raw_data
	
--What is the average number of tests per course?
	
	﻿SELECT AVG(num_published_practice_tests)
	FROM udemy_raw_data

--What is the average rating per course?	
	﻿SELECT AVG(avg_rating)
	FROM udemy_raw_data
	WHERE num_reviews >0

--What is the average course value?	

	﻿SELECT AVG(price_detail__amount*num_subscribers*0.014)
	FROM udemy_raw_data
	WHERE is_paid like 'TRUE'
	
--What is the average course value per lecture?	

	﻿SELECT is_paid, num_published_lectures, round(AVG(price_detail__amount*num_subscribers*0.014), 2)
	FROM udemy_raw_data
	WHERE is_paid like 'TRUE'
	GROUP BY 2
	
--What is the average course value per test?	

	﻿SELECT is_paid, num_published_practice_tests, 
        round(AVG(price_detail__amount*num_subscribers*0.014), 2)
	FROM udemy_raw_data
	WHERE is_paid like 'TRUE'
	GROUP BY 2
	
--What is the average & total course value per year?	

	SELECT 
	COUNT(title) as courses_created_per_year, 
	round(sum(price_detail__amount*num_subscribers*0.014), 2) as total_course_value, 
	round(AVG(price_detail__amount*num_subscribers*0.014), 2) as avg_course_value,
	CASE
	WHEN created like '2020%' THEN '2020'
	WHEN created like '2019%' THEN '2019'
	WHEN created like '2018%' THEN '2018'
	WHEN created like '2017%' THEN '2017'
	WHEN created like '2016%' THEN '2016'
	WHEN created like '2015%' THEN '2015'
	WHEN created like '2014%' THEN '2014'
	WHEN created like '2013%' THEN '2013'
	WHEN created like '2012%' THEN '2012'
	WHEN created like '2011%' THEN '2011'
	WHEN created like '2010%' THEN '2010'
	ELSE 'null'
	END as year
	FROM udemy1
	WHERE is_paid = 'TRUE'
	GROUP BY 4
	
--What is the average course value for discounted courses vs. not?
	
	﻿SELECT discount_price__amount, round(AVG(price_detail__amount*num_subscribers*0.014), 2)
	FROM udemy_raw_data
	GROUP BY discount_price__amount > 0
	
--What is the average price of a course per lecture?
	
	﻿SELECT num_published_lectures, COUNT(title), AVG(price_detail__amount)
	FROM udemy_raw_data
	GROUP BY 1
	
--What is the average price of a course per test?	

	﻿SELECT num_published_practice_tests, COUNT(title), AVG(price_detail__amount)
	FROM udemy_raw_data
	GROUP BY 1
	
--What is the average price of a course per rating?
	
	﻿SELECT COUNT(title), AVG(price_detail__amount)
	FROM udemy_raw_data
	GROUP BY 1	
	
--What is the average price of a course per number of subscriptions?	

	﻿SELECT num_subscribers, AVG(price_detail__amount), COUNT(title)
	FROM udemy_raw_data
	GROUP BY 1
	
--How many courses have zero subscriptions?
	
	﻿SELECT COUNT(title)
	FROM udemy_raw_data
	WHERE num_subscribers = '0'

--How many courses have no reviews?	

	﻿SELECT COUNT(title)
	FROM udemy_raw_data
	WHERE num_reviews = '0'
	
