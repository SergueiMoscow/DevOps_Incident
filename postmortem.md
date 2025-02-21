## Постмортем на инцидент GitHub:
https://habr.com/ru/post/427301/

https://github.blog/2018-10-30-oct21-post-incident-analysis/

##### Краткое описание инцидента
21 октября 2018 года в 22:52 UTC платформа GitHub столкнулась с инцидентом, вызвавшим деградацию работы сервиса на протяжении 24 часов и 11 минут.
##### Причина инцидента
Во время запланированного технического обслуживания произошёл кратковременный разрыв связи между узлом сети и основным центром данных из-за замены оборудования передачи данных.
##### Воздействие
Инцидент привел к деградации работы платформы GitHub на протяжении более 24 часов, что затронуло доставку вебхуков, сборку страниц GitHub Pages и доступность основных систем.
##### Обнаружение
Система мониторинга зафиксировала многочисленные ошибки спустя пару минут после начала инцидента, что быстро сигнализировало о возникших проблемах.
##### Реакция
Команда оперативно ввела режим частичной деградации, приостановив отдельные сервисы, и разработала стратегию восстановления, включающую восстановление данных, синхронизацию реплик и возврат к стабильной топологии.
##### Восстановление
Работа основных систем была постепенно восстановлена за счет увеличения ресурсов обработки и завершения обработки очередей задач; нормальное состояние системы было достигнуто спустя 24 часа после начала инцидента.
##### Таймлайн
- **21 октября 2018 года, 22:52 UTC** Во время запланированного технического обслуживания замена оборудования для передачи на 100G привела к кратковременному разрыву связи между узлом сети US East Coast и основным центром данных на Восточном побережье.
- **21 октября 2018 года, 22:54 UTC** Система мониторинга начала фиксировать многочисленные ошибки.
- **21 октября 2018 года, 23:09 UTC** Команда ввела режим частичной деградации: были приостановлены доставки вебхуков и сборка GitHub Pages.
- **22 октября 2018 года, 00:05 UTC** Была разработана стратегия восстановления: восстановление из резервных копий, синхронизация реплик, возврат к стабильной топологии обслуживания.
- **22 октября 2018 года, 11:12 UTC** Главные базы данных были возвращены к центру данных на Восточном побережье.
- **22 октября 2018 года, 13:15 UTC** Команда увеличила ресурсы обработки для ускорения синхронизации реплик.
- **22 октября 2018 года, 16:24 UTC** Ситуация стабилизировалась, однако оставалась очередь задач, связанных с вебхуками и Pages, что потребовало дополнительного времени на завершение их обработки.
- **22 октября 2018 года, 23:03 UTC** Очередь была полностью обработана, система возвращена в нормальное состояние.
##### Последующие действия
- Необходимо настроить Orchestrator для локальных лидеров, чтобы избежать автоматического переноса операций записи между регионами при сетевых сбоях.
- Будет ускорён переход на более наглядный механизм статусов, который позволит детализировать состояние каждого сервиса платформы.
- Проект по внедрению активной работы из нескольких дата-центров (active/active/active) приобретает высший приоритет. Цель — исключение сбоев уровня центра обработки данных.
- Мы переходим к систематическому тестированию отказов (chaos engineering), чтобы лучше понимать поведение системы в редких сценариях.
