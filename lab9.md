# 9. Потоки ввода/вывода

## Методические указания

Ввод-вывод данных реализованы на основе потоков. _Поток_ — это абстрактная сущность, представляющая устройства ввода-вывода, которая выдает и получает информацию.

_Байтовые потоки_ обеспечивают чтение и запись двоичных данных. Реализованы подклассами классов InputStream  (байтовые потоки ввода) и OutputStream (байтовые потоки вывода).

_Символьные потоки_ предназначены для чтения и записи текстовых данных в кодировке Unicode. Реализованы подклассами классов Reader  (символьные потоки ввода) и Writer  (символьные потоки вывода).

### Проверка существования и доступности файла

Объекты класса [File](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)  представляют файлы и директории. Объекты типа [Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html) представляют пути к файлам и директориям. Класс [Files](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html) обеспечивает статические методы управления файлами и директориями. Класс [Paths](https://docs.oracle.com/javase/7/docs/api/java/nio/file/Paths.html) предоставляет статические методы конвертирования путей, заданных строками [String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) или ссылками на ресурсы [URI](https://docs.oracle.com/javase/8/docs/api/java/net/URI.html) в объекты типа [Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html).
```java
package ru.isu.math.files;

import java.io.File;
import java.nio.file.Files;
import java.nio.file.Path;

public class MyApp {
    public static void main(String[] args) {
        File file = new File("data/source.txt");
        Path path = file.toPath();

        // Проверить существует ли заданный файл
        boolean isExisting = Files.exists(path);

        if (isExisting) {
            System.out.println("Заданный файл существует");

            // Проверить доступен ли заданный файл для чтения
            boolean isReadable = Files.isReadable(path);

            if (isReadable)
                System.out.println("Заданный файл доступен для чтения");
            else
                System.out.println("Заданный файл не доступен для чтения");

        } else {
            System.out.println("Заданный файл не существует");
        }
    }
}
```

Другой способ проверить существование и доступность файла
```java
public static void main(String[] args) {
    File file = new File("data/source.txt");
    if (file.exists()) {
        System.out.println("Заданный файл существует");

        if (file.canRead())
            System.out.println("Заданный файл доступен для чтения");
        else
            System.out.println("Заданный файл не доступен для чтения");

    } else {
        System.out.println("Заданный файл не существует");
    }
}
```

### Обработка исключительных ситуаций

_Исключение_ — это ошибка, возникающая в процессе выполнения программы. Обрабатываемые исключения являются объектами подклассов класса [Exception](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html).
```java
try {
    // Здесь может произойти исключительная ситуация
} catch (Exception e) {
    // Здесь можно обработать возникшее исключение 
} finally {
    // Здесь размещаются инструкции, которые будут выполнены в конце в любом случае 
}
```

При вводе выводе могут возникать следующие исключительные ситуации:
- [IOException](https://docs.oracle.com/javase/8/docs/api/java/io/IOException.html) — ошибка ввода-вывода.
- [FileNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/io/FileNotFoundException.html)  — файл не найден.
- [ClassNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/lang/ClassNotFoundException.html)  — класс не найден.

### Закрытие ресурсов и `try` c ресурсами

Файловые потоки ввода-вывода следует закрывать с помощью метода close(). Вызов этого метода следует размещать в блоке finally, при этом потребуется обработчик исключительной ситуации [IOException](https://docs.oracle.com/javase/8/docs/api/java/io/IOException.html). Вместо использования метода close(), автозакрываемые потоки ввода-вывода можно создавать, как аргумент инструкции try  c ресурсами.

### Чтение файла

Чтение текста из файла с помощью символьного потока ввода с использованием `try` c ресурсами.
```java
static void read() {
    File file = new File("data/source.txt");
    Path path = file.toPath();
    
    if (Files.exists(path) && Files.isReadable(path)) {
        try (BufferedReader reader = Files.newBufferedReader(path)) {
            String line;
            while ((line = reader.readLine()) != null)
                System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Чтение текста из файла с помощью символьного потока ввода без использования `try`  c ресурсами.
```java
static void read() {
    File file = new File("data/source.txt");
    Path path = file.toPath();

    if (Files.exists(path) && Files.isReadable(path)) {
        BufferedReader reader = null;
        try {
            reader = Files.newBufferedReader(path);
            String line;
            while ((line = reader.readLine()) != null)
                System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (reader != null) 
                    reader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### Создание и запись файла

Запись текста в файл с помощью байтового потока вывода.
```java
static void write() {
    // Данные для записи в файл
    String s = "Hello World!";
    byte data[] = s.getBytes();

    File file = new File("data/target.txt");
    Path path = file.toPath();
    try (OutputStream out = new BufferedOutputStream(
            Files.newOutputStream(path, CREATE, WRITE))) {
        out.write(data, 0, data.length);
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

Запись текста в файл с помощью символьного потока вывода.
```java
static void write() {
    String path = "data/target.txt";
    String lines[] = {"Line 1", "Line 2", "Line 3"};

    try (FileWriter writer = new FileWriter(path)) {
        for (String line: lines)
            writer.write(line + System.lineSeparator());
    } catch (IOException e) {
        System.err.println(e);
    }
}
```

### Сериализация и десериализация объектов

_Сериализация_ — запись состояния объектов в последовательность байтов.
_Десериализация_ — чтение состояния объектов из последовательности байтов.

Как правило при сериализации объекты записываются в файл, а при десериализации считываются из файла. Для того чтобы объекты класса могли быть сериализованы, класс должен реализовывать маркерный интерфейс [Serializable](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html). Для сериализации используется объектный поток ввода — [ObjectOutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectOutputStream.html). Для десериализации используется объектный поток ввода вывода — [ObjectInputStream](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectInputStream.html).
```java
import java.io.Serializable;

public class Person implements Serializable {
    private String firstName;
    private String lastName;
    private int age;

    public Person(String firstName, String lastName, int age) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "firstName = '" + firstName + '\'' +
                ", lastName = '" + lastName + '\'' +
                ", birthDate = " + age +
                '}';
    }
}
```

Сериализация:
```java
static void serialize() {
    Person max = new Person("Max", "Planck", 21);
    Person isaac = new Person("Isaac", "Newton", 40);

    Person persons[] = {max, isaac};

    try (FileOutputStream fos = new FileOutputStream("data/objects")) {
        ObjectOutputStream out = new ObjectOutputStream(fos);
  
        for (Person person: persons)
            out.writeObject(person);

    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

Десериализация:
```java
static void deserialize() {
    String path = "data/objects";
    try (FileInputStream fis = new FileInputStream(path)) {
        ObjectInputStream in = new ObjectInputStream(fis);

        while (true) {
            try {
                Person person = (Person) in.readObject();
                System.out.println(person);
            } catch (EOFException e) {
                break;
            }
        }
    } catch (IOException | ClassNotFoundException e) {
        e.printStackTrace();
    }
}
```

## Задание

**Часть I**

Найти заданную подстроку в выбранном текстовом файле.

**Часть II**

Извлечь все слова из заданного текстового файла и записать их в виде упорядоченного лексикографически списка (каждое слово с новой строки) в другой текстовый файл.

**Часть III**

Разработать два или более взаимосвязанных классов. Создать несколько объектов этих классов. Выполнить сериализацию этих объектов в двоичный файл и их десериализацию из этого файла.

## Вопросы

1.	Байтовые потоки ввода-вывода
2.	Символьные потоки ввода-вывода
3.	Сериализация и десериализация
4.	Файлы, директории, пути
5.	Обработка исключительных ситуаций
6.	`try` с ресурсами

## Ресурсы

1. Г. Шилдт. Java  Руководство для начинающих. Главы 9-10.
