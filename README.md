# supersales_sql
SQL exercises using window functions (ROW_NUMBER, CTE)
/*
📊 SQL Task: Top 3 best-selling products in each product group

🎯 Goal:
For each product group, find the top 3 products that generated the highest revenue.

🗃️ Used tables:
- product_groups: contains product_group, group_id, category
- products: contains product_id, product_price, group_id
- order_positions: contains product_id, item_quantity
