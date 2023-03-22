# linazili-funnels
Funnel Analysis

**1. First, I removed the duplicates to have 1 unique event per user_pseudo_id.**<br>
     SELECT <br>
            user_pseudo_id, event_name, <br> 
            MIN(event_timestamp) event_timestamp    <br>   FROM `turing_data_analytics.raw_events` raw <br>
      GROUP BY 1,2 <br>
      
**2. Aggregated identified events per top 3 countries.**<br>
    WITH dub AS <br>
    (<br>
     SELECT <br>
     user_pseudo_id, event_name, <br>
     MIN(event_timestamp) event_timestamp, country  <br>
     FROM `turing_data_analytics.raw_events` raw<br>
     GROUP BY 1,2,4)<br>
SELECT event_name,<br>
      SUM(CASE WHEN country LIKE "United States"  THEN 1 ELSE 0 END) AS us_events,<br>
      SUM(CASE WHEN country LIKE "India"  THEN 1 ELSE 0 END) AS india_events,<br>
      SUM(CASE WHEN country LIKE "Canada"  THEN 1 ELSE 0 END) AS canada_events<br>
FROM dub<br>
WHERE event_name IN ('user_engagement', 'view_promotion', 'view_item', 'add_to_cart', 'add_payment_info', 'purchase')<br>
GROUP BY 1 <br> 
ORDER BY 2 DESC<br>

**3. Created a sales funnel chart with a country split in top 3 countries.**
