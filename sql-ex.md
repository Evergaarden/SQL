

**Краткое содержание БД "Компьютерная фирма"**:

Схема БД состоит из четырех таблиц:

1) **Product** (**maker**, **model**, **type**) Таблица представляет:
<ul type="circle"><li><b>maker</b> - производитель,</li> 
<li>model - номер модели,</li>
<li>**type** - тип ('PC' - ПК, 'Laptop' - ПК-блокнот или 'Printer' - принтер).</li> 
Предполагается, что номера моделей в таблице Product уникальны для всех производителей и типов продуктов
</ul>
2) **PC** (**code**, **model**, **speed**, **ram**, **hd**, **cd**, **price**) В таблице PC:
<ul type="circle"><li>**code** (для каждого ПК, однозначно определяемого уникальным кодом),</li>
<li>**model** (внешний ключ к таблице Product),</li>
<li>**speed** - скорость процессора в мегагерцах,</li> 
<li>**ram** - объем памяти в мегабайтах,</li> 
<li>**hd** - размер диска в гигабайтах,</li> 
<li>**cd** - скорость считывающего устройства (например, '4x'),</li>
<li>**price** - цена</li>
</ul>
3) **Laptop** (**code**, **model**, **speed**, **ram**, **hd**, **price**, **screen**) В таблице Laptop:
<ul type="circle"><li>**code** (для каждого ПК, однозначно определяемого уникальным кодом),</li>
<li>**model** (внешний ключ к таблице Product),</li>
<li>**speed** - скорость процессора в мегагерцах,</li>
<li>**ram** - объем памяти в мегабайтах,</li>
<li>**hd** - размер диска в гигабайтах,</li>
<li>**price** - цена,</li>
<li>**screen** - размер экрана в дюймах.</li></ul>

4) **Printer** (**code**, **model**, **color**, **type**, **price**)  В таблице Printer: 
<ul type="circle">**code** - уникальный код,
<li>**model** - модель принтера,</li>
<li>**color** - для каждой модели принтера указывается, является ли он цветным  ('y', если цветной),</li> 
<li>**type** - тип принтера (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix'),</li>
<li>**price** - цена.</li></ul>

======================================================================

<br><b>Задание 1:</b>
<br>Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd


<br><b>Содержание запроса:</b>
<br>SELECT model, speed, hd
<br>FROM PC
<br>WHERE price < 500



====================
**Задание 2:**
Найдите производителей принтеров. Вывести: maker


**Содержание запроса:**
SELECT DISTINCT maker
FROM Product
WHERE type = 'Printer'


====================
**Задание 3:**
Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.


**Содержание запроса:**
SELECT model, ram, screen 
FROM Laptop 
WHERE price > 1000


====================
**Задание 4:**
Найдите все записи таблицы Printer для цветных принтеров.


**Содержание запроса:**
SELECT * 
FROM Printer
WHERE color = 'y'


====================
**Задание 5:**
Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.


**Содержание запроса:**
SELECT model, speed, hd
FROM PC
WHERE (CD = '12x' OR CD = '24x') AND price < 600


====================
**Задание 6:**
Для каждого производителя, выпускающего ПК-блокноты c объемом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

**Содержание запроса:**
SELECT DISTINCT Product.maker, Laptop.speed
FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
WHERE Laptop.hd >= 10 AND Product.type = 'Laptop'


======================
**Задание 7:**
Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

**Содержание запроса:**
SELECT DISTINCT Product.model, pc.price
FROM Product INNER JOIN PC ON Product.model = PC.model
WHERE maker = 'B'
UNION
SELECT DISTINCT Product.model, Laptop.price
FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
WHERE maker = 'B'
UNION
SELECT DISTINCT Product.model, Printer.price
FROM Product INNER JOIN Printer ON Product.model = Printer.model
WHERE maker = 'B'


======================
**Задание 8:**
Найдите производителя, выпускающего ПК, но не ПК-блокноты.

**Содержание запроса:**
SELECT DISTINCT maker
FROM Product
WHERE type = 'pc'
EXCEPT
SELECT DISTINCT maker
FROM Product
WHERE type = 'laptop'


======================
**Задание 9:**
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

**Содержание запроса:**
SELECT DISTINCT Product.maker
FROM Product INNER JOIN PC ON Product.model = PC.model
WHERE PC.speed >= 450


======================
**Задание 10:**
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

**Содержание запроса:**
SELECT DISTINCT model, price
FROM Printer 
WHERE price = (SELECT MAX(price)
FROM Printer)


======================
**Задание 11:**
Найдите среднюю скорость ПК

**Содержание запроса:**
SELECT AVG(speed)
FROM PC


======================
**Задание 12:**
Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

**Содержание запроса:**
SELECT AVG(speed) 
FROM Laptop
WHERE price > 1000


======================
**Задание 13:**
Найдите среднюю скорость ПК, выпущенных производителем A.

**Содержание запроса:**
SELECT AVG(PC.speed) AS AVG_speed
FROM PC INNER JOIN Product ON Product.model = PC.model
WHERE maker = 'A'



======================
**Задание 14:**
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

**Содержание запроса:**
SELECT DISTINCT Ships.class, Ships.name, Classes.country
FROM Classes INNER JOIN Ships ON Classes.class = Ships.class
WHERE numGuns >= 10


======================
**Задание 15:**
Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

**Содержание запроса:**
SELECT HD 
FROM PC
GROUP BY HD
HAVING COUNT(model) >= 2

======================
**Задание 19:**
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.

**Содержание запроса:**
SELECT DISTINCT Product.maker, AVG(screen) AS Avg_screen
FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
GROUP BY maker


======================
**Задание 20:**
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

**Содержание запроса:**
SELECT maker, COUNT(model) AS Count_Model
FROM Product
WHERE type = 'PC'
GROUP BY maker
HAVING COUNT(model) >= 3

======================
**Задание 21:**
Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.

**Содержание запроса:**
SELECT DISTINCT Product.maker, MAX(price) AS Max_price
FROM Product INNER JOIN PC ON Product.model = PC.model
GROUP BY maker


======================
**Задание 22:** 
Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.

**Содержание запроса:**
SELECT speed, AVG(price) AS Avg_price
FROM PC 
WHERE speed > 600
GROUP BY speed


======================
**Задание 23:** 
Найдите производителей, которые производили бы как ПК
со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц.
Вывести: Maker


**Содержание запроса:**
SELECT Product.maker 
FROM Product INNER JOIN PC ON Product.model = PC.model
WHERE type = 'PC' AND speed >= 750
INTERSECT
SELECT Product.maker 
FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
WHERE type = 'Laptop' AND speed >= 750


======================
**Задание 24:**
Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.

**Содержание запроса:**
WITH Max_price AS
(SELECT model, MAX(price) AS price_1
FROM PC
GROUP BY model
UNION
SELECT model, MAX(price) as price_1
FROM Laptop
GROUP BY model
UNION
SELECT model, MAX(price) as price_1
FROM Printer
GROUP BY model)
SELECT model 
FROM Max_price
WHERE price_1 = (SELECT MAX(price_1) FROM Max_price)






















