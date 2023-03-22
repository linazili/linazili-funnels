# linazili-funnels
Funnel Analysis

1. First, I removed the duplicates to have 1 unique event per user_pseudo_id.
     *SELECT 
            user_pseudo_id, event_name, 
            MIN(event_timestamp) event_timestamp       
      FROM `turing_data_analytics.raw_events` raw
      GROUP BY 1,2*
      
2. Aggregated identified events per top 3 countries.
    *WITH dub AS 
(
      SELECT 
      user_pseudo_id, event_name, 
      MIN(event_timestamp) event_timestamp, country  
      FROM `turing_data_analytics.raw_events` raw
      GROUP BY 1,2,4)

SELECT event_name,
      SUM(CASE WHEN country LIKE "United States"  THEN 1 ELSE 0 END) AS us_events,
      SUM(CASE WHEN country LIKE "India"  THEN 1 ELSE 0 END) AS india_events,
      SUM(CASE WHEN country LIKE "Canada"  THEN 1 ELSE 0 END) AS canada_events
FROM dub
WHERE event_name IN ('user_engagement', 'view_promotion', 'view_item', 'add_to_cart', 'add_payment_info', 'purchase')
GROUP BY 1
ORDER BY 2 DESC*

4. Created a sales funnel chart with a country split in top 3 countries.
