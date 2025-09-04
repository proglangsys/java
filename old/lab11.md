# 11. Лямбда выражения классов

## Методические указания

_Функциональный интерфейс_ — это интерфейс, определяющий единственный абстрактный метод.

_Лямбда-выражение_ — это анонимный метод, реализующий функциональный интерфейс.

_Лямбда-оператор_ `->` разделяет лямбда-выражение на две части: в левой части указываются параметры, а в правой — тело лямбда-выражения, реализующее абстрактный метод.

### Одиночное лямбда-выражение

Тело одиночного лямбда-выражения состоит из одного выражения.
```java
// Функциональный интерфейс
interface MetricConverter {
    double convert(double value);
}

public class MyMainClass {
    public static void main(String[] args) {
        // Лямбда выражения
        MetricConverter feet2meter = (val) -> val / 3.281;
        MetricConverter pound2kg = (val) -> val / 2.205;

        // Обращения к ссылкам на лямбда выражения
        double feet = 1000;
        double meter = feet2meter.convert(feet);
        System.out.printf("%s футов = %s метров%n", feet, meter);

        double pound = 10;
        double kg = pound2kg.convert(pound);
        System.out.printf("%s фунтов = %s килограмм %n", pound, kg);
    }
}
```

### Блочное лямбда-выражение

Правая часть лямбда-выражения может содержать несколько инструкций заключенных в блок кода.
```java
import java.util.Arrays;
import java.util.List;

// Функциональный интерфейс
interface NumericOperation {
     double apply(List<? extends Number> numbers);
}

public class MyMainClass {
    public static void main(String[] args) {
        // Лямбда выражения
        NumericOperation summation = (numbers) -> {
            double val = 0;
            for (Number n : numbers)
                val += n.doubleValue();
            return val;
        };

        // Лямбда выражения
        NumericOperation average = (numbers) -> {
            if (numbers.size() == 0)
                return 0;
            double val = summation.apply(numbers);
            return val / numbers.size();
        };

        List<Integer> primes = Arrays.asList(2, 3, 5, 7, 11, 13, 17, 19);

        System.out.println("Список: " + Arrays.toString(primes.toArray()));
        System.out.println("Сумма = " + summation.apply(primes));
        System.out.println("Среднее = " + average.apply(primes));
    }
}
```

### Создание  и  использование  компаратора

Компаратор можно создать на основе аннонимного класса.
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

class Student {
    String name;
    int age;
    float score;

    Student(String name, int age, float score) {
        this.name = name;
        this.age = age;
        this.score = score;
    }
}

public class MyMainClass {
    public static void main(String[] args) {
        // Создать список студентов
        List<Student> students = Arrays.asList(
                new Student("Иван", 21, 3.5f),
                new Student("Петя", 22, 4.1f),
                new Student("Мария", 20, 4.5f),
                new Student("Даша", 20, 3.0f)
        );

        // Создать компаратор студентов по среднему баллу на основе аннонимного класса
        Comparator<Student> scoreComparator = new Comparator<>() {
            @Override
            public int compare(Student s1, Student s2) {
                return Float.compare(s1.score, s2.score);
            }
        };

        // Упорядочить студентов с помощью компаратора
        students.sort(scoreComparator);

        // Напечатать студентов
        students.forEach(
                student -> System.out.printf("%s (%s)%n", student.name, student.score)
        );
    }
}
```

Альтернативно, компаратор можно создать с помощью лямбда-выражения.
```java
// Создать компаратор студентов по среднему баллу с помощью лямбда-выражения
Comparator<Student> scoreComparator = 
        (Student s1, Student s2) -> Float.compare(s1.score, s2.score);
```

### Фильтрация объектов коллекций

Лямбда-выражения можно использовать для фильтрации объектов из коллекций.
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

class Student {
    String name;
    int age;
    float score;

    Student(String name, int age, float score) {
        this.name = name;
        this.age = age;
        this.score = score;
    }
}

public class MyMainClass {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
                new Student("Иван", 21, 3.5f),
                new Student("Петя", 22, 4.1f),
                new Student("Мария", 20, 4.5f),
                new Student("Даша", 20, 3.0f)
        );

        // Выбрать студентов со средним баллом больше 4
        Stream<Student> filtered = students.stream().filter(p -> p.score > 4.0f);

        // Напечатать выбранных студентов
        filtered.forEach(
            student -> System.out.println(student.name)
        );
    }
}
```

## Задание

**Часть I**

- Разработать функциональный интерфейс для выполнения операций над коллекцией чисел. 
- Разработать лямбда выражения, реализующие данный функциональный интерфейс, для поиска минимального и максимального значения. 
- Применить эти лямбда выражения.

**Часть II**

- Разработать сущностный класс (например, Rectangle, Person, Location). 
- Создать два разных компаратора на основе лямбда-выражений для сортировки коллекции объектов данного класса по двум разным критериям.

**Часть III**

- Разработать сущностный класс (например, Rectangle, Person, Location). 
- Реализовать фильтрацию коллекции объектов данного класса по заданному критерию.

## Вопросы

1.	Функциональные интерфейсы
2.	Лямбда-выражения
3.	Обобщенные функциональные интерфейсы
4.	Компараторы
5.	Создание компараторов с помощью лямбда-выражений
6.	Фильтрация коллекций с помощью лямбда-выражений

## Ресурсы

1.	Г. Шилдт. Java Руководство для начинающих. Главы 9-10.
2.	Г. Шилдт (2015) Java 8 Полное руководство (Девятое издание). Глава 18. Пакет java. util, часть 1. Collections Framework
3.	https://mkyong.com/java8/java-8-lambda-comparator-example
4.	https://mkyong.com/tutorials/java-8-tutorials/java8/java-8-streams-filter-examples
