# MySQL exercises


## 03: Single table select

### 1
SELECT * FROM goal;

![alt text](img/03/select_all_from.png)

### 2
SELECT name, type 
FROM airport 
WHERE iso_country='FI';

![alt text](img/03/select_name_type_from.png)

### 3
SELECT name
FROM airport
WHERE iso_country='FI'
ORDER BY name;

![alt text](img/03/select_name_sorted.png)

### 4
SELECT name, type
FROM airport
WHERE iso_country='FI'
ORDER BY type, name;

![alt text](img/03/select_name_type_ordered.png)

### 5
SELECT name
FROM country
WHERE name LIKE 'F%';

![alt text](image.png)

### 6
SELECT name
FROM country
WHERE name like '%f%';

![alt text](img/03/select_name_where_f.png)

### 7
SELECT location FROM game WHERE screen_name='Vesa';

![alt text](img/03/select_location_screenname.png)

### 8
SELECT co2_consumed FROM game WHERE screen_name='Ilkka';

![alt text](img/03/select_co2consumed_screenname.png)

### 9
SELECT DISTINCT co2_budget FROM goal;

![alt text](img/03/select_distinct.png)

<hr>

## 04: Where-clause select

### 1
SELECT country.name as "country name", airport.name as "airport name"\
FROM country\
JOIN airport on country.iso_country = airport.iso_country\
WHERE country.name='Iceland';

![alt text](img/04/1.png)

### 2
SELECT airport.name as "airport name"\
FROM country\
JOIN airport on country.iso_country = airport.iso_country\
WHERE country.name='France' AND airport.type='large_airport';

![alt text](img/04/2.png)

### 3
SELECT country.name as "country_name", airport.name as "airport_name"\
FROM country\
JOIN airport on country.iso_country = airport.iso_country\
WHERE airport.continent='AN';

![alt text](img/04/3.png)

### 4
SELECT airport.elevation_ft\
FROM game\
JOIN airport on game.location = airport.ident\
WHERE screen_name='Heini';

![alt text](img/04/4.png)

### 5
SELECT airport.elevation_ft * 0.3048 as "elevation_m"\
FROM game\
JOIN airport on game.location = airport.ident\
WHERE screen_name='Heini';

![alt text](img/04/5.png)

### 6
SELECT airport.name as "name"\
FROM game\
JOIN airport on game.location = airport.ident\
WHERE screen_name='Ilkka';

![alt text](img/04/6.png)

### 7
SELECT country.name as "name"\
FROM game\
JOIN airport on game.location = airport.ident\
JOIN country on airport.iso_country = country.iso_country\
WHERE screen_name='Ilkka';

![alt text](img/04/7.png)

### 8
SELECT goal.name as "name"\
FROM game\
JOIN goal_reached on game.id = goal_reached.game_id\
JOIN goal on goal_reached.goal_id = goal.id\
WHERE screen_name='Heini';

![alt text](img/04/8.png)

### 9
SELECT airport.name as "name"\
FROM game\
JOIN ???\
WHERE screen_name='Ilkka';

En saanut ideasta kiinni, missä saavutuksien lokaatio tallentuu.

### 10
Sama homma kun 9:ssä

<hr>

## 05: Join-exercises

### 1
SELECT country.name as "country name", airport.name as "airport name"\
FROM airport\
JOIN country on airport.iso_country = country.iso_country\
WHERE scheduled_service='yes' AND country.name='Finland';

![alt text](img/05/1.png)

### 2
SELECT screen_name, airport.name as "name"\
FROM game\
JOIN airport on game.location = airport.ident;

![alt text](img/05/2.png)

### 3
SELECT screen_name, country.name as "name"\
FROM game\
JOIN airport on game.location = airport.ident\
JOIN country on airport.iso_country = country.iso_country;

![alt text](img/05/3.png)

### 4
SELECT airport.name as "name", screen_name\
FROM airport\
LEFT JOIN game on game.location = airport.ident\
WHERE airport.name LIKE '%hels%'\
ORDER BY screen_name DESC;

![alt text](img/05/4.png)

### 5
SELECT goal.name as "name", screen_name\
FROM goal\
LEFT JOIN goal_reached on goal.id = goal_reached.goal_id\
LEFT JOIN game on goal_reached.game_id = game.id;

![alt text](img/05/5.png)

<hr>

## 06: Join in Where clause

### 1
SELECT name\
FROM country\
WHERE iso_country in(\
    SELECT iso_country\
    FROM airport\
    WHERE name LIKE "satsuma%"\
);

![alt text](img/06/1.png)

### 2
SELECT name\
FROM airport\
WHERE iso_country in (\
    SELECT iso_country\
    FROM country\
    WHERE iso_country='MC'
);

![alt text](img/06/2.png)

### 3
SELECT screen_name\
FROM game\
WHERE id in(\
    SELECT game_id\
    FROM goal_reached\
    WHERE goal_id in(\
        SELECT id\
        FROM goal\
        WHERE target_text='Clouds'
    )\
);

![alt text](img/06/3.png)

### 4
SELECT name\
FROM country\
WHERE iso_country not in(\
    SELECT iso_country\
    FROM airport\
);

![alt text](img/06/4.png)

### 5
SELECT name\
FROM goal\
WHERE id not in(\
    SELECT goal_id\
    FROM goal_reached\
    WHERE game_id in(\
        SELECT id\
        FROM game\
        WHERE screen_name='Heini'\
    )\
);

![alt text](img/06/5.png)

<hr>

## 07: Summaries (distinct, group by)
SELECT max(elevation_ft) FROM airport;

![alt text](image.png)