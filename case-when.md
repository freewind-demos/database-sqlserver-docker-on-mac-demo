```
select 
  case 
    when users.name = 'java' then 'JAVA' 
    when users.name = 'javascript' then 'JAVASCRIPT'
  end 
from users;
```

\# | \(No column name\)
--- | ---
1 | 
2 | JAVA
3 | JAVASCRIPT