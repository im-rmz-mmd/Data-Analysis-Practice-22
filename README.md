# 🍽️ Food Orders Dashboard | Power BI Project

A clean, one-page **Power BI** dashboard that transforms raw food order data into clear insights.  
Designed to highlight top-performing items, categories, and revenue trends.

---

## 📁 Dataset Overview

- **menu_items.csv**  
  Contains: `item_name`, `category`, `price`

- **order_details.csv**  
  Contains: `order_id`, `order_date`, `item_id`

---

## 🛠️ Steps & Logic

### 1. Data Modeling
- One-to-many relationship: `menu_items[item_id]` ➝ `order_details[item_id]`
- Handled missing categories by filtering out blanks

### 2. DAX Measures
- **Total Revenue:**  
  ```DAX
  Total Revenue = SUMX(order_details, RELATED(menu_items[price]))
  ```

- **Total Orders:**  
  ```DAX
  Total Orders = COUNT(order_details[order_id])
  ```

- **Top Item:**  
  ```DAX
  Top Item = 
  CALCULATE(
    VALUES(menu_items[item_name]),
    TOPN(1, 
      SUMMARIZE(order_details, menu_items[item_name], "Order Count", COUNT(order_details[order_id])), 
      [Order Count], 
      DESC
    )
  )
  ```

---

## 📊 Visuals Used

- **KPI Cards:** Total Revenue, Total Orders, Top Item  
- **Bar Chart:** Order Count by `item_name`  
- **Donut Chart:** Order Count by `category`  
- **Bar Chart:** Total Revenue by `category`  
- **Line Chart:** Revenue over time (`order_date`)

---

## ✅ Insight Highlights

- **Hamburger** is the most ordered item  
- **Italian** food leads in revenue  
- Sales patterns show seasonal fluctuations  
- A clean visual layout, color-coded for categories
