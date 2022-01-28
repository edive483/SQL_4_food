# Projekt zawierający dane o zdrowym odżywianiu

## Tabela: SQL_4_food

Tabela ta zawiera kolumny i rekordy. Dotyczy kaloryczności produktów w 100g.

### Kolumny:  

**nazwa_produktu**  
**rodzaj**  : owoc, warzywo, zboża, nabiał, wędliny, konserwy, mięso, ryby, przyprawy, nasiona, inne.   
**kcal**  
**białka**  
**tłuszcze**  
**węglowodany**  

### Przykłady produktów (kolumna: nazwa_produktu)   

* agrest
* banan
* cytryna
* dynia
* estragon
* figi suszone
* grejpfrut

## Tabela: cena_produktow

Tabela ta zawiera dane dotyczące ceny 100g za określony produkt. Są w niej 2 kolumny:  
**nazwa_produktu** oraz **cena_zl_za_100g**


# Zapytania SQL

W bazie danych **baza_danych_SQL4food** można wykonać przykładowe zapytania SQL:
	
## Przykłady dla SELECT

* SELECT pokazujący wszystkie produkty należące do rodzaju "owoc" :  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj='owoc';
```
* SELECT pokazujący wszystkie produkty należące do rodzaju "warzywo":

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj ="warzywo";
```

* SELECT pokazujący typ np. warzywo i wszystkie produkty warzywne mające mniej niż 70 kalorii:

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="warzywo"AND kcal<=70;
```

* SELECT wyświetlający nazwy produktu, rodzaj, białka i tłuszcze

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="nasiona"AND białka<=5 AND tłuszcze<=1.2;
```

* Wszystkie produkty mające np. więcej niż 10 białka

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE białka >=10;
```

``` sql
SELECT 
kcal+2 AS Gladiator, 
białka-1 AS Maximus, 
tłuszcze*(12 + węglowodany/4) AS AGATA 
FROM SQL_4_food;
```

``` sql
SELECT nazwa_produktu, rodzaj, (kcal*białka)+(węglowodany-tłuszcze) FROM SQL_4_food;
```

* wszystkie produkty poniżej 200 kcal

``` sql
SELECT nazwa_produktu, kcal FROM SQL_4_food WHERE kcal <=200;
```

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE kcal = "owoc" <=200;
```

* wszystkie produkty poniżej 100

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj = "warzywo" AND kcal <=100;
```

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="owoc" AND kcal <= 50;
```

* wszystkie produkty poniżej 10 białka

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE "białka" <= 10;
```
## Przykład dla DELETE

* wyświetlenie rekordu 0 i usunięcie tego jednego rekordu:

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE nazwa_produktu = "0";
```

``` sql
DELETE FROM SQL_4_food WHERE nazwa_produktu = "0";
```
Usunięcie produktu o nazwie "wiśnia". Dobrą praktyką jest najpierw sprawdzenie istniejącego rekordu - w ten sposób można sprawdzić klauzulę WHERE:

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE nazwa_produktu = "wiśnia";
```

``` sql
DELETE FROM SQL_4_food WHERE nazwa_produktu = "wiśnia";
```

Pokaż produkty z brakującymi danymi dla "rodzaj" i "węglowodany":

``` sql
SELECT rodzaj, kcal, białka, tłuszcze, węglowodany
FROM SQL_4_food
WHERE rodzaj IS NULL AND węglowodany IS NULL;
``` 

``` sql
SELECT * FROM SQL_4_food WHERE (rodzaj IS NULL AND węglowodany IS NULL) OR (nazwa_produktu ='0' AND rodzaj='0' AND kcal ='0' AND białka ='0' AND tłuszcze ='0' AND węglowodany ='0');
```

``` sql
DELETE FROM SQL_4_food WHERE (rodzaj IS NULL AND węglowodany IS NULL) OR (nazwa_produktu ='0' AND rodzaj='0' AND kcal ='0' AND białka ='0' AND tłuszcze ='0' AND węglowodany ='0')
``` 

## Przykład - DELETE i INSERT

Sprawdzenie istnienia produktu o nazwie "guma_orbit":

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE nazwa_produktu = "guma_orbit";
```

Usunięcie produktu "guma_orbit":

``` sql
DELETE FROM SQL_4_food WHERE nazwa_produktu = "guma_orbit";
```

Dodanie produktu "guma_orbit":

``` sql
INSERT INTO SQL_4_food (nazwa_produktu, rodzaj,kcal, białka, tłuszcze, węglowodany) VALUES ('guma_orbit', 'inne', '50', '3', '2', '10');
```

## Przykład - UPDATE

Zmiana istniejącego rekordu dla "guma_orbit".  
Najpierw sprawdzamy aktualny stan danych:

``` sql
SELECT * FROM SQL_4_food WHERE nazwa_produktu = "guma_orbit";
```

Następnie możemy zaktualizować istniejące dane:

``` sql
UPDATE SQL_4_food SET białka = "4", kcal = "55" WHERE nazwa_produktu = "guma_orbit";
SELECT * FROM SQL_4_food WHERE nazwa_produktu = "guma_orbit";
UPDATE SQL_4_food SET białka = "3", kcal = "50" WHERE nazwa_produktu = "guma_orbit";
SELECT * FROM SQL_4_food WHERE nazwa_produktu = "guma_orbit";
```
## Przykład - INNER JOIN SELECT

``` sql
SELECT SQL_4_food.nazwa_produktu, SQL_4_food.kcal FROM SQL_4_food
INNER JOIN cena_produktow 
ON SQL_4_food.nazwa_produktu=cena_produktow.nazwa_produktu;
```

``` sql
SELECT cena_produktow.nazwa_produktu, cena_produktow.kcal FROM cena_produktow
INNER JOIN SQL_4_food 
ON cena_produktow.nazwa_produktu=SQL_4_food.nazwa_produktu;
```

## Przykład - LEFT JOIN

``` sql
SELECT SQL_4_food.kcal as KCAL_S4F, cena_produktow.kcal AS KCAL_CP
FROM SQL_4_food 
LEFT JOIN cena_produktow
ON SQL_4_food.kcal = cena_produktow.kcal;
```
