像JavaScript中的`splice`，用于将字符串中的一部分替换为另一个字符串

```
select stuff('abc', 2, 1, 'xxx')
```

prints 

```
axxxc
```

Doc: https://docs.microsoft.com/en-us/sql/t-sql/functions/stuff-transact-sql?view=sql-server-2017

```
STUFF ( character_expression , start , length , replaceWith_expression ) 
```
