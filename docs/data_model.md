# Data Model

This project uses a star-schema approach centered on an order-level fact table for SLA performance.

## Fact Table: fact_order_fulfillment

**Grain:** One row per order  
**Primary key:** order_id  
**Purpose:** Stores order-level timestamps and SLA outcome used to measure delivery performance.

### Columns (Minimum)
- order_id (PK)
- customer_id (FK → dim_customer)
- order_status
- order_purchase_timestamp
- order_approved_at
- order_delivered_carrier_date
- order_delivered_customer_date
- order_estimated_delivery_date
- is_delivered (1 if delivered, else 0)
- is_late (1 if delivered and delivered_customer_date > estimated_delivery_date, else 0)
- days_to_deliver (delivered_customer_date - purchase_timestamp, in days)
- days_late (0 if on-time or not delivered; else delivered_customer_date - estimated_delivery_date, in days)

### Notes / Rules
- SLA is evaluated only for delivered orders.
- Non-delivered orders are excluded from SLA compliance rate.

## Dimension Tables

### dim_customer
- customer_id (PK)
- customer_unique_id
- customer_city
- customer_state

### dim_seller
- seller_id (PK)
- seller_city
- seller_state

### dim_product (optional)
- product_id (PK)
- product_category_name
- product_weight_g

### dim_date
- date_key (PK)
- date
- year, month, day_of_week

## Bridge Table

### bridge_order_item
- order_id (FK)
- order_item_id
- seller_id (FK)
- product_id (FK)
- price
- freight_value
