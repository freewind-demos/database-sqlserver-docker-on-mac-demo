# For JSON

## "path" mode

`aaa.bbb` will create nested json

```
select users.id, users.name as 'aaa.bbb' from users for json path
```

```
[{
    "id": 1,
    "aaa": {
        "bbb": "sql"
    }
}, {
    "id": 2,
    "aaa": {
        "bbb": "java"
    }
}, {
    "id": 3,
    "aaa": {
        "bbb": "javascript"
    }
}]
```

## "auto" mode

`aaa.bbb` will be the a single key

```
[{
    "id": 1,
    "aaa.bbb": "sql"
}, {
    "id": 2,
    "aaa.bbb": "java"
}, {
    "id": 3,
    "aaa.bbb": "javascript"
}] 
```

## root 

```
select users.id, users.name as 'aaa.bbb' from users for json path, root('user')
```

```
{
    "user": [{
        "id": 1,
        "aaa": {
            "bbb": "sql"
        }
    }, {
        "id": 2,
        "aaa": {
            "bbb": "java"
        }
    }, {
        "id": 3,
        "aaa": {
            "bbb": "javascript"
        }
    }]
}
```

## openjson

```
select * from openjson('{"aa":"11"}')
```

```
\# | key | value | type
--- | --- | --- | ---
1 | aa | 11 | 1
```

## multi level json

```
select 
(   select 
    (select users.* from users for json path) a,
    (select users.* from users for json path) b
    for json path
) as c
```

```
[{
    "c": [{
        "a": [{
            "id": 1,
            "name": "sql"
        }, {
            "id": 2,
            "name": "java"
        }, {
            "id": 3,
            "name": "javascript"
        }],
        "b": [{
            "id": 1,
            "name": "sql"
        }, {
            "id": 2,
            "name": "java"
        }, {
            "id": 3,
            "name": "javascript"
        }]
    }]
}]
```