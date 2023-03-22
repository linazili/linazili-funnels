# linazili-funnels
Funnel Analysis

1. First, I removed the duplicates to have 1 unique event per user_pseudo_id.
     *SELECT 
            user_pseudo_id, event_name, 
            MIN(event_timestamp) event_timestamp       
      FROM `turing_data_analytics.raw_events` raw
      GROUP BY 1,2*
      
2. Aggregated identified events per top 3 countries.
3. Created a sales funnel chart with a country split in top 3 countries.
