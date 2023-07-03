# Исследование LinkedIn

## Для доступа к красивой визуализации моделей рекомендуется перейти по [ссылке](https://nbviewer.org/github/anshilina/hackathon_yandex/blob/main/topic_modelling_linkedin_mentors.ipynb)

Проект был выполнен в рамках хаккатона Яндекс Практикума. Исследование посвящено теме наставничества, менторства, а также включает работу с профилем ЦА. 

**Цель: провести исследование по теме наставничества и менторства на основании контента социальной сети LinkedIn, размещенного в открытом доступе, созданного целевой аудиторией**

**Задачи исследования:**

1. Определить топ-10 тем в направлении наставничества на основании наибольшего охвата, используя теги *наставничество, менторство, коучинг, mentorship, mentor, coaching, buddy*
2. Определить топ-10 популярных тем по реакциям
3. Дополнить профили целевой аудитории новыми параметрами

**Этапы исследования**

1. Подготовка и предобработка данных
- создание кода для сбора данных
- сбор данных
- предобработка данных: удаление эмодзи, стоп-слов и слов паразитов, приведение слов в начальную форму, удаление лишних текстовых символов, создание таблицы с информацией о пользователе, его должности и опыте работы, текстом публикаций и количеством реакций
2. Анализ данных
- анализ и выделение 100 постов с большей частотой встречающихся слов
- Topic Modeling на всех постах
- Topic Modeling на самых популярных постах (по числу реакций)
- выделение топ-10 ключевых слов и интерпретация тем

**Данные**

Основной источник данных – социальная сеть LinkedIn, где менторы и наставники оставляли публикации. Результаты парсинга данных доступны в файле [**russian_mentors_raw.csv**](https://github.com/anshilina/hackathon_yandex/blob/main/russian_mentors_raw.csv). Предобработанные данные (русскоязычные и англоязычные публикации) доступны в файлах [**data_english.csv**](https://github.com/anshilina/hackathon_yandex/blob/main/data_english.csv) и [**data_russian.csv**](https://github.com/anshilina/hackathon_yandex/blob/main/data_russian.csv). Были построены отдельные языковые модели на русскоязычных и англоязычных текстах.

Нам доступны данные о пользователях (имя, место работы, ссылка на аккаунт), а также его посты и реакции к ним. Все публикации пользователей были загружены в формате вложенных списков со структурой [['ТЕКСТ ПУБЛИКАЦИИ', 'КОЛИЧЕСТВО РЕАКЦИЙ'], ['ТЕКСТ ПУБЛИКАЦИИ', 'КОЛИЧЕСТВО РЕАКЦИЙ'] и т.д.]. Такая структура может быть легко преобразована как в отдельные корпуса текстов и реакции к ним, так и в один единый текст от каждого автора. Продробнее об этом – на этапе предобработки данных.

**Библиотеки**

*pandas, time, re, bs4, selenium, pycld2, pymystem3, nltk, gensim, pyLDAvis, matplotlib.pyplot, IPython, logging*

Подробная информация о версиях библиотек доступна в файле [**requirements.txt**](https://github.com/anshilina/hackathon_yandex/blob/main/requirements.txt).

### Результаты исследования

*Топ-10 тем по ключевым словам.*

Темы расположены по частоте встречаемости в публикациях.

- **Тема 1: истории о работе ментором**

*Ключевые слова: ментор, работа, менторинг, поддержка, проходить, помогать, коучинг, находить, понимать, работать, а также цель, курс, рассказывать*

В публикациях на эту тему наставники рассказывают о своей профессии: цели, проекты, курсы, а также о коучинге и поддержке начинающих специалистов.

- **Тема 2: истории о работе в сфере аналитики данных, менторы делятся своим опытом работы**

*Ключевые слова: бизнес, компания, клиент, проект, сессия, хороший, продукт, рынок, интернет, датасет, модель, а также возможность, книга, понимание*

Многие наставники в первую очередь сами являются дата саентистами и аналитиками данных, поэтому многие их публикации посвящены рассказам о своей основной деятельности.

- **Тема 3: поиск работы в сфере дата саенс**

*Ключевые слова: рынок, вакансия, сайт поиск, машинное обучение, встреча, навык, коуч, учиться, конверсия, граница (поиск работы за границей) и др.*

Также наставники рассказывают о поиске работы (в т.ч. за границей), делятся инсайдами рынка трудоустройства, делятся новыми вакансиями, анонсами тематических встреч.

- **Тема 4: навыки, востребованные у работодателей**

*Ключевые слова: опыт, команда, модель, знание, тестирование, компания, система, бизнес, собес (собеседование), опыт работы, нужный, а также развитие, инструмент, использовать, мочь, гайд, язык*

Еще одна тема, связанная трудоустройством – это навыки, которые по мнению работодателей необходимы для соискателя на позицию в сфере дата саенс. Другими словами, какие навыки необходимо прокачать тем, кто хочет трудоустроиться в этой сфере.

- **Тема 5: перспективы экономического роста и развития в сфере дата саенс**

*Ключевые слова: рост, реклама, продавать, бизнес, предприниматель, человек, скорость, косвенный конкурент, сверхзадача, изменение, а также рубль, млн., делать, деньги*

Наставники также обсуждают перспективы IT-специалистов, проектов, в т.ч. стартапы, предпринимателей – эта тема связана с бизнесом и экономикой.

- **Тема 6: рассказы о задачах наставников и менторов**

*Ключевые слова: групповой менторинг, вебинар, карьерный, коуч, друг, партнер, команда, опытный, разработка, мастер, научиться, продолжать, а также специфические: Практикум, Москва*

Не спроста данная тема на графике расположена близко к **Теме 1** – они близки по содержанию. Но в отличие от темы 1, где фокус повествования смещен на описание профессии в целом, в **Теме 6** менторы рассказывают о задачах, которые перед ними стоят: групповой менторинг, проведение вебинаров и карьерных консультаций, работа в команде, обучение, поддержка, ментор – это друг для своих подопечных. В теме также часто упоминался Практикум – скорее всего менторы из Яндекс Практикума часто публикуют посты на эту тему.

- **Тема 7: полезные советы от менторов**

*Ключевые слова: полезно, качество, каждый, профессия, требование, курс, аналитика, практически, осознавать, история, расширение, круг, прочитывать*

Менторы также в публикациями часто делаться полезными советами, ссылками на курсы, книги, полезные для расширения кругозора и погружения в профессию аналитика или дата саентиста.

- **Тема 8: важность стратегического планирования, как разработать стратегию своего карьерного развития**

*Ключевые слова: план, цель, работать, регулярный, горизонт (планирования), движение, двигаться, планирование, планировать, копилочка, стратегический, достижение, подводить, итог, завтра, ограничение, месяц* 

В качестве отдельного тематического блока можно выделить стратегическое планирование: менторы часто пишут о стратегиях карьерного развития, подчеркивают необходимость ставить чёткие цели и строить планы, двигаться на пути их достижения.

- **Тема 9: рассказы о методиках обучения, в т. ч. от коллег**

*Ключевые слова: методика, учет, развитие, решение, эксперт, обучение, цифра, стоить искать, анализ, проводить, коллега*

Темы 9 и 10 наименее популярные (их меньше всего поднимают в своих публикациях менторы). **Тема 9** скорее посвещена методикам менторинга и наставничества, скорее всего аудитория таких постов – коллеги-менторы. 

- **Тема 10: образование, освоение навыков в сфере анализа данных, анонсы и приглашения на вебинары**

*Ключевые слова: аналитика, тема, данные, практика, мониторинг, приветствовать, вебинар, ревьюер, оценка, курс, школа, навык, быстро, а также работа, любить*

Исходя из ключевых слов в **Теме 10**, можно предположить, что эти публикации направлены на анонсирование вебинаров, курсов, школ и матерских, возможность получить практических опыт в сфере аналитики, по работе с данными.

*Топ-5 популярных тем по реакциям.*

Темы расположены по частоте встречаемости в публикациях.

- **Тема 1: Поиск работы**

*Ключевые слова:* вакансия, работа, опыт, компания, подходить, тестирование, опыт работа, искать, новый, сайт поиск, поиск работа, разработчик

Публикации, связанные с поиском работы, открытыми вакансиями.

- **Тема 2: Приглашение на групповой менторинг**

*Ключевые слова:* групповой менторинг, ментор, менторинг, коучинг, коуч, получать, становиться, научиться, результат, профессия

Приглашение на групповой менторинг, рассказы о результатах работы с менторами и коучами.

- **Тема 3: Планирование, постановка целей**

*Ключевые слова:* план, цель, курс, планирование, горизонт, книга, регулярный, собеседование, групповой менторинг, вместе

Полезные советы, планирование в рамках программ группового менторинга. Но акцент смещен на стратегию работы в рамках курсов менторов (в **Теме 2** основной фокус на приглашение в курсы).

- **Тема 4: Задачи менторов**

*Ключевые слова:* сессия, навык, делать, коучинг, хотеть, менторинг, развивать, понимание, помогать, урок, учиться, создавать

Рассказы о задачах менторов, какие навыки развивают, с чем помогают.

- **Тема 5: Мотивирующие посты**

*Ключевые слова:* проект, решение, принимать, анализ, вовлекать, заниматься, браться, находить, апатия, страстный, полезно

Исходя из ключевых слов, тексты публикаций направлены на мотивацию своей аудитории делать, заниматься, браться, находить, принимать решения.

### Выводы

На русском языке менторы пишут в основном о **своей профессии, задачах наставников и менторов, работе в сфере анализа данных, поиске работы и навыках, востребованных у работодателя**. Они делятся **полезными советами и ресурсами**, рассказывают о своих **методиках поддержки начинающих специалистов**. Отдельная тема посвящена **важности стратегического планирования**. Также менторы публикуют **анонсы** различных мероприятий. 

Среди самых популярных (по количеству реакций) тем на русском языке – **поиск работы, приглашения на групповой менторинг, планирование и постановка целей, а также мотивирующие посты**: тексты публикаций направлены на мотивацию своей аудитории делать, заниматься, браться, находить, принимать решения.

На английском языке наставники пишут на схожие темы. Акцент больше смещен на их **карьерные успехи**, они также говорят о **возможностях для роста и развития**. Среди самых популярных (по количеству реакций) тем на английском языке – сообщения о **начале новой позиции, истории о проектах, возможностях для стажировок в различных компаниях**.

