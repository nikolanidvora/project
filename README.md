# Парсинг, систематизация и анализ списка "250 лучших фильмов" Кинопоиска с помощью библиотек Beautiful Soup, Requests и Pandas

# Об области применения испульзуемых библиотек

Данные библиотеки, безусловно, являются из удобным, зачастую необходимым инструментом для исследования в области культурологии. Они могут стать помощниками для прикладных задач классического поля социальных наук, когда исследователю сталкивается с необходимостью обработать большие объемы данных (здесь особенно пригодятся возможности библиотеки Pandas работать с наборами данных, приводить их в табличный или графический вид, изменять анализировать).

В тоже время современная культурология/социология значимимо расширила область своего интереса и исследовательскую оптику, активно ворвавшись в пространство дигитального. Коль скоро культура есть процесс и результат человеческой деятельности, культурологическая оптика предполагает, что объектом изучения может оказаться практически любое явление или артефакт сетевой культуры. Ими могут стать как феномены возникновения и взаимодействий различных комьюнити - групп, форумов, социальных сетей, так и архетиктура, дизайн сайта или даже одной конкретной страницы в интернете. 

Для полноты изучения объектов исследования, а также для удобства их анализа культуролог может работать с данными на уровне кода. Полезными и понятными инструментами инструментами для подобной работы являются библиотеки Requests и Beautiful Soup, которые хорошо дополняют друг друга. Библиотека requests является стандартным инструментом для составления HTTP-запросов в Python. BeautifulSoup позволяет трансформировать сложный HTML-документ в сложное древо различных объектов Python. Это могут быть теги, навигация или комментарии.

# Применение библиотек на примере работы со списком ["250 лучших фильмов"  с сайта Кинопоиск](https://www.kinopoisk.ru/lists/top250/?tab=all).

Исследование кинематографа для культуролога может подразумевать совершенно разное. С одной стороны, это может исследование отдельного фильма, стиля, жанра, автора. С другой стороны, это исслеодвание всего, что находится за рамками кинопроизведения и процесса его создания - культурная политика и исторический контекст, отношение аудитории к кино и ее вкусовые предпочтения. 

В этом смысле, изучение современного кинематографа, как явления массовой культуры, находится за пределами поля исследований эстетики и истории искуства (повторюсь, если рассуждать в этом строгом смысле). Оно отдается на откуп культурологии и междисциплинарным исслеодваниям. 

Умение извлекать списки фильмов, подобные топ 250 Кинопоиска, может быть полезно для сравнения с другими списками, например аналогичным списком сайта IMDB или списком Кинопоиска в прошлом, дальнейшим анализом зрительских предпочтений относящихся к периоду выхода, жанру, стране производства.

