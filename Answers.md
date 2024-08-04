# Контрольная работа GB

## Задание 1

Используя команду cat в терминале операционной системы Linux, создать два файла Домашние животные (заполнив файл собаками, кошками, хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и ослы, а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя (Друзья человека).

```bash
# Создание и заполнение файлов
echo -e "Собаки\nКошки\nХомяки" > Домашние_животные.txt
echo -e "Лошади\nВерблюды\nОслы" > Вьючные_животные.txt

# Объединение файлов и просмотр содержимого
cat Домашние_животные.txt Вьючные_животные.txt > Все_животные.txt
cat Все_животные.txt

# Переименование файла
mv Все_животные.txt Друзья_человека.txt
```

## Задание 2

Создать директорию, переместить файл туда.

```bash
# Создание директории
mkdir Звери

# Перемещение файла в директорию
mv Друзья_человека.txt Звери/
```

## Задание 3

Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.

```bash
# Подключение репозитория
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.17-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb
sudo apt-get update

# Установка пакета из репозитория
sudo apt-get install mysql-server
```

## Задание 4 

Установить и удалить deb-пакет с помощью dpkg.

```bash
# Установка deb-пакета
sudo dpkg -i пакет.deb

# Устранение зависимости и настройка пакета
sudo apt-get install -f

# Удаление deb-пакета
sudo dpkg -r имя_пакета
```

## Задание 5

Выложить историю команд в терминале ubuntu

```bash
history > history.txt
```

## Задание 6

Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: (Лошади, верблюды и ослы).

```
            Животные
               |
    --------------------------------
    |                              |
Домашние животные          Вьючные животные
   |          |         |          |         |
Собаки     Кошки     Лошади     Верблюды   Ослы
```

## Задание 7

В подключенном MySQL репозитории создать базу данных “Друзья человека”

```sql
CREATE DATABASE Друзья_человека;
```

## Задание 8

Создать таблицы с иерархией из диаграммы в БД

```sql
-- Таблицы для категорий животных
CREATE TABLE Животные (
    id INT AUTO_INCREMENT PRIMARY KEY,
    тип VARCHAR(50)
);

CREATE TABLE Домашние_животные (
    id INT AUTO_INCREMENT PRIMARY KEY,
    животное_id INT,
    FOREIGN KEY (животное_id) REFERENCES Животные(id)
);

CREATE TABLE Вьючные_животные (
    id INT AUTO_INCREMENT PRIMARY KEY,
    животное_id INT,
    FOREIGN KEY (животное_id) REFERENCES Животные(id)
);

-- Таблицы для видов животных
CREATE TABLE Собаки (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    домашнее_животное_id INT,
    FOREIGN KEY (домашнее_животное_id) REFERENCES Домашние_животные(id)
);

CREATE TABLE Кошки (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    домашнее_животное_id INT,
    FOREIGN KEY (домашнее_животное_id) REFERENCES Домашние_животные(id)
);

CREATE TABLE Хомяки (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    домашнее_животное_id INT,
    FOREIGN KEY (домашнее_животное_id) REFERENCES Домашние_животные(id)
);

CREATE TABLE Лошади (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    вьючное_животное_id INT,
    FOREIGN KEY (вьючное_животное_id) REFERENCES Вьючные_животные(id)
);

CREATE TABLE Верблюды (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    вьючное_животное_id INT,
    FOREIGN KEY (вьючное_животное_id) REFERENCES Вьючные_животные(id)
);

CREATE TABLE Ослы (
    id INT AUTO_INCREMENT PRIMARY KEY,
    имя VARCHAR(50),
    команды VARCHAR(255),
    дата_рождения DATE,
    вьючное_животное_id INT,
    FOREIGN KEY (вьючное_животное_id) REFERENCES Вьючные_животные(id)
);
```

## Задание 9

Заполнить низкоуровневые таблицы именами (животных), командами которые они выполняют и датами рождения

```sql
INSERT INTO Собаки (имя, команды, дата_рождения, домашнее_животное_id) VALUES ('Бобик', 'Сидеть, Лежать', '2020-01-01', 1);
INSERT INTO Кошки (имя, команды, дата_рождения, домашнее_животное_id) VALUES ('Мурзик', 'Мяукать', '2024-06-15', 1);
INSERT INTO Хомяки (имя, команды, дата_рождения, домашнее_животное_id) VALUES ('Хома', 'Бегать в колесе', '2023-03-10', 1);

INSERT INTO Лошади (имя, команды, дата_рождения, вьючное_животное_id) VALUES ('Буцефал', 'Бежать', '2020-05-21', 1);
INSERT INTO Верблюды (имя, команды, дата_рождения, вьючное_животное_id) VALUES ('Кэмел', 'Идти', '2023-11-11', 1);
INSERT INTO Ослы (имя, команды, дата_рождения, вьючное_животное_id) VALUES ('Иа', 'Таскать грузы', '2022-09-09', 1);
```

## Задание 10

Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу

```sql
-- Удаление верблюдов
DELETE FROM Верблюды;

-- Объединение таблиц Лошади и Ослы
CREATE TABLE Лошади_и_Ослы AS
SELECT * FROM Лошади
UNION ALL
SELECT * FROM Ослы;
```

## Задание 11

Создать новую таблицу “молодые животные” в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице

```sql
CREATE TABLE Молодые_животные AS
SELECT *, TIMESTAMPDIFF(MONTH, дата_рождения, CURDATE()) AS возраст_в_месяцах
FROM (
    SELECT имя, команды, дата_рождения FROM Собаки WHERE дата_рождения BETWEEN DATE_SUB(CURDATE(), INTERVAL 3 YEAR) AND DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
    UNION ALL
    SELECT имя, команды, дата_рождения FROM Кошки WHERE дата_рождения BETWEEN DATE_SUB(CURDATE(), INTERVAL 3 YEAR) AND DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
    UNION ALL
    SELECT имя, команды, дата_рождения FROM Хомяки WHERE дата_рождения BETWEEN DATE_SUB(CURDATE(), INTERVAL 3 YEAR) AND DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
    UNION ALL
    SELECT имя, команды, дата_рождения FROM Лошади WHERE дата_рождения BETWEEN DATE_SUB(CURDATE(), INTERVAL 3 YEAR) AND DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
    UNION ALL
    SELECT имя, команды, дата_рождения FROM Ослы WHERE дата_рождения BETWEEN DATE_SUB(CURDATE(), INTERVAL 3 YEAR) AND DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
) AS молодые;
```

## Задание 12

Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.

```sql
CREATE TABLE Все_животные AS
SELECT * FROM Собаки
UNION ALL
SELECT * FROM Кошки
UNION ALL
SELECT * FROM Хомяки
UNION ALL
SELECT * FROM Лошади
UNION ALL
SELECT * FROM Ослы;
```

## Задание 13

Создать класс с Инкапсуляцией методов и наследованием по диаграмме.

```java
public abstract class Animal {
    private String name;
    private int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public abstract void makeSound();
}

public class Dog extends Animal {
    public Dog(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

public class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}
```

## Задание 14

Написать программу, имитирующую работу реестра домашних животных.

В программе должен быть реализован следующий функционал:

- 14.1 Завести новое животное
- 14.2 определять животное в правильный класс
- 14.3 увидеть список команд, которое выполняет животное
- 14.4 обучить животное новым командам
- 14.5 Реализовать навигацию по меню

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class PetRegister {

    private List<Animal> animals = new ArrayList<>();
    private Counter counter = new Counter();

    public void addAnimal(Animal animal) {
        animals.add(animal);
        counter.increment();
    }



    public void listCommands(Animal animal) {
        if (animal instanceof Dog) {
            System.out.println("Commands: sit, stay, fetch");
        } else if (animal instanceof Cat) {
            System.out.println("Commands: sit, jump");
        } else {
            System.out.println("No commands available");
        }
    }

    public void trainAnimal(Animal animal, String command) {
        System.out.println(animal.getName() + " is trained to " + command);
    }

    public void showMenu() {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("1. Add new animal");
            System.out.println("2. List commands");
            System.out.println("3. Train animal");
            System.out.println("4. Exit");
            int choice = scanner.nextInt();
            scanner.nextLine();
            switch (choice) {
                case 1:
                    System.out.print("Enter animal type (dog/cat): ");
                    String type = scanner.nextLine();
                    System.out.print("Enter name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter age: ");
                    int age = scanner.nextInt();
                    if (type.equalsIgnoreCase("dog")) {
                        addAnimal(new Dog(name, age));
                    } else if (type.equalsIgnoreCase("cat")) {
                        addAnimal(new Cat(name, age));
                    } else {
                        System.out.println("Unknown animal type");
                    }
                    break;
                case 2:
                    System.out.print("Enter animal name: ");
                    name = scanner.nextLine();
                    Animal animal = findAnimalByName(name);
                    if (animal != null) {
                        listCommands(animal);
                    } else {
                        System.out.println("Animal not found");
                    }
                    break;
                case 3:
                    System.out.print("Enter animal name: ");
                    name = scanner.nextLine();
                    animal = findAnimalByName(name);
                    if (animal != null) {
                        System.out.print("Enter new command: ");
                        String command = scanner.nextLine();
                        trainAnimal(animal, command);
                    } else {
                        System.out.println("Animal not found");
                    }
                    break;
                case 4:
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice");
            }
        }
    }

    private Animal findAnimalByName(String name) {
        for (Animal animal : animals) {
            if (animal.getName().equalsIgnoreCase(name)) {
                return animal;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        PetRegister register = new PetRegister();
        register.showMenu();
    }
}
```

## Задание 15

Создайте класс Счетчик, у которого есть метод add(), увеличивающий значение внутренней int переменной̆на 1 при нажатие “Завести новое животное” Сделайте так, чтобы с объектом такого типа можно было работать в блоке try-with-resources. Нужно бросить исключение, если работа с объектом типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение считать в ресурсе try, если при заведения животного заполнены все поля.

```java
import java.io.Closeable;
import java.io.IOException;

public class Counter implements Closeable {
    private int count = 0;
    private boolean isClosed = false;

    public void increment() {
        if (isClosed) {
            throw new IllegalStateException("Resource is already closed");
        }
        count++;
    }

    @Override
    public void close() throws IOException {
        if (!isClosed) {
            isClosed = true;
            System.out.println("Resource is closed. Total count: " + count);
        } else {
            throw new IOException("Resource already closed");
        }
    }
}
```

В классе `PetRegister` изменим метод `addAnimal` для использования `try-with-resources`:

```java
import java.io.IOException;

public void addAnimal(Animal animal) {
    try (Counter counter = new Counter()) {
        animals.add(animal);
        counter.increment();
    } catch (IOException e) {
        System.err.println("Failed to close the counter: " + e.getMessage());
    }
}
```