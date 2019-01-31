# For XML

这里只是试了几个例子，没有仔细研究，比如`type`的作用，以及两种生成嵌套xml的写法的区别

## "raw" type

```
select users.id, users.name as 'aaa.bbb' from users for xml raw, root('rows')
```

```
<rows>
  <row id="1" aaa.bbb="sql"/>
  <row id="2" aaa.bbb="java"/>
  <row id="3" aaa.bbb="javascript"/>
</rows>
```

### "path" type

```
select users.id, users.name as 'aaa.bbb' from users for xml path, root('rows')
```

```
<rows>
  <row>
    <id>1</id>
    <aaa.bbb>sql</aaa.bbb>
  </row>
  <row>
    <id>2</id>
    <aaa.bbb>java</aaa.bbb>
  </row>
  <row>
    <id>3</id>
    <aaa.bbb>javascript</aaa.bbb>
  </row>
</rows>
```

### nested

```
select users.*, profiles.* 
from users, profiles 
where users.id = profiles.user_id for xml auto, type, root('data')
```

```
<users id="1" name="sql">
  <profiles user_id="1" address="sql address"/>
</users>
<users id="2" name="java">
  <profiles user_id="2" address="java address"/>
</users>
```

```
<data>
  <users id="1" name="sql">
    <profiles user_id="1" address="sql address"/>
  </users>
  <users id="2" name="java">
    <profiles user_id="2" address="java address"/>
  </users>
</data>
```

### elements

```
select users.*, profiles.* 
from users, profiles 
where users.id = profiles.user_id for xml auto, type, root('data'), elements
```

```
<data>
  <users>
    <id>1</id>
    <name>sql</name>
    <profiles>
      <user_id>1</user_id>
      <address>sql address</address>
    </profiles>
  </users>
  <users>
    <id>2</id>
    <name>java</name>
    <profiles>
      <user_id>2</user_id>
      <address>java address</address>
    </profiles>
  </users>
</data>
```

### nested query

```
select *, 
(select * from profiles for xml auto, type, elements)
from users
for xml auto, type, elements
```

```
<data>
  <users>
    <id>1</id>
    <name>sql</name>
    <profiles>
      <user_id>1</user_id>
      <address>sql address</address>
    </profiles>
    <profiles>
      <user_id>2</user_id>
      <address>java address</address>
    </profiles>
  </users>
  <users>
    <id>2</id>
    <name>java</name>
    <profiles>
      <user_id>1</user_id>
      <address>sql address</address>
    </profiles>
    <profiles>
      <user_id>2</user_id>
      <address>java address</address>
    </profiles>
  </users>
  <users>
    <id>3</id>
    <name>javascript</name>
    <profiles>
      <user_id>1</user_id>
      <address>sql address</address>
    </profiles>
    <profiles>
      <user_id>2</user_id>
      <address>java address</address>
    </profiles>
  </users>
</data>
```