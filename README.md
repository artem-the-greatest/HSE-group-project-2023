# HSE-group-project-2023
Здравствуйте! Вы находитесь в репозитории нашего группового проекта. Здесь вы найдете все материалы нашего проекта и полезные ссылки. 

В рамках изначально выбранной темы мы пробовали спарсить данные с сайта ЦИАН. К сожалению, обойти блокировку известными нам способами нам так и не удалось, поэтому мы обратились к библиотеке cianparser.
Тем не менее в ходе "парсинга" у нас возникло несколько сложностей: 
1. Данные из Москвы отсутствуют в данной библиотеке.
2. Данные других городов (Нижний Новгород, Ижевск) парсились по несколько часов, а затем выходила ошибка. Все наши попытки результаты по первой теме можно посмотреть в файле "попытки по первой теме"

В результате этого нашей командой было принято решение сменить тему. Наша новая тема проекта: 
Анализ и выбор стратегии момент трейдинга. Все наши попытки результаты по первой теме можно посмотреть в файле "попытки по первой теме"

В рамках нашего проекта мы попытаемся построить оптимальную стратегию торговли на импульсах, заложив правила, по которым мы входим в ту или иную позицию.\
В нашей модели на целесообразность действий влияют шесть параметров:
- Веса валют в портфеле
- Порог, при котором мы считаем изменение стоимости значительным
- Количество последовательных предыдущих дней, в течение которых порог был
преодолен

Мы предполагаем, что отклонения обменного курса симметричны, поэтому мы устанавливаем
единый порог в обоих направлениях. Среди всех возможных вариантов мы пытаемся найти исход с самым высоким коэффициентом Шарпа\

*Коэффициент Шарпа - это показатель эффективности, который позволяет инвесторам сравнивать доходность различных портфелей относительно их рисков. Коэффициент подчеркивает волатильность или стандартное отклонение как основной источник риска для многих портфелей, и позволяет инвесторам учитывать его при расчете пригодности различных инвестиций*\

*Коэффициент Шарпа = (доходность портфеля - безрисковая ставка)/стандартное отклонение портфеля*.

В соответствии с заданными значениями параметров, мы покупаем или продаем валюту с определенным весом ("коэффициентом доверия"), в тот момент, когда порог изменения стоимости в одном и том же направлении был преодолен. Если в конкретный день ограничения на покупку не соблюдены, то остаемся в рубле и не покупаем/занимаем иностранную валюту. В противном случае, если какая-то валюта была куплена, то в такой день получаем курс иностранной валюты. Далее мы продаем купленную валюту/закрываем короткую позицию по цене закрытия торгов на следующий день. То есть проекте мы хотим составить эффективную стратегию входа в долгие и короткие позиции (в лонги и шорты) и посмотреть, насколько часто мы будем в итоге совершать сделки с иностранной валютой. Наша основная гипотеза состоит в том, что валюты достаточно редко будут пробивать тот самый "порог повышенной доходности" (а именно это дает нам понять, что нужно бы вложиться в валюту, например), поэтому, в основном, мы останемся в рублевой risk-free ставке. 

Описание данных
В рамках нашего проекта были спасены и используются следующие данные:
- Доллар США - курс доллара к рублю
- Евро - курс евро к рублю
- Фунт стерлингов - курс фунт стерлингов к рублю
- Китайский юань - курс китайского юаня к рублю
- Японская йена - курс японской йены к рублю
- value_RUB - ключевая ставка процента РФ
- value_USD - индекс LIBOR USD overnight 
- value_EUR - индекс LIBOR EUR overnight 
- value_GBP - индекс LIBOR GBP 3m 
- value_JPY - индекс LIBOR JPY 1m 
- value_CNY - индекс SHIBOR CNY overnight 
Описание индексов: 
1. Индекс LIBOR - это самая распространённая в мире средневзвешенная процентная ставка по краткосрочным межбанковским кредитам. Лондонская межбанковская ставка предложения (LIBOR, London Interbank Offered Rate) - это процентная ставка, по которой банки одалживают средства на Лондонском межбанковском рынке.

2. SHIBOR (аббревиатура от Shanghai Interbank Offered Rate) – Шанхайская межбанковская ставка предложения, то есть ставка, по которой банки готовы предоставлять необеспеченные долги в юанях (RMB) на различные сроки. 

Рассматриваемый период: 2015-05-15 - 2023-12-05 


Данные по индексам парсились с: 
http://iborate.com/jpy-libor/

https://www.investing.com/rates-bonds/shibor-overnight-historical-data

Данные по курсам парсились с:https://cbr.ru/currency_base/dynamics/?UniDbQuery.Posted=True&UniDbQuery.so=1&UniDbQuery.mode=1&UniDbQuery.date_req1=&UniDbQuery.date_req2=&UniDbQuery.VAL_NM_RQ=R01035&UniDbQuery.From=15.05.2015&UniDbQuery.To=15.05.2023

Все питоновские тетрадки мы дублируем как в ipynb, так и в hmtl, чтобы не слетали графики. Парсинг данных и предобработку можно найти в файлах с соответствующими названиями. Построение стратегии торговли и выводы по ней в файле "Стратегия". Также с помощью методов машинного оубчения мы строили предсказывающую курс некоторых валют модель, измеряли ее качество, чтобы использовать ее алгоритмы в глобальных целях проекта: чтобы потом инвестор мог предсказывать обратный курс валюты (без сильных шоков) и принимать соответствующие решения. Работу по этой части можно найти в отдельном файле "Модель"





Выводы по проекту: как нам кажется, мы не смогли построить мега-эффективную модель на основе "весов доверия" к валютам - очень много доходностей было отрицательными, согласно нашей стратегии, хотя общая доходность возрастала бы при применении ее на данных тестовой выборки, то есть позже 2020 года.

