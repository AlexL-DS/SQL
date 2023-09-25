We have a datebase, which include table about online sales:
https://dsintrodb.skillbox.cc/
Username: student;
Password: VisionDrivesDecision;
Database: skillbox

We have to find the product that customers most often order with [product X].

Let's write a SQL-query


***
SELECT
p.product_id
, count(p.product_id)
FROM orders_product op
JOIN products p
ON op.product_id = p.product_id
JOIN (
SELECT
op.order_id
FROM orders_product op
JOIN products p
ON op.product_id = p.product_id
WHERE p.product_name = [product_X]
) t
ON op.order_id = t.order_id
WHERE p.product_name <> [product_X]
GROUP BY p.product_id
ORDER BY count(p.product_id) DESC
LIMIT 1;
***
