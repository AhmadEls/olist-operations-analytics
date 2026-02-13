# KPI Definitions — Olist Operations Analytics

## Delivered Orders
**Definition:** Count of successfully delivered orders.  
**Metric meaning:** Total completed deliveries (baseline volume).  
**Field source:** m_exec_kpis[delivered_orders]

## On-Time Orders
**Definition:** Delivered orders where delivery date <= estimated delivery date.  
**Metric meaning:** Volume meeting the delivery promise.  
**Field source:** m_exec_kpis[on_time_orders]

## Late Orders
**Definition:** Delivered orders where delivery date > estimated delivery date.  
**Metric meaning:** Volume that missed the promise.  
**Field source:** m_exec_kpis[late_orders]

## On-Time Rate
**Definition:** On-Time Orders / Delivered Orders.  
**Metric meaning:** Overall SLA success rate.  
**Field source:** m_exec_kpis[on_time_rate]

## Avg Days Late
**Definition:** Average number of days late for late deliveries only.  
**Metric meaning:** Severity of SLA misses (not just count).  
**Field source:** m_exec_kpis[avg_days_late]
