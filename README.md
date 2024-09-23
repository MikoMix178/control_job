Итоговая контрольная работа
Информация о проекте
Необходимо организовать систему учета для питомника в котором живут
домашние и вьючные животные.
Как сдавать проект
Для сдачи проекта необходимо создать отдельный общедоступный
репозиторий(Github, gitlub, или Bitbucket). Разработку вести в этом
репозитории, использовать пул реквесты на изменения. Программа должна
запускаться и работать, ошибок при выполнении программы быть не должно.
Программа, может использоваться в различных системах, поэтому необходимо
разработать класс в виде конструктора
Задание
1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.
4. Установить и удалить deb-пакет с помощью dpkg.
5. Выложить историю команд в терминале ubuntu
6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).
7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”
8. Создать таблицы с иерархией из диаграммы в БД
9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения
10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
11.Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
13. Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных.
В программе должен быть реализован следующий функционал:
14. 1. Завести новое животное
    2. определять животное в правильный класс
    3. увидеть список команд, которое выполняет животное
    4. обучить животное новым командам
    5. Реализовать навигацию по меню
15. Создайте класс Счетчик, у которого есть метод add(), увеличивающий̆
значение внутренней̆int переменной̆на 1 при нажатие “Завести новое
животное” Сделайте так, чтобы с объектом такого типа можно было работать в
блоке try-with-resources. Нужно бросить исключение, если работа с объектом
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение
считать в ресурсе try, если при заведения животного заполнены все поля.


# 1: Создание файлов и их объединение
```bash
echo -e "Dog\nCat\nHamster" > domestic_animals.txt
```
```bash
echo -e "Horse\nCamel\nDonkey" > pack_animals.txt
```
```bash
cat domestic_animals.txt pack_animals.txt > combined_animals.txt
```
```bash
cat combined_animals.txt
```
```bash
mv combined_animals.txt human_friends.txt
```
# 2: Создание директории и перемещение файла
```bash
mkdir my_animals
```
```bash
mv human_friends.txt my_animals/
```
# 3: Подключение дополнительного репозитория MySQL и установка пакета
```bash
sudo add-apt-repository 'deb http://repo.mysql.com/apt/ubuntu/ bionic mysql-5.7'
```
```bash
sudo apt update
```
```bash
sudo apt install mysql-server
```
# 4: Установка и удаление deb-пакета с помощью dpkg
```bash
wget http://mirrors.kernel.org/ubuntu/pool/universe/h/htop/htop_3.0.5-3_amd64.deb
```
```bash
sudo dpkg -i htop_3.0.5-3_amd64.deb
```
```bash
sudo dpkg -r htop
```
# 5: История команд
```bash
history > command_history.txt
```
# 6: Диаграмма классов
![image](https://github.com/user-attachments/assets/4234a4c1-f98b-4293-8dad-d1ad3cbd6bfb)


# 7: Создание базы данных
```bash
sudo mysql
```
```sql
CREATE DATABASE human_friends;
```
# 8: Создание таблиц
```sql
CREATE TABLE Dog (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    commands VARCHAR(255),
    birth_date DATE
);
```
Повторить для всех классов (кошки, хомяки, лошади, верблюды, ослы).

# 9: Заполнение таблиц
```sql
INSERT INTO Dog (name, commands, birth_date) VALUES ('Bobik', 'Sit', '2022-05-01');
```
# 10: Удаление верблюдов и объединение таблиц
```sql
DELETE FROM Camel;
```
```sql
CREATE TABLE Horse_Donkey AS 
SELECT * FROM Horse 
UNION 
SELECT * FROM Donkey;
```
# 11: Создание таблицы "Молодые животные"
```sql
CREATE TABLE young_animals AS
SELECT *, TIMESTAMPDIFF(MONTH, birth_date, CURDATE()) AS age_in_months
FROM Dog
WHERE TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) BETWEEN 1 AND 3;

```
Повторить для других животных и объедините данные.

# 12: Объединение всех таблиц
```sql
CREATE TABLE all_animals AS
SELECT 'Dog' AS animal_type, * FROM Dog
UNION ALL
SELECT 'Cat', * FROM Cat
UNION ALL
SELECT 'Hamster', * FROM Hamster
UNION ALL
SELECT 'Horse_Donkey', * FROM Horse_Donkey;
```
# 13: Инкапсуляция методов и наследование
```python
# Родительский класс Animal
# Parent class Animal
class Animal:
    def __init__(self, name, birth_date):
        self.__name = name  # Encapsulation of the name
        self.__birth_date = birth_date  # Encapsulation of the birth date

    # Method to get information about the animal
    def get_info(self):
        return f"Name: {self.__name}, Birth Date: {self.__birth_date}"

    # Method to get the animal's age
    def get_age(self, current_date):
        # Age in years
        return current_date.year - self.__birth_date.year - \
            ((current_date.month, current_date.day) < (self.__birth_date.month, self.__birth_date.day))

# Class DomesticAnimals, inheriting from Animal
class DomesticAnimals(Animal):
    def __init__(self, name, birth_date, commands):
        super().__init__(name, birth_date)  # Inherited attributes
        self.__commands = commands  # Encapsulation of the list of commands

    # Method to get the commands that the domestic animal performs
    def get_commands(self):
        return f"Commands: {', '.join(self.__commands)}"

# Class Dog, inheriting from DomesticAnimals
class Dog(DomesticAnimals):
    def __init__(self, name, birth_date, commands):
        super().__init__(name, birth_date, commands)

# Class Cat, inheriting from DomesticAnimals
class Cat(DomesticAnimals):
    def __init__(self, name, birth_date, commands):
        super().__init__(name, birth_date, commands)

# Class Hamster, inheriting from DomesticAnimals
class Hamster(DomesticAnimals):
    def __init__(self, name, birth_date, commands):
        super().__init__(name, birth_date, commands)

# Class PackAnimals, inheriting from Animal
class PackAnimals(Animal):
    def __init__(self, name, birth_date):
        super().__init__(name, birth_date)

# Class Horse, inheriting from PackAnimals
class Horse(PackAnimals):
    def __init__(self, name, birth_date):
        super().__init__(name, birth_date)

# Class Camel, inheriting from PackAnimals
class Camel(PackAnimals):
    def __init__(self, name, birth_date):
        super().__init__(name, birth_date)

# Class Donkey, inheriting from PackAnimals
class Donkey(PackAnimals):
    def __init__(self, name, birth_date):
        super().__init__(name, birth_date)

# Example of using the classes
from datetime import date

dog = Dog("Bobik", date(2021, 5, 1), ["Sit", "Lie down"])
cat = Cat("Murka", date(2020, 8, 15), ["Meow"])

print(dog.get_info())
print(dog.get_commands())
print(f"Dog age: {dog.get_age(date.today())} years")

print(cat.get_info())
print(cat.get_commands())
print(f"Cat age: {cat.get_age(date.today())} years")
```