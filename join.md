Note: `join` and `inner join` are same

```
select users.*, profiles.address from users join profiles on users.id = profiles.user_id;

select users.*, profiles.address from users inner join profiles on users.id = profiles.user_id;

select users.*, profiles.address from users, profiles where users.id = profiles.user_id;
```


```
select users.*, profiles.address from users left join profiles on users.id = profiles.user_id;
```

