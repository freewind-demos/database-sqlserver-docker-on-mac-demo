
## function to select table
```
create alter function findUserById(@id int) returns table
as
return (select * from users where id=@id);
GO

select * from findUserById(1);
```

第1个`GO`不可缺少，用来表示定义结束。

## function to calculate

```
alter function plus(@a int, @b int) returns int
as
begin
return @a+@b;
end
GO

select dbo.plus(1,2) as 'a';
``` 

`select`的时候，`dbo.plus`中的`dbo`不可缺少，
否则会提示`'plus' is not a recognized built-in function name.` 