### ERD
![Диаграмма создания заказа](erd.puml)

### Таблица `orders`

| Атрибут     | Ключ | Тип       | Ограничения        | Описание                          |
|-------------|------|-----------|---------------------|-------------------------------------|
| id          | PK   | bigint    | not null, auto increment | Идентификатор заказа           |
| user_id     | FK → users.id | bigint | not null       | Кто оформил заказ                 |
| status_id   | FK → order_statuses.id | smallint | not null | Текущий статус заказа       |
| total_amount| —    | numeric(10,2) | not null, >= 0  | Итоговая сумма заказа              |
| created_at  | —    | timestamp | not null, default now() | Дата создания заказа          |

**Индексы:** `idx_orders_user_id` (по `user_id`, для быстрой выборки заказов пользователя).

### Таблица `order_items`

| Атрибут    | Ключ | Тип     | Ограничения        | Описание                       |
|------------|------|---------|----------------------|-----------------------------------|
| id         | PK   | bigint  | not null, auto increment | Идентификатор строки заказа |
| order_id   | FK → orders.id | bigint | not null      | К какому заказу относится      |
| product_id | FK → products.id | bigint | not null    | Какой товар заказан             |
| quantity   | —    | integer | not null, > 0        | Количество товара                |
| price      | —    | numeric(10,2) | not null, >= 0 | Цена товара на момент заказа    |

### Справочник `order_statuses`

| id | code       | Описание                    |
|----|------------|-------------------------------|
| 1  | created    | Заказ создан, ожидает оплаты  |
| 2  | paid       | Заказ оплачен                 |
| 3  | shipped    | Заказ передан в доставку      |
| 4  | cancelled  | Заказ отменён                 |

---
