# Netflix
| Целевая аудитория                                 | Россия |
|---------------------------------------------------|--------|
| Размер ЦА                                         | 80млн  |
| Количество посетителей в сутки                    | 800тыс |
| Используемые данные подписчиком в час (в среднем) | 3Гб    |
| Среднее время просмотра | 3.2 часа    |

Источник: https://backlinko.com/netflix-users
## Расчет нагрузки
В сутки Нетфликс посещает 100тыс пользователей => в месяц нетфликс посещает 30 * 8 * 10^5 пользователей.

Главная страница сервиса весит около 0.6 Мб => 4 Тб в месяц нужно отдавать в среднем

Так как нам нужно хранить видео в разных форматах, то для дальнейших расчетов воспользуемся готовым калькулятором (https://toolstud.io/video/filesize.php).
Расчеты будем производить для самых популярных (>1%) разрешений экранов (данные: https://ru.screenresolution.org/year-2020/)
Частота кадров видео - 60 кадров

| Разрешение | Объем (Гб) | 
|------------|------------|
| 1920х1080  | 12.53      |
| 1366х768   | 6.34       |
| 1536х864   | 8.02       |
| 1366х768   | 6.34       |

Получается одно видео в среднем будет занимать ~34Гб. На официальной статистике нетфликса сказано, что контента на 36000 =>
36000 * 34 = 1200Тб

| качество | трафик      | 
|----------|-------------|
| Minimum  | 0.5 Мбит/с  |
| Medium   | 1.5 Мбит/с  |
| SD       | 3.0 Мбит/с  |
| HD       | 5.0 Мбит/с  |
| Ultra HD | 25.0 Мбит/с |

Источник: https://www.sony.ru/electronics/support/speakers-wired-speakers/sa-cs9/articles/00022091

В среднем десктоп: HD-30% и Medium-70% => 8 * 10^5 * 0.41 * (0.3 * 0.3 + 0.7 * 0.09) = 48 Тб
В среднем смартфон: HD-30% и Medium-70% => 8 * 10^5 * 0.59 (0.3 * 0.3 + 0.7 * 0.09) = 56 Тб
104 Тб в среднем в сутки.

#### средний трафик:
104 * 10^3 / (24 * 60 * 60) = 9.6 Гбит/сек
#### пиковый трафик:
пусть 1.6млн человек онлайн: 244 * 10^3 / (24 * 60 * 60) = 22.4 Гбит/сек

| запрос | нагрузка, rps | 
|------------|------------|
| профиль | 130 * 8 * 10^5 / (24 * 60 * 60) = 1200 |
| страница контента | 300 * 8 * 10^5 / (24 * 60 * 60) = 2700 |
| главная страница | 150 * 8 * 10^5 / (24 * 60 * 60) = 1380 |
| favorites | 5 * 8 * 10^5 / (24 * 60 * 60) = 46 |
| воспроизведение контента | 100 * 8 * 10^5 / (24 * 60 * 60) = 925 |

## Логическая схема
![img.png](src/base.png)
