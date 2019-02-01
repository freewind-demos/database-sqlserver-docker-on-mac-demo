Doc: https://stackoverflow.com/questions/1139160/when-should-i-use-cross-apply-over-inner-join

## cross apply == inner join

```
select * from 
(users
cross apply (select * from profiles where users.id = profiles.user_id) p)
```

```
select * from users inner join profiles on users.id = profiles.user_id
```

```
\# | id | name | user\_id | address
--- | --- | --- | --- | ---
1 | 1 | sql | 1 | sql address
2 | 2 | java | 2 | java address
```

## outer apply == left outer join

```
select * from 
(users
outer apply (select * from profiles where users.id = profiles.user_id) p)
```

```
select * from users left outer join profiles on users.id = profiles.user_id
```

```
\# | id | name | user\_id | address
--- | --- | --- | --- | ---
1 | 1 | sql | 1 | sql address
2 | 2 | java | 2 | java address
3 | 3 | javascript |  | 
```

## cross apply that "join" can't do

```
select * from (
users
cross apply 
(select top 2 * from profiles) p
)
```

```
\# | id | name | user\_id | address
--- | --- | --- | --- | ---
1 | 1 | sql | 1 | sql address
2 | 2 | java | 1 | sql address
3 | 3 | javascript | 1 | sql address
4 | 1 | sql | 2 | java address
5 | 2 | java | 2 | java address
6 | 3 | javascript | 2 | java address
```

## cross apply with reused calculation

```
select users.*, x.address from users 
cross apply (select address + address as 'address'  from profiles where users.id = profiles.user_id) x
```