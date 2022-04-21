# Week11---Database

M : Manuel
K : SQL,
C : Python

Asagidaki sorudan K ve C ile cozulmesini tasdikimizin cozumlerini (komut kodlarini) ustte test veya altta cozumu sekilde bir dosyaya yapistirip gondermenizi istiyoruz.

1- 'pycoders' isimli bir server kurun. (M)+

2- 'class4' veritabanı olusturun (M). Veritabanı silindi (M). Ayni veri tabanı yine olusturun (K)+
CREATE DATABASE class4;

3- https://www.postgresqltutorial.com/postgresql-sample-database/ gidiş ve ER modelini kullanarak. Tablolar arasindaki en az 5 iliskiyi yazin.(Hangi tablodaki arasinda ne tur bir iliski var)

1. customer - payment tabloları arasında one-to-many ilişkisi var; bir müşterinin birden fazla ödemesi olabilir fakat her ödemeyi yapan bir müşteri olabilir.
2. staff - store tabloloları arasında one-to-many ilişkisi var; bir personelin bir mağazası vadır fakat bir mağazanın birden fazla personeli olabilir.
3. staff - rental tabloları arasında one-to-many ilişkisi var; bir ödemeyi yanlızca bir personel alabilir fakat bir personel birden fazla ödeme alabilir.
4. staff -address tabloları arasında one-to-many ilişkisi var; bir adres bir personele aittir fakat her personelin bir adresi olabilir.
5. film - inventory tabloları arasında one-to-many ilişkisi var; her filmin bir envanteri olabilir fakat envanterde birden fazla film olabilir.

4- ER modeldeki tablolardan 3 tanesini M olusturun. (4-5-6. sorulari cozerken toblolar arasındaki iliskileri gözardı edebilirsiniz.)+

category
inventory
customer

5- ER modeldeki tablolardan 3 tanesini K olusturun.

CREATE TABLE film_category (
	film_id int PRIMARY KEY NOT NULL,
	category_id int NOT NULL,
	last_update date
);


CREATE TABLE rental (
	rental_id int PRIMARY KEY NOT NULL,
	rental_date date NOT NULL,
	inventory_id int NOT NULL,
	customer_id int NOT NULL,
	return_date date NOT NULL,
	staff_id int NOT NULL,
	last_update date
);


CREATE TABLE address (
	address_id int PRIMARY KEY NOT NULL,
	address varchar(50),
	adddress2 varchar(50),
	district varchar(50),
	city_id int NOT NULL,
	postal_code varchar(6),
	phone int,
	last_update date
);


6- ER modeldeki tablolardan 3 tanesini C olusturun. 

import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

comand = '''create table film
(
film_id integer primary key,
title varchar(50),
description varchar(255),
realease_year date,
language_id int,
rental_duration varchar,
rental_rate float,
length int,
replacement_cost int,
raiting float,
last_update date,
special_features varchar(255),
full_text varchar(255)
)
'''
cur.execute(comand)

cur.close()

conn.commit()

conn.close()


----------


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

comand = '''create table payment
(
payment_id integer primary key,
customer_id int,
staff_id int,
rental_id int,
amount float,
payment_date date
)
'''
cur.execute(comand)

cur.close()

conn.commit()

conn.close()


----------


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

comand = '''create table city
(
city_id integer primary key,
city varchar (25),
country_id varchar (25),
last_update date
)
'''
cur.execute(comand)

cur.close()

conn.commit()

conn.close()


----------



7- Olusturdugunuz 3 tabloya M ile 5 veri girişi yapin. +

8- Olusturdugunuz 3 tabloya K ile 5 veri girişi yapin.


INSERT INTO film_category (film_id, category_id, last_update)
VALUES ('1', '1', '2022-04-19');

INSERT INTO film_category (film_id, category_id, last_update)
VALUES ('2', '1', '2022-04-18');

INSERT INTO film_category (film_id, category_id, last_update)
VALUES ('3', '2', '2022-04-19');

INSERT INTO film_category (film_id, category_id, last_update)
VALUES ('4', '2', '2022-04-17');

INSERT INTO film_category (film_id, category_id, last_update)
VALUES ('5', '1', '2022-04-19')



INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id, last_update)
VALUES ('1', '2022-04-11', '1', '101', '2022-04-12', '01', '2022-04-15');

INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id, last_update)
VALUES ('2', '2022-04-12', '2', '101', '2022-04-13', '01', '2022-04-15');

INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id, last_update)
VALUES ('3', '2022-04-13', '3', '102', '2022-04-14', '01', '2022-04-15');

INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id, last_update)
VALUES ('4', '2022-04-14', '4', '104', '2022-04-15', '01', '2022-04-15');

INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id, last_update)
VALUES ('5', '2022-04-15', '5', '105', '2022-04-16', '01', '2022-04-15');



INSERT INTO address (address_id, address, address2, district, city_id, postal_code, phone, last_update)
VALUES ('1', 'Aşağı Mah. Yan Sk. 1/1 Xxx/YYYY', 'Adress 2', 'Aşağı', '01', '1234AB', '678912345','2022-04-15');

INSERT INTO address (address_id, address, address2, district, city_id, postal_code, phone, last_update)
VALUES ('2', 'Aşağı Mah. Yan Sk. 2/2 Xxx/YYYY', 'Adress 2', 'Aşağı', '01', '1234AB', '255511225','2022-04-12');

INSERT INTO address (address_id, address, address2, district, city_id, postal_code, phone, last_update)
VALUES ('3', 'Aşağı Mah. Yan Sk. 3/3 Xxx/YYYY', 'Adress 2', 'Aşağı', '01', '1234AB', '143113453','2022-04-13');

INSERT INTO address (address_id, address, address2, district, city_id, postal_code, phone, last_update)
VALUES ('4', 'Aşağı Mah. Yan Sk. 4/4 Xxx/YYYY', 'Adress 2', 'Aşağı', '01', '1234AB', '2345765','2022-04-17');

INSERT INTO address (address_id, address, address2, district, city_id, postal_code, phone, last_update)
VALUES ('5', 'Aşağı Mah. Yan Sk. 5/5 Xxx/YYYY', 'Adress 2', 'Aşağı', '01', '1234AB', '9876543','2022-04-18');



9- Olusturdugunuz 3 tabloya C ile 5 veri girişi yapin.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

cur.execute('INSERT INTO film VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)', 
(1, 'Esaretin Bedeli', 'Efsane', '1994-01-01', 1, '1 day', 3.5, 3, 5.50, 9.99, '2022-04-19', '3 cds', 'Çok güzel bir film.'))

cur.close()

conn.commit()

conn.close()

-----


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

cur.execute('INSERT INTO film VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)', 
(2, 'Yeşil Yol', 'Efsane', '1995-01-01', 1, '1 day', 3.5, 3, 5.50, 9.99, '2022-04-19', '3 cds', 'Çok güzel bir film.'))

cur.close()

conn.commit()

conn.close()

-----


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

cur.execute('INSERT INTO film VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)', 
(3, 'Schindler\'in Listesi', 'Efsane', '1993-01-01', 1, '1 day', 3.5, 3, 5.50, 9.99, '2022-04-19', '3 cds', 'Çok güzel bir film.'))

cur.close()

conn.commit()

conn.close()


-----

import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

cur.execute('INSERT INTO film VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)', 
(4, 'Forrest Gump', 'Efsane', '1994-01-01', 1, '1 day', 3.5, 3, 5.50, 9.99, '2022-04-19', '3 cds', 'Çok güzel bir film.'))

cur.close()

conn.commit()

conn.close()



-----

import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

cur.execute('INSERT INTO film VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)', 
(5, '3 Idiots', 'Efsane', '2009-01-01', 1, '1 day', 3.5, 3, 5.50, 9.98, '2022-04-19', '3 cds', 'Çok güzel bir film.'))

cur.close()

conn.commit()

conn.close()



10- 3 tablodaki birer veriyi M ile degistirin. +

11- 3 tablodaki birer veriyi K ile degistirin.

UPDATE customer
SET first_name = 'Alican', email = 'alicanbey@yahoo.com'
WHERE customer_id = 101;

UPDATE customer
SET first_name = 'Velican', email = 'velicanbey@yahoo.com'
WHERE customer_id = 102;

UPDATE customer
SET first_name = 'Fatmanur', email = 'fatmanurhanim@yahoo.com', address_id = 9999
WHERE customer_id = 105;


12- 3 tablodaki birer veriyi C ile degistirin.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('UPDATE inventory SET film_id = %s WHERE inventory_id = %s', (5, 1))

cur.close()
conn.commit()
conn.close()

-------------

import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('UPDATE inventory SET film_id = %s WHERE inventory_id = %s', (5, 2))

cur.close()
conn.commit()
conn.close()


-------------

import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('UPDATE inventory SET film_id = %s WHERE inventory_id = %s', (5, 3))

cur.close()
conn.commit()
conn.close()



13- 3 tablonun son satirini M ile silinmiş. +

14- 3 tablonun son satirini K ile silinmiş. +


DELETE FROM customer WHERE customer_id = (SELECT MAX(customer_id) FROM customer);

DELETE FROM film WHERE film_id = (SELECT MAX(film_id) FROM film);

DELETE FROM film_category WHERE film_id = (SELECT MAX(film_id) FROM film_category);



15- 3 tablonun son satirini C ile silinmiş.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('DELETE FROM inventory WHERE inventory_id = (SELECT MAX(inventory_id) FROM inventory)')

cur.close()
conn.commit()
conn.close()



16- 1 tabloyu M ile silindi.+

17- 1 tabloyu K ile silinmiş.

DROP TABLE payment


18- 1 tabloyu C ile silinmiş.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('DROP TABLE inventory')

cur.close()
conn.commit()
conn.close()



19- Kalan tablolardan 1 tanesinin 2 veya 3 sutununu K ile baska bir tablo olarak olusturun.


CREATE TABLE nineteen(
	city_id int,
	city varchar(25),
	country_id varchar (25)
)



20- Kalan tablolardan 1 tanesinin 2 veya 3 sutununu C ile baska bir tablo olarak olusturun.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password =1")

cur = conn.cursor()

comand = '''create table twenty
(
customer_id int PRIMARY KEY NOT NULL,
store_id int ,
first_name varchar (50)
)
'''
cur.execute(comand)

cur.close()

conn.commit()

conn.close()




21- Tablolardan 1 tanesini budamak edin.

22- Tablolardan 1 tanesini keserek edin.

23- Tablolardan 1 tanesini keserek edin.

24- Kesil edilmis tablolari M ile silinmiş.+

25- 2 tabloyu K ile silindi.


DROP TABLE category;
DROP TABLE city;


26- 2 tabloyu silin.++

27- Elimizde veri olan 1 tablo kalmis olmasi lazim. Tabloyu csv olarak bilgisayarınızı yukleyin.

28- Postgresql diziuzundeki son tabloyu da K ile silinmiş.

29- Bilgisayarınızdaki csv yi arayuze ithalat edin.

CREATE TABLE customer (
	customer_id int,
	store_id int,
	first_name varchar (25),
	last_name varchar (25),
	email varchar (50),
	address_id int,
	activebool boolean,
	create_date date,
	last_update date,
	active boolean
);



30- İthalatın bu tabloyu C ile silinmiş.


import psycopg2

conn = psycopg2.connect("dbname = class4 user = postgres password = 1")

cur = conn.cursor()

cur.execute('DROP TABLE customer')

cur.close()
conn.commit()
conn.close()


31- https://www.postgresqltutorial.com/postgresql-sample-database/ linkindeki ornek DB yi bilgisayariniza indirin ve arayuze yukleyin.+

32- DB nizde 15 adet tablo olmasi lazim. Her tabloyu teker teker goruntuleyin ve kolon isimlerine bakarak, 5 tablodaki hangi kolonun PK ve FK olduğunu yazin.

actor tablosunda actor_id PK
address tablosunda address_id PK, city FK
category tablosunda category_id PK
city tablosunda city_id PK, city FK
country tablosunda country_id PK



sorgular? (Asagi'deki sorularıin sayfasınıini ve bu cedakibi bulurken kullandiginiz kodlari yazin)

33- Aksiyon filmlerinin ortalama suresi ne kadar?


SELECT AVG(length) as ortamalama_sure FROM film;


34- En cok personel olan mağaza mı?


SELECT store_id, COUNT(*)
FROM staff
GROUP BY store_id
ORDER BY COUNT(*)
LIMIT 1;



35- 'Gene Willis' adli aktörün filmlerin reytingi nedir?



SELECT actor.actor_id, film_actor.actor_id, film.film_id, film.film_id, film.title, film.rating
FROM actor, film, film_actor
WHERE first_name = 'Gene' AND last_name = 'Willis'



36- Aktif müşteri sayisi nedir?

SELECT COUNT(*) FROM customer WHERE active = 1



37-'C' harfiyle baslayan müziktir?

soru ne istiyor anlayamadım!


38- 4$ den az odeme yapan musterilerin e-posta edresleri nedir?

SELECT email FROM customer

WHERE customer_id IN
(
SELECT customer_id FROM payment
	
WHERE amount < 4
)


39- Moskova'da ikamet eden personel ve müşteri tablosu? (sadece isim/soyisim sütün olsun)

SELECT first_name, last_name FROM customer

WHERE address_id IN
(
SELECT address_id FROM address
	
WHERE city_id = (SELECT city_id FROM city WHERE city = 'Moscow')
)



40- En az kiralanan 5 film?


SELECT title FROM film

WHERE film_id IN (

SELECT film_id FROM inventory

WHERE inventory_id IN (SELECT inventory_id FROM rental)
	
GROUP BY film_id
	
ORDER BY SUM(inventory_id)

LIMIT 5

)



41- 2006 yilinda yayinlanan film filmlerdir?


SELECT title FROM film

WHERE release_year = '2006'