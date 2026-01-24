# SQL Build Plan

Goal: Build a clean, order-level SLA fact table and supporting dimensions using reproducible SQL layers.

---

## 01_staging (Raw → Clean)

### stg_orders
Source: olist_orders_dataset  
Purpose: Clean timestamps and standardize order fields.
Key fields:
- order_id
- customer_id
- order_status
- order_purchase_timestamp
- order_approved_at
- order_delivered_carrier_date
- order_delivered_customer_date
- order_estimated_delivery_date

Rules:
- Parse all timestamps to DATETIME
- Keep nulls as nulls (do not fill)
- No aggregations in staging

### stg_order_items
Source: olist_order_items_dataset  
Purpose: Clean numeric fields and preserve item grain.
Key fields:
- order_id
- order_item_id
- product_id
- seller_id
- shipping_limit_date
- price
- freight_value

Rules:
- price and freight_value as numeric
- shipping_limit_date parsed to DATETIME

### stg_customers
Source: olist_customers_dataset  
Key fields:
- customer_id
- customer_unique_id
- customer_city
- customer_state

### stg_sellers
Source: olist_sellers_dataset  
Key fields:
- seller_id
- seller_city
- seller_state

(Optional later)
### stg_products
Source: olist_products_dataset  
- product_id
- product_category_name
- product_weight_g

### stg_category_translation
Source: product_category_name_translation  
- product_category_name
- product_category_name_english

---

## 02_dimensions

### dim_customer
Built from stg_customers
- customer_id (PK)
- customer_unique_id
- customer_city
- customer_state

### dim_seller
Built from stg_sellers
- seller_id (PK)
- seller_city
- seller_state

(Optional)
### dim_product
Built from stg_products (+ translation)
- product_id (PK)
- product_category_name_english
- product_weight_g

---

## 03_facts

### fact_order_fulfillment
Built from stg_orders (+ derived metrics)
Grain: one row per order
Fields:
- order_id (PK)
- customer_id
- order_status
- order_purchase_timestamp
- order_delivered_customer_date
- order_estimated_delivery_date
- is_delivered
- is_late
- days_to_deliver
- days_late

Rules:
- is_delivered = 1 when order_status = 'delivered' and delivered_customer_date is not null
- is_late = 1 when is_delivered = 1 and delivered_customer_date > estimated_delivery_date
- days_to_deliver = date_diff(delivered_customer_date, purchase_timestamp)
- days_late = max(0, date_diff(delivered_customer_date, estimated_delivery_date)) for delivered orders

### bridge_order_item
Built from stg_order_items
Grain: one row per order item
Fields:
- order_id
- order_item_id
- seller_id
- product_id
- price
- freight_value

---

## 04_metrics (KPI Queries for Power BI)

We will compute KPI-ready outputs from fact_order_fulfillment:
- on_time_rate
- late_rate
- avg_days_late
- avg_days_to_deliver
- late_orders_count
- delivered_orders_count
- trend by purchase month
- breakdown by customer_state and seller_state
