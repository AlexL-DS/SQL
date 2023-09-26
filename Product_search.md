# SQL Query for Finding Products Often Ordered with [product X]

## Introduction
This SQL query is designed to find the product that customers most often order with a given product (referred to as [product X]). It retrieves this information from a database containing online sales data.

Database contains tables *orders_product* and *products*

## SQL Query

```sql
SELECT
    p.product_id,
    COUNT(p.product_id) AS order_count
FROM
    orders_product op
JOIN
    products p ON op.product_id = p.product_id
JOIN (
    SELECT
        op.order_id
    FROM
        orders_product op
    JOIN
        products p ON op.product_id = p.product_id
    WHERE
        p.product_name = '[product_X]'
) t ON op.order_id = t.order_id
WHERE
    p.product_name <> '[product_X]'
GROUP BY
    p.product_id
ORDER BY
    order_count DESC
LIMIT 1;
```
