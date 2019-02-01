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

## cross apply with for json

```
select * from users cross apply (select * from profiles for json path) p(profiles)
```

其中，`p(profiles)`表示表名为`p`，第一个字段名为`profiles`。
如果没有指定，则会报错。

```
\# | id | name | profiles
--- | --- | --- | ---
1 | 1 | sql | \[\{"user\_id":1\,"address":"sql address"\}\,\{"user\_id":2\,"address":"java address"\}\]
2 | 2 | java | \[\{"user\_id":1\,"address":"sql address"\}\,\{"user\_id":2\,"address":"java address"\}\]
3 | 3 | javascript | \[\{"user\_id":1\,"address":"sql address"\}\,\{"user\_id":2\,"address":"java address"\}\]
```

## outer apply with dummy table

```
with dummy(dummy) as (select 1)
select 'a' as 'a' from dummy 
outer apply (select * from profiles for json path) p(p1)
```

```
\# | a
--- | ---
1 | a
```
