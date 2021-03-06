# Парсинг, систематизация и анализ списка "250 лучших фильмов" Кинопоиска с помощью библиотек Beautiful Soup, Requests и Pandas

## Об области применения испульзуемых библиотек

Данные библиотеки, безусловно, являются из удобным, зачастую необходимым инструментом для исследования в области культурологии. Они могут стать помощниками для прикладных задач классического поля социальных наук, когда исследователю сталкивается с необходимостью обработать большие объемы данных (здесь особенно пригодятся возможности библиотеки Pandas работать с наборами данных, приводить их в табличный или графический вид, изменять анализировать).

В тоже время современная культурология/социология значимимо расширила область своего интереса и исследовательскую оптику, активно ворвавшись в пространство дигитального. Коль скоро культура есть процесс и результат человеческой деятельности, культурологическая оптика предполагает, что объектом изучения может оказаться практически любое явление или артефакт сетевой культуры. Ими могут стать как феномены возникновения и взаимодействий различных комьюнити - групп, форумов, социальных сетей, так и архетиктура, дизайн сайта или даже одной конкретной страницы в интернете.

Для полноты изучения объектов исследования, а также для удобства их анализа культуролог может работать с данными на уровне кода. Полезными и понятными инструментами инструментами для подобной работы являются библиотеки __Requests__ и __Beautiful Soup__, которые хорошо дополняют друг друга. Библиотека __requests__ является стандартным инструментом для составления HTTP-запросов в __Python__. __BeautifulSoup__ позволяет трансформировать сложный HTML-документ в сложное древо различных объектов __Python__. Это могут быть теги, навигация или комментарии.

![This is an image](https://github.com/nikolanidvora/project/blob/main/folder/welcome%20to%20the%20internet.jpeg)

## Применение библиотек на примере работы со списком ["250 лучших фильмов"  с сайта Кинопоиск](https://www.kinopoisk.ru/lists/top250/?tab=all).

Исследование кинематографа для культуролога может подразумевать совершенно разное. С одной стороны, это может исследование отдельного фильма, стиля, жанра, автора. С другой стороны, это исслеодвание всего, что находится за рамками кинопроизведения и процесса его создания - культурная политика и исторический контекст, отношение аудитории к кино и ее вкусовые предпочтения. 

В этом смысле, изучение современного кинематографа, как явления массовой культуры, находится за пределами поля исследований эстетики и истории искуства (повторюсь, если рассуждать в этом строгом смысле). Оно отдается на откуп культурологии и междисциплинарным исслеодваниям. 

Умение извлекать списки фильмов, подобные топ 250 Кинопоиска, может быть полезно для сравнения с другими списками, например аналогичным списком сайта IMDB или списком Кинопоиска в прошлом, дальнейшим анализом зрительских предпочтений относящихся к периоду выхода, жанру, стране производства.

## Работа с кодом

Чтобы получить список 250 фильмов на сайте Кинопоиска, нам необходима библиотека __Requests__ - она позволяет делать запросы (те самые requests) и брать данные из интернета.
```
import requests
```
Чтобы получить данные мы должны применить к адресу сайта метод библиотеки `get`. Чтобы узнать, какую именно информацию мы получили, можно применить опцию `text`... Но делать этого мы, конечно же, не будем (если честно, я попробовал выгрузить на гитхаб вариант с выводом кода - он получился безумно большим).
```
url = 'https://www.kinopoisk.ru/lists/top250/' 
top = requests.get(url)
```
Код получился нечитаемым (поверьте мне). Справиться с этим поможет другая библиотека, `Beautifulsoup`. Эта библиотека для извлечения данных из файлов `HTML` и `XML`. Она работает с библиотеками для парсинга, чтобы дать естественные способы навигации, поиска и изменения дерева разбора.
```
from bs4 import BeautifulSoup
```
Мы должны передать библиотеке ответ, полученный с помощью __Requests__. Создадим переменную `soup`, передадим ей `top.text` и укажем необходимый формат (насколько я понял, наиболее быстрый и удобный - `lxml`)
```
soup = BeautifulSoup(top.text, 'lxml')
```
Давайте тоже не будем печатать код. Он упорядочен (честно пионерское), теги идут один за одним — теперь мы можем вынимать из кода то, что нам нужно. Для этого просмотрим и проанализируем код страницы "Топ 250". Анализ показывает, что карточки каждого из фильмов лежат в теге `div`.
![This is an image](https://github.com/nikolanidvora/project/blob/main/folder/Снимок%20экрана%202021-10-24%20в%2020.42.06.png)
С помощью команды `find` (и `get` для получения ссылки на фильм) вытащим данные из первой карточки, а затем перепишем код так, чтобы он сработал на все фильмы со страницы. Получаем ссылку на фильм. Она лежит в классе `href` (для него то и пригодится `get`), однако не полностью, поэтому добавим вначале адрес главной страницы сайта.
```
link = 'https://www.kinopoisk.ru/'+soup.find('div', class_='desktop-rating-selection-film-item').find('a', class_='selection-film-item-meta__link').get('href')
print(link)
```
```
https://www.kinopoisk.ru//film/24705/
```
Вытаскиваем русское название фильма.
```
russian_name = soup.find('div', class_='desktop-rating-selection-film-item').find('a', class_='selection-film-item-meta__link').find('p', class_='selection-film-item-meta__name').text
print(russian_name)
```
```
Green Mile, The, 1999
```
Забираем оригинальное название (для нас еще более важно, что в этом же теге располагается год выхода фильма)
```
original_name = soup.find('div', class_='desktop-rating-selection-film-item').find('a', class_='selection-film-item-meta__link').find('p', class_='selection-film-item-meta__original-name').text
print(original_name)
```
```
Green Mile, The, 1999
```
Ищем страну-производителя фильма
```
country = soup.find('div', class_='desktop-rating-selection-film-item').find('a', class_='selection-film-item-meta__link').find('span', class_='selection-film-item-meta__meta-additional-item').text
print(country)
```
```
США
```
Жанр. В коде Кинопоиска страна и жанр имеют одинаковый класс `selection-film-item-meta__meta-additional-item` — а команда `find` находит только первое соответствие нашему запросу. Применим команду `findAll`, чтобы получить список.
```
genre = soup.find('div', class_='desktop-rating-selection-film-item').find('a', class_='selection-film-item-meta__link').findAll('span', class_='selection-film-item-meta__meta-additional-item')[1].text
print(genre)
```
```
фэнтези, драма
```
Рейтинг фильма на Кинопоиске
```
rate = soup.find('div', class_='desktop-rating-selection-film-item').find('span', class_='rating__value rating__value_positive').text
print(rate)
```
```
8.9
```
Чтобы давать меньшую нагрузку на сервер, эксперты советуют импортировать из библиотеки `time` функцию `sleep`. Пытался запустить код без нее - получалось хуже.
```
from time import sleep
```
Сделаем так, чтобы код работал для всех фильмов
```
data = [] #переменную data, в который будем добавлять все переменные, которые запрашиваем.

for p in range(1, 6): #Список топ-250 разбит на 5 страниц по 50 фильмов. Чтобы код прогрузил данные всех фильмов, создадим цикл, который будет последовательно просматривать страницы.
    print(p)

    url = f"https://www.kinopoisk.ru/lists/top250/?page={p}&tab=all" #В каждом цикле меняется номер страницы (в адресной строке она записаны как page=<2,3,4>)
    top = requests.get(url)
    sleep(7)
    soup = BeautifulSoup(top.text, 'lxml')

    films = soup.findAll('div', class_='desktop-rating-selection-film-item') #Создаем поиск всех фильмов с уже знакомой нам командой findAll.

    for film in films:
        link = 'https://www.kinopoisk.ru/'+film.find('a', class_='selection-film-item-meta__link').get('href')
        russian_name = film.find('a', class_='selection-film-item-meta__link').find('p', class_='selection-film-item-meta__name').text
        original_name = film.find('a', class_='selection-film-item-meta__link').find('p', class_='selection-film-item-meta__original-name').text
        country = film.find('a', class_='selection-film-item-meta__link').find('span', class_='selection-film-item-meta__meta-additional-item').text
        genre = film.find('a', class_='selection-film-item-meta__link').findAll('span', class_='selection-film-item-meta__meta-additional-item')[1].text
        rate = film.find('span', class_='rating__value rating__value_positive').text
        data.append([link, russian_name, original_name, country, genre, rate])
```
```
1
2
3
4
5
```
Проверяем, все ли запрашиваемые данные загрузились... И усердно танцуем с бубном.
```
len(data)
```
```
250
```
Ура!!! с ~~сто~~первой попытки!
**Pandas** - библиотека **Python** для анализа данных. Она позволяет работать с данными в табличном виде. В **Pandas** можно изучить набор данных, почистить его, внести изменения, проанализировать и сделать выводы, построить графики и многое другое.
```
import pandas as pd
```
Сейчас библиотека нам нужна, чтобы создать и сохранить таблицу.
```
header = ['Ссылка', 'Русское название', 'Оригинальное название, год', 'Страна', 'Жанр', 'Рейтинг']
df = pd.DataFrame(data, columns=header)
df.to_csv('kinopoisk_top250.csv', sep=';', encoding='utf8')
df
```
```
Ссылка	Русское название	Оригинальное название, год	Страна	Жанр	Рейтинг
0	https://www.kinopoisk.ru//film/435/	Зеленая миля	Green Mile, The, 1999	США	фэнтези, драма	8.9
1	https://www.kinopoisk.ru//film/326/	Побег из Шоушенка	Shawshank Redemption, The, 1994	США	драма	8.9
2	https://www.kinopoisk.ru//film/3498/	Властелин колец: Возвращение короля	Lord of the Rings: The Return of the King, The...	Новая Зеландия, США	фэнтези, приключения	8.8
3	https://www.kinopoisk.ru//film/312/	Властелин колец: Две крепости	Lord of the Rings: The Two Towers, The, 2002	Новая Зеландия, США	фэнтези, приключения	8.8
4	https://www.kinopoisk.ru//film/328/	Властелин колец: Братство Кольца	Lord of the Rings: The Fellowship of the Ring,...	Новая Зеландия, США	фэнтези, приключения	8.8
...	...	...	...	...	...	...
245	https://www.kinopoisk.ru//film/770973/	Вселенная Стивена Хокинга	Theory of Everything, The, 2014	Великобритания, Япония	биография, мелодрама	8.0
246	https://www.kinopoisk.ru//film/634254/	Ип Ман 4	Yip Man 4, 2019	Гонконг, Китай	боевик, биография	8.0
247	https://www.kinopoisk.ru//film/316/	Матрица: Революция	Matrix Revolutions, The, 2003	США	фантастика, боевик	8.0
248	https://www.kinopoisk.ru//film/493208/	Холодное сердце	Frozen, 2013	США, Норвегия	мультфильм, мюзикл	8.0
249	https://www.kinopoisk.ru//film/472/	Индиана Джонс и последний крестовый поход	Indiana Jones and the Last Crusade, 1989	США	приключения, боевик	8.0
```
[Ссылка на код](https://github.com/nikolanidvora/project/blob/main/folder/top250_project.ipynb)

[Ссылка на получившуюся таблицу](https://github.com/nikolanidvora/project/blob/main/folder/kinopoisk_top250.numbers)
