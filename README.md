### Задание

1. Используя команду cat в терминале операционной системы Linux, создать два файла "Домашние животные"
   (заполнив файл "собаками", "кошками", "хомяками") и "Вьючные животные" (заполнив файл "лошадьми", "верблюдами" и "
   ослами"),
   а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя "Друзья
   человека".
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.
4. Установить и удалить deb-пакет с помощью dpkg.
5. Выложить историю команд в терминале Ubuntu.
6. Нарисовать диаграмму, в которой есть классы - родительский, домашние животные и вьючные животные,
   в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут:
   лошади, верблюды и ослы.
7. В подключенном MySQL репозитории создать базу данных “Друзья человека”.
8. Создать таблицы с иерархией из диаграммы в БД.
9. Заполнить низкоуровневые таблицы именами (животных), командами которые они выполняют и датами рождения.
10. Удалить из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку.
    Объединить таблицы "лошади", и "ослы" в одну таблицу.
11. Создать новую таблицу "молодые животные" в которую попадут все животные старше 1 года, но младше 3 лет
    и в отдельном столбце, с точностью до месяца, подсчитать возраст животных в новой таблице.
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.
13. Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных.
    В программе должен быть реализован следующий функционал:

    14.1. Завести новое животное;

    14.2. Определять животное в правильный класс;

    14.3. Увидеть список команд, которое выполняет животное;

    14.4. Обучить животное новым командам;

    14.5. Реализовать навигацию по меню.

15. Создайте класс Счетчик, у которого есть метод add(), увеличивающий̆ значение внутренней̆ int переменной̆ на 1
    при нажатии “Завести новое животное”. Сделайте так, чтобы с объектом такого типа можно было работать в блоке
    try-with-resources.
    Нужно бросить исключение, если работа с объектом типа счетчик была не в ресурсном try и/или ресурс остался открыт.
    Значение считать в ресурсе try, если при заведения животного заполнены все поля.

   #### 1.
![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/1.png)
   #### 2.
![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/2.png)
   #### 3.
   ![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/3_1.png)
   ![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/3_2.png)
   ![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/3_3.png)
   #### 4.
   ![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/4.png)
   #### 5.
   <details>
    <summary>Команды (развернуть)</summary>

```bash
1. mkdir final

2. cd final

3. cat > "Домашние животные"

4. cat > "Вьючные животные"

5.  cat "Домашние животные" "Вьючные животные" > "Друзья человека" 

6.  mkdir new_directory 

7.  mv "Друзья человека" new_directory/

8. cd new_directory/

```

</details>

   #### 6.
   ![](https://github.com/AlexanderKorepin/AlexanderKorepin-Final_home_work/blob/main/Foto/diagram.jpg).
   
   #### 7. Создать таблицы с иерархией из диаграммы в БД

   ```sql
   CREATE TABLE Commands
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       description varchar(255)
   );
   
   
   CREATE TABLE AnimalGroup
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30)
   );
   
   CREATE TABLE AnimalGenius
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       group_id INT,
       FOREIGN KEY (group_id) REFERENCES AnimalGroup (id)
       ON DELETE CASCADE ON UPDATE CASCADE
   );
   
   CREATE TABLE KennelAnimal
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       birthDate DATE,
       genius_id INT,
       FOREIGN KEY (genius_id) REFERENCES AnimalGenius (id)
       ON DELETE CASCADE ON UPDATE CASCADE
   );
   
   CREATE TABLE AnimalCommands
   (
       animal_id INT NOT NULL,
       command_id INT NOT NULL,

       PRIMARY KEY (animal_id, command_id),
       FOREIGN KEY (animal_id) REFERENCES KennelAnimal (id)
        ON DELETE CASCADE ON UPDATE CASCADE,
       FOREIGN KEY (command_id) REFERENCES Commands (id)
        ON DELETE CASCADE  ON UPDATE CASCADE
   );
   ```
#### 8. Заполнить низкоуровневые таблицы именами (животных), командами которые они выполняют и датами рождения
   
   ```sql
    USE HumanFriends;

   INSERT INTO commands(name)
   VALUES
    ('Принести тапки'),
    ('Вертеться в колесе'),
    ('Галоп!'),
    ('Поклон!'),
    ('КАШ!');
   
   INSERT INTO AnimalGroup (name)
   VALUES
    ('Вьючные животные'),
    ('Домашние животные');
   
   INSERT INTO AnimalGenius (name, group_id)
   VALUES
    ('Лошадь', 1),
    ('Верблюд', 1),
    ('Осел', 1),
    ('Кошка', 2),
    ('Собака', 2),
    ('Хомяк', 2);
   
   INSERT INTO KennelAnimal (name, birthDate, genius_id)
   VALUES
    ('Гнедой', '2021-02-04', 1),
    ('Гнедой_2', '2022-12-01', 1),
    ('Тупица', '2020-08-24', 3),
    ('Рыжий', '2022-05-20', 2),
    ('Песик', '2023-01-24', 5),
    ('Хомяк', '2022-12-20', 6),
    ('Эльза', '2022-07-12', 4);
   
   INSERT INTO AnimalCommands (animal_id, command_id)
   VALUES
    (1, 3), (2, 3), (2, 4), (3, 4),
    (4, 5), (5, 1), (5, 4), (6, 2),
    (7, 1);
   ```
#### 9. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
   ```sql
      USE HumanFriends;
      DELETE FROM KennelAnimal WHERE genius_id = 2;
   
      CREATE TABLE HorseAndDonkey AS
	  SELECT * from KennelAnimal WHERE genius_id = 1
      UNION
      SELECT * from KennelAnimal WHERE genius_id = 3;
   ```
#### 10. Создать новую таблицу “молодые животные” в которую попадут всеживотные старше 1 года, но младше 3 лет и в отдельном столбце с точностьюдо месяца подсчитать возраст животных в новой таблице

   ```sql
      CREATE TABLE YoungAnimals AS
         SELECT id, name, birthDate, 
         datediff(curdate(),birthDate) DIV 31 as age, genius_id 
         from KennelAnimal 
         WHERE date_add(birthDate, INTERVAL 1 YEAR) < curdate() 
               AND date_add(birthDate, INTERVAL 3 YEAR) > curdate();
   ```
#### 11. Объединить все таблицы в одну, при этом сохраняя поля, указывающие напрошлую принадлежность к старым таблицам.
   ```sql
      SELECT id, name, birthDate, genius_id FROM HorseDonkey
      UNION
      SELECT id, name, birthDate, genius_id FROM YoungAnimals;
   ```
