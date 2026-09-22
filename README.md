# CodeRefine Qualification 2 - Carieeer

## [Excalidraw file](amazieee.excalidraw)

## Functional Requirements :

- system should receive and validate orders (same order shouldn't get processed twice)
-  system should check availability of order's items 
- system should reserve order items to prevent overselling
- system should allocate robots to pack order
- system should get progress of robots handling the order continuously
- system should move order to packing station after fully collecting the order
- warehouse operators should view order status (Received → Confirmed →etc..)
- system should notify operators about important events (low stock, a robot failure, a delayed      order, or a robot with a low battery)
- customer should place and track (get notified) order status 

## nonFunctional Requirements :

- scalability to handle many orders
- resilience to handle robot failures
- consistency to prevent overselling items
- idempocity (I dont remember the exact word but it is for handling order submitted twice or more)

## Data Model :

```text
Customer 
{
    - id
    - name
    - Order[]
    - address
    - email
    - password
    - payment_info

}
```
``` text
Operator
{
    - id
    - name
    - email
    - password
    - Item[]

}
```
```text
Order
{
    - id(PK)
    - items[<item_id(fk) : quantity>]
    - ordered_at:Time
    - status <Received ,Confirmed , Picking , Collected , Packed , Ready for Shipping, or Cancelled / Failed>
    - robot_fleet_status
    - customer_id
    - estimated_arrival_time

}
```


```text
Item
{
    - id(pk)
    - stock_quantity
    - price
    - name
    - is_available

}
```

```text
Robot
{
    - id(pk)
    - status <ASSIGNED,INPROGRESS,COMPLETED,FAILED>
    - item_id(fk)
    - location <x,y>
    - battery level
}
```

## API Design

**`POST orders/place -> Partial<Order<Received>>`**

```text
{
    - items[<item_id(fk) : quantity>]
    - ordered_at:Time
    - customer_id
}
```

**`GET /orders/order?page{}-> Order[]`**

**`GET /orders/ordrer?{id}-> Order<id>`**

**`GET /orders/status/order?{id} -> Partial<Order<status>>`**

**`PUT /orders/update_status/order?{id} -> Partial<Order<status>>`**

```text
{
    - new_order_status
}
```

**`GET /items/isavailable/item?{id} -> <True,False>`**

**`PUT /items/reserve/item -> Item`**
```text
{
    - item_id
    - item_quantity
}
```

**`POST /robots/allocate -> <Robots[],Order>`**
```text
{
    - order_id
}
```

**`GET /robots/status/robot?{id} -> Partial<Robot<status>>`**

**`Event-Listener ("low stock") -> item stock is low notify operator`**

```text
{
    - item_id
}
```
**`Event-Listener ("low battery robot") -> robot battery is low notify operator`**
```text
{
    - robot_id
}
```

**`Event-Listener ("failed robot") -> robot failed notify operator`**
```text
{
    - robot_id,
    - order_id<delayed by robot failure (<5s)>
}
```


**`Event-Listener ("ORDER_STATUS") -> order status changed notify customer`**
``` text
{
    - order_id,
    - customer_id,
}
```

## High level architecture :
<img width="1210" height="648" alt="v1_arch" src="v1_arch.png" />

----
[Deep Dives](deep_dives.md)
---
## Team Members :
### Fatma Omara
### Salma Shaker




