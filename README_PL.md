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

* SELECT pokazujący nazwy wszystkich produktów należące do rodzaju "owoc" :  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="owoc";
```
* SELECT pokazujący nazwy wszystkich produktów należące do rodzaju "warzywo":  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj ="warzywo";
```

* SELECT pokazujący rodzaj warzywo i wszystkie produkty warzywne mające mniej niż 70 kalorii:  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="warzywo" AND kcal<=70;
```

* SELECT wyświetlający nazwę produktu w oparcu o określone parametry: rodzaj = "nasiona" oraz białka <= 5 i tłuszcze <=1.2 (trzy warunki muszą być spełnione)  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="nasiona"AND białka<=5 AND tłuszcze<=1.2;
```

* SELECT pokazujący nazwy wszystkich produktów uwzględniające białko równe bądź większe od 10  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE białka >=10;
```

* SELECT wyświetlający przykładowe obliczenia dla kcal, białek i tłuszczy i odpowiadające im aliasy  

``` sql
SELECT 
kcal+2 AS Gladiator, 
białka-1 AS Maximus, 
tłuszcze*(12 + węglowodany/4) AS Kate
FROM SQL_4_food;
```

* SELECT wyświetlający nazwy wszystkich produktów i rodzaj oraz odpowiadające im obliczenia kcal, białek, węglowodanów i tłuszczy  

``` sql
SELECT nazwa_produktu, rodzaj, (kcal*białka)+(węglowodany-tłuszcze) FROM SQL_4_food;
```

* SELECT pokazujący nazwy wszystkich produktów w których kcal są <=200  

``` sql
SELECT nazwa_produktu, kcal FROM SQL_4_food WHERE kcal <=200;
```

* SELECT wyświetlający nazwy wszystkich produktów przypisanych jako produkty niskokaloryczne w przedziale kcal <=200  

``` sql
SELECT nazwa_produktu AS "produkty niskokaloryczne" FROM SQL_4_food WHERE kcal <=200;
```

* SELECT wyświetlający nazwy wszystkich produktów z rodzaju konserwy zawierajace kcal <=100  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj = "konserwy" AND kcal <=100;
```

* SELECT wyświetlający nazwy wszystkich produktów z rodzaju owoc zawierające kcal <=50  

``` sql
SELECT nazwa_produktu FROM SQL_4_food WHERE rodzaj="owoc" AND kcal <= 50;
```

* SELECT wyświetlający nazwy wszystkich produktów w których białka są <=10 

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
