# ECommerce Website Analysis

**Situation** I'm working as a data analyst for an ecommerce company. Time period is 2012 - 2015. The following analysis need to be made in order to show that the company is growing in terms of revenue, orders, and website sessions. 

I used MYSQL to do my SQL queries and house my data. Google Looker Studio was used to visualize the results. 

Google looker studio dashboard can be found <a href="https://lookerstudio.google.com/u/0/reporting/f52d1e60-158b-491a-b419-144e640c4386/page/HSSMD"> here </a>

### 1.  Pull overall session and order volume, trended by quarter for the life of the business. 

```SQL
SELECT 
    year(website_sessions.created_at) AS yr,
    quarter(website_sessions.created_at) AS qtr,
    COUNT(DISTINCT website_sessions.website_session_id) AS sessions, 
    COUNT(DISTINCT orders.order_id) AS orders
FROM 
	website_sessions
		LEFT JOIN orders
			ON website_sessions.website_session_id = orders.website_session_id 
WHERE 
	website_sessions.created_at <= '2015-03-20'
GROUP BY 
	1,2;
```

<img src="Q1.jpg">

Fourth quarter is always the strongest quarter for the company in terms of website sessions and orders. 

### 2.Quarterly figures since launching for session-to-order conversion rate, revenue per order, revenue per session.

