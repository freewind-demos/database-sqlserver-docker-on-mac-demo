```
CREATE TABLE users (
    id int NOT NULL IDENTITY PRIMARY KEY,
    name varchar(30) NOT NULL,
);

CREATE TABLE profiles (
    user_id int NOT NULL PRIMARY KEY,
    address varchar(100) NOT NULL,
);

CONSTRAINT FK_PROFILES_USER_ID FOREIGN KEY (user_id)     
    REFERENCES users (id)     
    ON DELETE CASCADE    
    ON UPDATE CASCADE    
);
```

`IDENTITY`用来自动生成增长的ID