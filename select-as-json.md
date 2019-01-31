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