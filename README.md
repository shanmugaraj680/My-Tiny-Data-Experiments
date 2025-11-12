#SQL Challenge 1,
Question: Find the Top 5 products based on average sales amount from the previous month.

Dataset
| sale_id | product_name | sale_date  | quantity | total_amount |
| ------- | ------------ | ---------- | -------- | ------------ |
| 1       | Coffee       | 2025-10-02 | 20       | 2500.00      |
| 2       | Tea          | 2025-10-05 | 15       | 1200.00      |
| 3       | Milk         | 2025-09-28 | 30       | 1800.00      |
| 4       | Yogurt       | 2025-10-10 | 10       | 1500.00      |
| 5       | Butter       | 2025-10-12 | 8        | 900.00       |
| 6       | Coffee       | 2025-10-15 | 25       | 3000.00      |
| 7       | Tea          | 2025-10-20 | 10       | 800.00       |
| 8       | Butter       | 2025-09-25 | 5        | 400.00       |
| 9       | Milk         | 2025-10-08 | 20       | 1600.00      |
| 10      | Yogurt       | 2025-10-17 | 15       | 2000.00      |

```sql
MySQL Query
SELECT 
    product_name,
    ROUND(AVG(total_amount), 2) AS avg_sales
FROM sales_data
WHERE sale_date >= DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01')
  AND sale_date < DATE_FORMAT(CURDATE(), '%Y-%m-01')
GROUP BY product_name
ORDER BY avg_sales DESC
LIMIT 5;


###
DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01') → gives the first day of the previous month.

DATE_FORMAT(CURDATE(), '%Y-%m-01') → gives the first day of the current month, used as the upper limit (exclusive).

This filters all sales from the previous month only.
###

Output
| product_name | avg_sales |
| ------------ | --------- |
| Coffee       | 2750.00   |
| Yogurt       | 1750.00   |
| Milk         | 1600.00   |
| Tea          | 1000.00   |
| Butter       | 900.00    |

