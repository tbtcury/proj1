# proj1
SELECT 
    pcnt.product_category_name_english,
    COUNT(o.order_id) AS orders,
    AVG(DATEDIFF(o.order_delivered_customer_date, o.order_approved_at)) AS average_delivery_time_in_days
FROM
    orders AS o
        LEFT JOIN
    order_items AS oi ON o.order_id = oi.order_id
        LEFT JOIN
    products AS p ON oi.product_id = p.product_id
        LEFT JOIN
    product_category_name_translation AS pcnt ON p.product_category_name = pcnt.product_category_name
WHERE
    o.order_status = 'delivered'
GROUP BY pcnt.product_category_name_english
ORDER BY orders DESC;
