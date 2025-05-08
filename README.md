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

🧮 Revenue = SUM(item_quantity) * product_price
*/
with tabela as (
select 
	pg.group_id 
	,pg.product_group
	,pg.category as category
	,p.product_id
	,p.product_price 
	,sum(op.item_quantity)
	,round(sum(op.item_quantity)*p.product_price,2) as revenue
from product_groups pg 
left join products p on pg.group_id = p.group_id 
left join order_positions op on p.product_id = op.product_id 
group by 1,2,3,4,5
)
-- Rank products within each group by revenue (descending)
select * from(
	select*
	,row_number() over (partition by product_group order by revenue desc) as top
	from tabela
) as ranked
-- Select only top 3 products per group
where top <=3
