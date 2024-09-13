# 06: Join in Where clause

### 1
```sql
SELECT name
FROM country
WHERE iso_country in(
    SELECT iso_country
    FROM airport
    WHERE name LIKE "satsuma%"
);
```

![alt text](../img/06/1.png)

### 2
```sql
SELECT name
FROM airport
WHERE iso_country in (
    SELECT iso_country
    FROM country
    WHERE iso_country='MC'
);
```

![alt text](../img/06/2.png)

### 3
```sql
SELECT screen_name
FROM game
WHERE id in(
    SELECT game_id
    FROM goal_reached
    WHERE goal_id in(
        SELECT id
        FROM goal
        WHERE target_text='Clouds'
    )
);
```

![alt text](../img/06/3.png)

### 4
```sql
SELECT name
FROM country
WHERE iso_country not in(
    SELECT iso_country
    FROM airport
);
```

![alt text](../img/06/4.png)

### 5
```sql
SELECT name
FROM goal
WHERE id not in(
    SELECT goal_id
    FROM goal_reached
    WHERE game_id in(
        SELECT id
        FROM game
        WHERE screen_name='Heini'
    )
);
```

![alt text](../img/06/5.png)