## Задание
- Получить все заказы в которых встречается нужная категория товара
- Получить все заказы в которых содержится больше 3 товаров
- Получить все заказы в которых больше 3 разных категорий товаров

## Решение
```
SELECT order.*
FRON order
LEFT JOIN Order2Product o2p ON order.uniqId = o2p.order_id
LEFT JOIN Product ON o2p.product_id = product.uniqId
LEFT JOIN Product2Category p2c ON p2c.product_id = product.uniqId
WHERE p2c.category_id = :categoryId
```
```
SELECT order.*
FROM order
LEFT JOIN Order2Product o2p ON order.uniqId = o2p.order_id
GROUP BY order.uniqId
HAVING count(o2p.product_id) > 3
```
```
SELECT tbl.*
FROM (SELECT order.uniqId as uniqId, p2c.category_id as category_id
      FROM odrer
      JOIN Order2Product o2p ON order.uniqId = o2p.order_id
      JOIN Product2Category p2c ON p2c.product_id = o2p.product_id
      GROUP BY order.uniqId, p2c.category_id
) tbl
GROUP BY tbl.uniqId
HAVING count(tbl.category_id) > 3
```
