```
with 
  t1 as (select * from users), 
  t2 as (select * from profiles) 
select t1.*, t2.* from t1, t2 
where t1.id = t2.user_id
```