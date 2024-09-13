# 03: Single table select

### 1
```sql
SELECT * FROM goal;
```

![alt text](../img/03/1.png)

### 2
```sql
SELECT name, type 
FROM airport 
WHERE iso_country='FI';
```

![alt text](../img/03/2.png)

### 3
```sql
SELECT name
FROM airport
WHERE iso_country='FI'
ORDER BY name;
```

![alt text](../img/03/3.png)

### 4
```sql
SELECT name, type
FROM airport
WHERE iso_country='FI'
ORDER BY type, name;
```

![alt text](../img/03/4.png)

### 5
```sql
SELECT name
FROM country
WHERE name LIKE 'F%';
```

![alt text](../img/03/5.png)

### 6
```sql
SELECT name
FROM country
WHERE name like '%f%';
```

![alt text](../img/03/6.png)

### 7
```sql
SELECT location FROM game WHERE screen_name='Vesa';
```

![alt text](../img/03/7.png)

### 8
```sql
SELECT co2_consumed FROM game WHERE screen_name='Ilkka';
```

![alt text](../img/03/8.png)

### 9
```sql
SELECT DISTINCT co2_budget FROM goal;
```

![alt text](../img/03/9.png)