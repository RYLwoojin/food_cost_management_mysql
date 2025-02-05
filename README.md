Purpose of this database

To create and manage the food cost easily.
This repository includes 6 databases; menu_list, menu_detail, recipe, recipe_detail, ingredients_list, and vendor_list.


![food_cost_erd](https://github.com/user-attachments/assets/469eb937-7246-4511-986b-c7ef0454787d)
![스크린샷 2025-02-05 141304](https://github.com/user-attachments/assets/cd1437d4-9913-4ac7-bda4-3988712fc5a7)


'''
UPDATE menu_detail md
SET m_cost = (
    SELECT COALESCE(SUM(rd.quantity_used * il.unit_price), 0)
    FROM recipe_detail rd
    JOIN ing_list il ON rd.ing_id = il.ing_id
    WHERE rd.r_id = md.r_id
),
m_selling_price = (
    SELECT COALESCE(SUM(rd.quantity_used * il.unit_price), 0) * 1.6
    FROM recipe_detail rd
    JOIN ing_list il ON rd.ing_id = il.ing_id
    WHERE rd.r_id = md.r_id
);
'''
Use this for update cost and selling price after ingredients price adjustment
