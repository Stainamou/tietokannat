# Viikko 2: Yhteen tauluun kohdistuvat osiot ja where-osan liitosehto

## Yhteen tauluun kohdistuvien kyselyiden harjoitukset

### Tehtävä 1: Tee kysely, joka tulostaa kaikki sarakkeet goal-talusta.
SELECT * FROM goal;

![image](https://github.com/user-attachments/assets/f1a537a3-3f2f-46aa-9a1f-3fd58c22572c)

### Tehtävä 2: Tee kysely, joka tulostaa nimen ja tyypin kaikista Suomessa sijaitsevista lentokentistä. Suomen maatunnus on: FI
SELECT name airport_type FROM airport WHERE iso_country = "FI";

![image](https://github.com/user-attachments/assets/0beca3c3-b552-4ea7-8e3f-67a7ac6ddba8)

### Tehtävä 3: Tee kysely, joka tulostaa suomalaisten lentokenttien nimet aakkosjärjestyksessä. Suomen maatunnus: FI
SELECT name FROM airport WHERE iso_country = "FI" order by name;

![image](https://github.com/user-attachments/assets/e74dc12e-d666-4c0e-bcae-450fe3a95d29)

### Tehtävä 4: Tee kysely, joka tulostaa nimen ja tyypin kaikista Suomessa sijaitsevista lentokentistä. Järjestä tulos ensisijaisesti tyypin mukaan ja toissijaisesti nimen mukaan.
SELECT name, type FROM airport WHERE iso_country = "FI" order by type, name;

![image](https://github.com/user-attachments/assets/00abecff-108a-4929-829e-47eb3025a9f9)

### Tehtävä 5: Tee kysely, joka tulostaa kaikki F-kirjaimella alkavat maan nimet country-taulusta.
SELECT name FROM country WHERE name like "F%";

![image](https://github.com/user-attachments/assets/b04063de-54a4-4b78-97ba-3e7f37649587)

### Tehtävä 6: Tee kysely, joka tulostaa kaikki country-taulun maiden nimet, joissa esiintyy F-kirjain.
SELECT name FROM country WHERE name like "%F%";

![image](https://github.com/user-attachments/assets/3bbad19a-dea2-4b01-8ccb-07deced0e8e6)

### Tehtävä 7: Missä locationissa Vesa sijaitsee?
SELECT location FROM game WHERE screen_name = "Vesa";

![image](https://github.com/user-attachments/assets/d7b42305-7959-43a1-85ce-6ab21f39a156)

### Tehtävä 8: Kuinka paljon Ilkka on kuluttanut CO2 budjettia?
SELECT co2_consumed FROM game WHERE screen_name = "Ilkka";

![image](https://github.com/user-attachments/assets/65e6239a-f156-4af1-ac04-6db806a494fc)

### Tehtävä 9: Kuinka paljon alkuperäinen CO2 budjetti on (tulosta CO2 budjetin arvo vain kerran)?
SELECT distinct co2_budget FROM game;

![image](https://github.com/user-attachments/assets/ca1f038a-8a56-4e74-9808-72c90333d6b0)

## Where-osan liitosehto harjoitukset

### Tehtävä 1: Tee kysely, joka listaa maan nimen ja lentokentän nimen. Valitse maaksi Islanti ja anna country-taulun name-kentälle alias "country name" ja airport taulun name-kentälle alias "airport name".
SELECT country.name AS "country name", airport.name AS "airport name"
FROM airport, country
WHERE airport.iso_country = country.iso_country AND country.name = "Iceland";

![image](https://github.com/user-attachments/assets/332f89bf-7d23-4230-9d1b-569791e21653)

### Tehtävä 2: Listaa Ranskan isojen lentokenttien nimet. Anna kentän nimelle alias "airport name".
SELECT airport.name AS "airport name"
from airport, country
WHERE airport.iso_country = country.iso_country AND country.name = "France" AND airport.type = "large_airport";

![image](https://github.com/user-attachments/assets/99615424-28ff-441d-b731-7a260ca50276)

### Tehtävä 3: Tee kysely, joka listaa kaikki Antarktiksella sijaitsevien lentokenttien nimet ja vastaava maan nimi.
SELECT country.name AS "country name", airport.name AS "airport name"
FROM airport, country
WHERE airport.iso_country = country.iso_country AND country.continent = "AN";

![image](https://github.com/user-attachments/assets/46e406d2-5332-4381-8e88-000d1d2601d7)

### Tehtävä 4: Kuinka korkealla Heini on paraikaa merenpinnasta mitattuna?
SELECT elevation_ft
FROM airport, game
WHERE location = ident AND screen_name = "Heini";

![image](https://github.com/user-attachments/assets/3a2eac05-d66b-45a5-8a9d-fd56cbd80d0a)

### Tehtävä 5: Kuinka korkealla Heini on paraikaa merenpinnasta mitattuna? Anna tulos metreissä, ja anna tulokselle alias elevation_m. Yksi jalka on 0,3048 metriä. Älä käytä muutuujaa. Voit kuitenkin tehdä laskutoimituksen ilman muuttujaa
SELECT elecation_ft * 0.3048 AS elevation_m
FROM airport, game
WHERE location = ident AND screen_name = "Heini";

![image](https://github.com/user-attachments/assets/f2cee4ba-2358-47ba-9188-61b64845122f)

### Tehtävä 6: Minkä nimisellä lentokentällä Ilkka on?
SELECT name
FROM airport, game
WHERE location = ident AND screen_name = "Ilkka";

![image](https://github.com/user-attachments/assets/f8dd19b4-18d2-497e-a094-ce1fff92ce46)

### Tehtävä 7: Minkä nimisessä maassa Ilkka on?
SELECT country.name
FROM airport, game, country
WHERE location = ident AND airport.iso_country = country.iso_country AND screen_name = "Ilkka";

![image](https://github.com/user-attachments/assets/58f81465-1388-46b3-82c6-75af781ccb4c)

### Tehtävä 8: Minkä nimiset säätila-tavoitteet Heini on saavuttanut?
SELECT name
FROM goal, goal_reached, game
WHERE game.id = game_id and goal.id = goal_id and screen_name = "Heini";

![image](https://github.com/user-attachments/assets/42723367-f2cf-4b0e-b394-f3fae2e7c8cd)

### Tehtävä 9: Minkä nimisellä lentokentällä Ilkka saavutti säätilan clouds?
SELECT airport.name
FROM airport, game, goal, goal_reached
WHERE location = ident AND game.id = game_id AND goal.id = goal_id and screen_name = "Ilkka" and goal.name = "CLOUDS"; 

![image](https://github.com/user-attachments/assets/c33b8418-7e09-4057-9964-d5b0a177355f)

### Tehtävä 10: Minkä nimisessä maassa Ilkka saavutti säätilan clouds?
SELECT country.name
FROM country, airport, game, goal, goal_reached
WHERE airport.iso_country = country.iso_country AND location = ident AND game.id = game_id AND goal.id = goal_id AND screen_name = "Ilkka" AND goal.name = "CLOUDS";

![image](https://github.com/user-attachments/assets/bb3f195f-dc16-491e-b7ea-f4a898902f45)

# Viikko 3

## Join harjoitukset

### Tehtävä 1: Luettele suomalaiset lentokentät, joilla on aikataulutettuja palveluja. Lopputulokseen halutaan sekä maan nimi että lentokentän nimi.
SELECT country.name AS "country name", airport.name AS "airport name"
FROM country INNER JOIN airport ON airport.iso_country = country.iso_country
WHERE country.name = "Finland" AND scheduled_service = "yes";

![image](https://github.com/user-attachments/assets/4fbc6e5b-3cee-4f68-9174-123cade29e34)

### Tehtävä 2: Luettele pelaajanimet ja niiden lentokentrien nimet, joilla he ovat nyt.
SELECT screen_name, airport.name
FROM game INNER JOIN airport ON location = ident;

![image](https://github.com/user-attachments/assets/0e8dc84f-7694-4d43-8899-0ca7885f4f9d)

### Tehtävä 3: Luettele pelaajanimet ja maat, joissa he ovat nyt.
SELECT screen_name, country.name
FROM game INNER JOIN airport ON location = ident INNER JOIN country ON airport.iso_country = country.iso_country;

![image](https://github.com/user-attachments/assets/6630a545-c8e0-4ee7-a338-b176e24bbd78)

### Tehtävä 4: Luettele kaikkien niiden lentokenttien nimet, jotka sisältävät merkkijonon "Hels" ja pelaajan nimi, jos joku pelaaja sattuu ko. kentällä olemaan.
SELECT airport.name, screen_name
FROM airport LEFT JOIN game ON ident = location WHERE name like "%Hels%";

![image](https://github.com/user-attachments/assets/ae3963bd-dc79-4649-a66a-aad45da7c6be)

### Tehtävä 5: Luettele kaikki säätilatavoitteiden nimet ja pelaajan nimi, jos pelaaja on sen saavuttanut
SELECT name, screen_name
FROM goal LEFT JOIN goal_reached ON goal.id = goal_id LEFT JOIN game ON game.id = game_id; 

![image](https://github.com/user-attachments/assets/a928e7df-2d50-49f0-a9b8-84918337f014)

## Sisäkysely harjoitukset

### Tehtävä 1: Minkä nimisessä maassa sijaitsee sanalla ”Satsuma” alkava lentokenttä?
SELECT name FROM country
WHERE iso_country in (SELECT iso_country FROM airport WHERE name like "Satsuma%";

![image](https://github.com/user-attachments/assets/442ea898-2729-4328-a691-d8d0f0b86a31)

### Tehtävä 2: Luettele Monacossa sijaitsevien lentokenttien nimet.
SELECT name FROM airport
WHERE iso_country in (SELECT iso_country FROM country WHERE name like "Monaco");

![image](https://github.com/user-attachments/assets/0cd54054-bfd5-4ea7-a04e-428b76cdf07a)

### Tehtävä 3:  Luettele nimimerkit, jotka ovat saavuttaneet säätilatavoitteen pilvistä (CLOUDS).
SELECT screen_name FROM game
WHERE id in (SELECT game_id FROM goal_reached WHERE goal_id in (SELECT id FROM goal WHERE name = "CLOUDS"));

![image](https://github.com/user-attachments/assets/be78da10-2c00-41c1-acb2-a8b43a6cb60c)

### Tehtävä 4: Luettele kaikki maat, joissa ei ole lentokenttää.
SELECT country.name FROM country
WHERE iso_country NOT IN (SELECT airport.iso_country FROM airport);

![image](https://github.com/user-attachments/assets/d85b3fec-42b6-4e2f-9e59-c062a9e74e07)

### Tehtävä 5: Minkä nimiset säätilatavoitteet Heiniltä on saavuttamatta?
SELECT name FROM goal
WHERE id NOT IN (SELECT goal.id FROM goal, goal_reached, game WHERE goal.id = goal_id AND game.id = game_id AND screen_name = "Heini");

![image](https://github.com/user-attachments/assets/2179590b-54b7-453e-951e-50bdf9e6e1b7)

