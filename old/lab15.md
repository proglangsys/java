# 15. XML/JSON маршалинг/демаршалинг

## Методические указания

*Маршалинг* — процесс кодирования объектов в обменный формат данных (XML, JSON, YAML и др.). Обычно для обмена данными (объектами) между различными приложениями, сервисами.

*Демаршалинг* — обратный процесс, т.е. декодирование данных, представленных в обменном формате (XML, JSON, YAML и др.) в объекты.

### XML маршалинг/демаршалинг

XML (eXtensible Markup Language) — расширяемый язык разметки.

#### Подключение зависимостей

Для того чтобы реализовать XML маршалинг/демаршалинг необходимо включить в POM-файл вашего проекта следующие зависимости.
```xml
<dependency>
	<groupId>jakarta.xml.bind</groupId>
	<artifactId>jakarta.xml.bind-api</artifactId>
	<version>4.0.0</version>
</dependency>

<dependency>
	<groupId>com.sun.xml.bind</groupId>
	<artifactId>jaxb-impl</artifactId>
	<version>4.0.0</version>
</dependency>
```

Пример POM-файла:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>JAXB</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>13</maven.compiler.source>
        <maven.compiler.target>13</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>jakarta.xml.bind</groupId>
            <artifactId>jakarta.xml.bind-api</artifactId>
            <version>4.0.0</version>
        </dependency>
        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-impl</artifactId>
            <version>4.0.0</version>
        </dependency>
    </dependencies>

</project>
```

#### Аннотирование предметных классов 

Для того чтобы объекты класса можно было записывать/считывать в/из XML, его необходимо сопроводить аннотацией Jakarta XML Binding.

Создадим класс Book, экземпляры которого представляют книги следующим образом:

```java
package proglangsys.domain;

import jakarta.xml.bind.annotation.*;
import java.util.Date;

@XmlRootElement(name = "book")
@XmlAccessorType(XmlAccessType.FIELD)
public class Book {
    @XmlAttribute
    int id;
    @XmlElement
    String title;
    @XmlElement
    Date date;
    @XmlElement
    Author author;

    public Book() {
    }

    public Book(int id, String title, Date date, Author author) {
        this.id = id;
        this.title = title;
        this.date = date;
        this.author = author;
    }
    
    @Override
    public String toString() {
        return "Book {" +
                "id=" + id +
                ", title='" + title + '\'' +
                ", date=" + date +
                ", author=" + author +
                '}';
    }
}
```

Создадим класс Author, экземпляры которого представляют авторов книг следующим образом:

```java
package proglangsys.domain;

import jakarta.xml.bind.annotation.*;

@XmlRootElement(name = "book")
@XmlAccessorType(XmlAccessType.FIELD)
public class Author {
    @XmlElement
    String name;

    @XmlElement
    String email;

    public Author() {
    }

    public Author(String name, String email) {
        this.name = name;
        this.email = email;
    }

    @Override
    public String toString() {
        return "Author{" +
                "name='" + name + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}
```

Для того чтобы выполнять XML маршалинг/демаршалинг списка книг, необходимо реализовать
служебный класс, представляющий набор книг следующим образом:

```java
package proglangsys.xml;

import jakarta.xml.bind.annotation.XmlAccessType;
import jakarta.xml.bind.annotation.XmlAccessorType;
import jakarta.xml.bind.annotation.XmlElement;
import jakarta.xml.bind.annotation.XmlRootElement;

import java.util.List;

@XmlRootElement(name = "books")
@XmlAccessorType(XmlAccessType.FIELD)
public class Books {
    @XmlElement(name = "book")
    private List<Book> list;

    public List<Book> getList() {
        return list;
    }

    public void setList(List<Book> list) {
        this.list = list;
    }
}
```

#### XML маршалинг
 
Метод, выполняющий XML маршалинг списка книг:

```java
public static void xmlMarshal(Books books) throws JAXBException {
    JAXBContext context = JAXBContext.newInstance(Books.class);

    Marshaller marshaller= context.createMarshaller();
    marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);

    File file = new File("results/books.xml");
    marshaller.marshal(books, file);
}
```

#### XML демаршалинг

Метод, выполняющий XML демаршалинг списка книг:

```java
public static void xmlUnmarshal() {
    try {
        JAXBContext context = JAXBContext.newInstance(Books.class);

        Unmarshaller unmarshaller = context.createUnmarshaller();
        Books books = (Books) unmarshaller.unmarshal(new File("results/books.xml"));

        List<Book> list = books.getList();
        list.forEach(System.out::println);

    } catch (JAXBException e) {
        e.printStackTrace();
    }
}
```

#### Демонстрация работоспособности

```java
public static void main(String[] args) throws JAXBException, IOException {
    Book book1 = new Book(
            1,
            "Cancer Immunotherapy",
            new Date("01/02/2018"),
            new Author("Leja Mullen", "mullen@mail.com")
    );

    Book book2 = new Book(
            2,
            "Cancer Radiotherapy",
            new Date("11/09/2020"),
            new Author("Sachin Potter", "potter@mail.com")
    );

    Books books= new Books();
    List<Book> list = new ArrayList<>();
    list.add(book1);
    list.add(book2);
    books.setList(list);

    xmlMarshal(books);
    xmlUnmarshal();
}
```

### JSON маршалинг/демаршалинг

JSON (JavaScript Object Notation) — текстовый формат обмена данными, основанный на JavaScript.

#### Подключение зависимостей

Для того чтобы реализовать XML маршалинг/демаршалинг необходимо включить в POM-файл вашего проекта следующюю зависимость.

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.9.1</version>
</dependency>
```

#### Предметные классы 

В случае JSON маршалинга/демаршалинга аннотировать предметные классы не нужно.

Создадим класс Book, экземпляры которого представляют книги следующим образом:

```java
package proglangsys.domain;

import java.util.Date;

public class Book {
    int id;
    String title;
    Date date;
    Author author;

    public Book() {
    }

    public Book(int id, String title, Date date, Author author) {
        this.id = id;
        this.title = title;
        this.date = date;
        this.author = author;
    }
    
    @Override
    public String toString() {
        return "Book {" +
                "id=" + id +
                ", title='" + title + '\'' +
                ", date=" + date +
                ", author=" + author +
                '}';
    }
}
```

Создадим класс Author, экземпляры которого представляют авторов книг следующим образом:

```java
package proglangsys.domain;

import jakarta.xml.bind.annotation.*;

public class Author {
    String name;
    String email;

    public Author() {
    }

    public Author(String name, String email) {
        this.name = name;
        this.email = email;
    }

    @Override
    public String toString() {
        return "Author{" +
                "name='" + name + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}
```

#### JSON маршалинг

Метод, выполняющий JSON маршалинг списка книг:

```java
public static void jsonMarshal(Book books[]) throws IOException {
    Gson gson = new Gson();
    Path path = Paths.get("results/books.json");
    String json = gson.toJson(books);
    Files.writeString(path, json);
}
```

#### JSON демаршалинг

Метод, выполняющий JSON демаршалинг списка книг:

```java
public static void jsonUnmarshal() throws IOException {
    Gson gson = new Gson();
    Path path = Paths.get("results/books.json");
    String json = Files.readString(path);
    Book[] books = gson.fromJson(json, Book[].class);

    for (Book book: books)
        System.out.println(book);
}
```

#### Демонстрация работоспособности

```java
public static void main(String[] args) throws JAXBException, IOException {
    Book book1 = new Book(
            1,
            "Cancer Immunotherapy",
            new Date("01/02/2018"),
            new Author("Leja Mullen", "mullen@mail.com")
    );

    Book book2 = new Book(
            2,
            "Cancer Radiotherapy",
            new Date("11/09/2020"),
            new Author("Sachin Potter", "potter@mail.com")
    );

    jsonMarshal(new Book[]{book1, book2});
    jsonUnmarshal();
}
```

## Задание


**Часть I**

 - Разработать один предметный класс.  
 - Создать один объект этого класса.
 - Выполнить XML маршалинг/демаршалинг этого объекта.

**Часть II**

- Разработать два предметных класса, связанных отношением ассоциации. 
- Разработать служебный класс для представления наборов объектов охватывающего класса. 
- Создать несколько объектов этого класса. 
- Выполнить XML маршалинг/демаршалинг списка этих объектов.

**Часть III**

- Разработать два предметных класса, связанных отношением ассоциации. 
- Создать несколько объектов этого класса. 
- Выполнить JSON маршалинг/демаршалинг списка этих объектов.

## Вопросы

1.	Предметные классы
2.	Маршалинг
3.	Демаршалинг
4.	XML
5.	JSON

## Ресурсы

1.	
