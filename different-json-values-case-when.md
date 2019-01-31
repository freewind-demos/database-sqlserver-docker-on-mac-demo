```
select 
JSON_QUERY(case 
  when name='Java' then (select '1' as 'type',name for json path, WITHOUT_ARRAY_WRAPPER)
  when name='Sql' then (select '2' as 'type',name for json path, WITHOUT_ARRAY_WRAPPER)
  else null
end) as 'item'
from users
for JSON path
```

当我们使用了`WITHOUT_ARRAY_WRAPPER`后，`for json`的内容将被escape成一个字符串，`JSON_QUERY`再把这个字符串变成一个正常的JSON.

```
[{
    "item": {
        "type": "2",
        "name": "sql"
    }
}, {
    "item": {
        "type": "1",
        "name": "java"
    }
}, {}]
```

Doc: https://docs.microsoft.com/en-us/sql/relational-databases/json/solve-common-issues-with-json-in-sql-server?view=sql-server-2017