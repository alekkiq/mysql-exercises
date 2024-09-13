# MySQL exercises


## Single table select

### 1
SELECT * FROM goal;

![alt text](img/exc_1/select_all_from.png)

### 2
SELECT name, type 
FROM airport 
WHERE iso_country='FI';

![alt text](img/exc_1/select_name_type_from.png)

### 3
SELECT name
FROM airport
WHERE iso_country='FI'
ORDER BY name;

![alt text](img/exc_1/select_name_sorted.png)

### 4
SELECT name, type
FROM airport
WHERE iso_country='FI'
ORDER BY type, name;

![alt text](img/exc_1/select_name_type_ordered.png)

### 5
SELECT name
FROM country
WHERE name LIKE 'F%';

![alt text](image.png)

### 6
SELECT name
FROM country
WHERE name like '%f%';

![alt text](img/exc_1/select_name_where_f.png)

### 7
SELECT location FROM game WHERE screen_name='Vesa';

![alt text](img/exc_1/select_location_screenname.png)

### 8
SELECT co2_consumed FROM game WHERE screen_name='Ilkka';

![alt text](img/exc_1/select_co2consumed_screenname.png)

### 9
SELECT DISTINCT co2_budget FROM goal;

![alt text](img/exc_1/select_distinct.png)

<hr>

## Where-clause select

### 1
SELECT country.name as "country name", airport.name as "airport name" 
FROM country 
JOIN airprot on country.iso_country = airport.iso_country 
WHERE country.name='Iceland';

