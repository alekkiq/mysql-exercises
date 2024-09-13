# MySQL exercises

## Sections
- [03: Single table select](#03-single-table-select)
- [04: Where clause select](#04-where-clause-select)
- [05: Join exercises](#05-join-exercises)
- [06: Join in Where clause](#06-join-in-where-clause)
- [07: Summaries (distinct, group by)](#07-summaries-distinct-group-by)
- [08: Update queries](#08-update-queries)

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

### 1
SELECT max(elevation_ft)\
FROM airport;

![alt text](img/07/1.png)

### 2
SELECT continent, COUNT(*)\
FROM country
GROUP BY continent;

Tässä pieni ongelma "NA" kohdalla, sillä tietokannan "täyttäjä" lukee datan CSV:stä, ja muuttaa kaikki NA-tyypit nolliksi. Tällöin myös string "NA" muunnetaan nollaksi.*

![alt text](img/07/2.png)*

### 3
SELECT screen_name, COUNT(*)\
FROM goal_reached\
JOIN game on game.id = goal_reached.game_id\
GROUP BY screen_name;

![alt text](img/07/3.png)

### 4
SELECT screen_name\
FROM game\
WHERE co2_consumed in(\
    SELECT min(co2_consumed)\
    FROM game\
);

![alt text](img/07/4.png)

### 5
SELECT country.name as "name", count( * )\
FROM airport\
JOIN country on country.iso_country = airport.iso_country\
GROUP BY country.name\
HAVING count( * ) > 50\
ORDER BY count( * ) DESC;

![alt text](img/07/5.png)

### 6
SELECT country.name as "name"\
FROM airport\
JOIN country on country.iso_country = airport.iso_country\
GROUP BY country.iso_country\
HAVING count(*) > 1000;

![alt text](img/07/6.png)

### 7
SELECT name\
FROM airport\
WHERE elevation_ft in(\
    SELECT max(elevation_ft)\
    FROM airport\
);

![alt text](img/07/7.png)

### 8
SELECT country.name as "name"\
FROM airport\
JOIN country on country.iso_country = airport.iso_country\
WHERE elevation_ft in(\
    SELECT max(elevation_ft)\
    FROM airport\
);

![alt text](img/07/8.png)

### 9
SELECT count( * )\
FROM goal_reached\
WHERE game_id in(\
    SELECT id\
    FROM game\
    WHERE screen_name='Vesa'\
);

![alt text](img/07/9.png)

### 10
SELECT name\
FROM airport\
WHERE latitude_deg in(\
    SELECT min(latitude_deg)\
    FROM airport\
);

![alt text](img/07/10.png)

<hr>

## 08: Update queries

### 1
SELECT * from game;

UPDATE game\
SET location=(
    SELECT ident\
    FROM airport\
    WHERE name='Nottingham Airport'\
), 
co2_consumed=co2_consumed+500
WHERE screen_name='Vesa';

SELECT * from game;

![alt text](img/08/1.png)

### 2 (multichoice question)
"
Ja nyt alustetaan oma tietokanta valmiiksi projektin kannalta. Eli poistetaan kaikki pelin tilaan liittyvä testidata. Viite-eheyden takia pystyt poistamaan datan vain fiksussa järjestyksessä.

Täytyykö sinun poistaa ensin data game-taulusta vai goal_reached taulusta?"

v: **goal_reached**

### 3
DELETE FROM goal_reached;

### 4
DELETE FROM game;