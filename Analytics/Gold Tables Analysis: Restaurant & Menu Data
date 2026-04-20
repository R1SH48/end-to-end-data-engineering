# Table Overview

SELECT
  'gold_cuisine_by_city' as table_name,
  COUNT(*) as row_count,
  COUNT(DISTINCT `city_name`) as unique_cities,
  COUNT(DISTINCT `top_cuisines`) as unique_cuisines,
  SUM(`total_restaurant`) as total_restaurants
FROM
  `dbacademy`.`dbuser_100426`.`gold_cuisine_by_city`
UNION ALL
SELECT
  'gold_city_by_cuisine' as table_name,
  COUNT(*) as row_count,
  COUNT(DISTINCT `top_cities`) as unique_cities,
  COUNT(DISTINCT `cuisines`) as unique_cuisines,
  SUM(`total_restaurant`) as total_restaurants
FROM
  `dbacademy`.`dbuser_100426`.`gold_city_by_cuisine`
UNION ALL
SELECT
  'gold_price_analysis_by_cuisine' as table_name,
  COUNT(*) as row_count,
  NULL as unique_cities,
  COUNT(DISTINCT `cuisines`) as unique_cuisines,
  SUM(`total_restaurants`) as total_restaurants
FROM
  `dbacademy`.`dbuser_100426`.`gold_price_analysis_by_cuisine`
UNION ALL
SELECT
  'gold_restaurant_price_by_city' as table_name,
  COUNT(*) as row_count,
  COUNT(DISTINCT `city_name`) as unique_cities,
  NULL as unique_cuisines,
  SUM(`total_restaurants`) as total_restaurants
FROM
  `dbacademy`.`dbuser_100426`.`gold_restaurant_price_by_city`
UNION ALL
SELECT
  'gold_menu_price_by_city' as table_name,
  COUNT(*) as row_count,
  COUNT(DISTINCT `city_name`) as unique_cities,
  NULL as unique_cuisines,
  SUM(`total_items`) as total_restaurants
FROM
  `dbacademy`.`dbuser_100426`.`gold_menu_price_by_city`

The gold tables are organized into complementary analytical views:

# 1. gold_cuisine_by_city (565 rows)
Shows the top cuisine in each city with restaurant counts. Covers 565 unique cities with 22 distinct top cuisines. Chinese cuisine dominates as the top cuisine in most cities, including major metros like Delhi, Dehradun, and Mughalsarai. [3]

# 2. gold_city_by_cuisine (194 rows)
Inverse view showing the top city for each cuisine type. Identifies 194 unique cuisines across 85 cities, revealing regional specializations (e.g., Kerala cuisine peaks in Kochi with 221 restaurants, Goan cuisine in Central Goa with 203 restaurants). [4]

# 3. gold_price_analysis_by_cuisine (194 rows)
Aggregates average dining costs and restaurant counts by cuisine. Reveals pricing patterns from budget options (South Indian at ₹242 avg) to premium cuisines (Thai at ₹797 avg). [5]

# 4. gold_restaurant_price_by_city (565 rows)
City-level restaurant pricing with min/max/average cost for two. Shows significant price variation—Central Goa averages ₹484 while Mughalsarai averages ₹243. [1]

# 5. gold_menu_price_by_city (566 rows)
Menu item-level pricing by city. Tracks 11.2M menu items with average prices ranging from ₹416 (Charkhi Dadri) to lower-cost cities. [2]
Key Insights


# Cuisine Market Dominance

Chinese cuisine leads with 29,626 restaurants (18% of total), generating an estimated market value of ₹8.3M based on average costs. North Indian (14,349) and Biryani (13,186) follow as the next largest segments.

# Top Restaurant Markets

15 cities have reached the 2,000-restaurant threshold, led by Surat, Ahmedabad, Kochi, Kanpur, and Hyderabad. Central Goa stands out with the highest average cost (₹484) while maintaining 2,000 restaurants, indicating a premium dining market.

# Pricing Patterns

The scatter analysis reveals that volume doesn't dictate pricing—Chinese cuisine has the highest restaurant count but maintains mid-range pricing (₹279 avg), while specialty cuisines like Thai (₹797) and Japanese (₹693) command premium prices despite smaller footprints.

SELECT
  `cuisines`,
  `total_restaurants`,
  `avg_cost_for_two`,
  ROUND(`avg_cost_for_two` * `total_restaurants`, 2) as total_market_value
FROM
  `dbacademy`.`dbuser_100426`.`gold_price_analysis_by_cuisine`
WHERE
  `total_restaurants` >= 100
ORDER BY
  `total_restaurants` DESC
LIMIT 15

# Restaurant vs Menu Pricing Correlation

Comparing restaurant-level costs to menu item prices shows a consistent 1.1-1.3x ratio across major cities, suggesting menu prices are a reliable predictor of overall dining costs. Central Goa shows the highest ratio (1.65x), indicating either multi-course dining or premium beverage markups.

SELECT
  r.`city_name`,
  r.`total_restaurants`,
  r.`avg_cost_for_two` as avg_restaurant_cost,
  m.`avg_price` as avg_menu_price,
  m.`total_items` as total_menu_items,
  ROUND(r.`avg_cost_for_two` / NULLIF(m.`avg_price`, 0), 2) as price_ratio
FROM
  `dbacademy`.`dbuser_100426`.`gold_restaurant_price_by_city` r
    JOIN `dbacademy`.`dbuser_100426`.`gold_menu_price_by_city` m
      ON r.`city_name` = m.`city_name`
WHERE
  r.`total_restaurants` >= 500
ORDER BY
  r.`total_restaurants` DESC
LIMIT 15



