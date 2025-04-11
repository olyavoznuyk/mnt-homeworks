# Домашнее задание к занятию 11 «Teamcity»

**Решение:**

![alt text](./img/screen_1.png)

5. Для deploy будет необходимо загрузить `settings.xml` в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

Взят settings.xml из репозитория, креды такие же

6. pom.xml - изменённые настройки

![alt text](./img/screen_2.png)

7. Артефакт в Nexus

![alt text](./img/screen_3.png)

8. Настройки сборки -> Version Control Settings (миграция сборки)

9. Создайте отдельную ветку `feature/add_reply` в репозитории.

10. `Wake up, hunter! We have a city to burn!`

![alt text](./img/screen_4.png)

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

![alt text](./img/screen_5.png)

12. Сделайте push всех изменений в новую ветку репозитория.

13. Запустились только тесты

![alt text](./img/screen_6.png)

14. Успешная сборка на мастере

![alt text](./img/screen_7.png)

15. Артефактов нет

![alt text](./img/screen_8.png)

16. Путь для артефактов

![alt text](./img/screen_9.png)

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![alt text](./img/screen_10.png)

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.

19. [example-teamcity](https://github.com/olyavoznuyk/example-teamcity)