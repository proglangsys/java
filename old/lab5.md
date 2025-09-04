# 5. Классы и объекты

## Методические указания

### Классы

![Класс и объект](https://cdn-images.visual-paradigm.com/guide/uml/uml-class-diagram-tutorial/01-uml-base-class-and-object-explained.png)

Картинка с сайта [Visual-Paradigm](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial)

Класс состоит из объявления и тела. Класс объявляется с помощью ключевого слова `class`.
```java
// Создать класс для представления прямоугольников

// Объявление класса
public class Rectangle {
    // Тело класса
}

```

### Поля

_Поле_ — переменная, объявленная непосредственно в теле класса; представляет некоторую характеристику объектов этого класса.

Объявление поля включает тип данных и имя. Полю может быть присвоено начальное значение. В случае, когда поле не инициализируется явно, ему присваивается значение по умолчанию в зависимости от его типа данных.
```java
public class Rectangle {
    // Координаты базовой точки
    int x, y;
    // Ширина и высота
    int width, height;
    // Цвет
    Color color = Color.BLACK;
}
```

### Методы

_Метод_ — это функция или процедура, объявленная в теле класса и определяющая алгоритм работы с объектами этого класса.

Метод состоит из объявления и тела. Объявление метода включает возвращаемый тип данных, имя и список параметров. В случае, когда метод ничего не возвращает, возвращаемый тип данных указывается ключевым словом `void`.
```java
public class Rectangle {
    // Поля
    int x, y;
    int width, height;
    Color color = Color.BLACK;

    // Вычислить площадь
    int area() {
        return width * height;
    }

    // Нарисовать прямоугольник в графическом контексте
    void draw(Graphics g) {
        g.setColor(color);
        g.fillRect(x, y, width, height);
    }

    // Передвинуть
    void move(int x, int y) {
        // Здесь происходит скрытие полей локальными переменными
        this.x = x;
        this.y = y;
    }

    // Масштабировать ширину и высоту пропорционально
    void scale(double factor) {
        if (factor > 0.0) {
            width *= factor;
            height *= factor;
        }
    }
}
```

### Перегрузка методов

Перегрузка методов позволяет объявлять в одном классе несколько методов с одинаковыми именами, но разными списками параметров.
```java
// Масштабировать ширину и высоту пропорционально
void scale(double factor) {
    if (factor > 0.0) {
        width *= factor;
        height *= factor;
    }
}

// Масштабировать ширину и высоту раздельно
void scale(double wFactor, double hFactor) {
    if (wFactor > 0.0)
        width *= wFactor;
    if (hFactor > 0.0)
        height *= hFactor;
}
```

### Конструкторы

Конструкторы служат для создания объектов с заданным начальным состоянием. Имя конструктора должно совпадать с именем класса, в котором он объявлен.
```java
public class Rectangle {
    // Поля
    int x, y;
    int width, height;
    Color color;

    // Конструктор
    Rectangle(int x, int y, int width, int height, Color color) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
        this.color = color;
    }


    // Методы 
}
```

### Перегрузка конструкторов

В одном классе можно объявить несколько конструкторов с разными списками параметров.
```java
public class Rectangle {
    // Поля
    int x, y;
    int width, height;
    Color color;

    // Конструкторы
    Rectangle(int x, int y, int width, int height, Color color) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
        this.color = color;
    }

    Rectangle(int x, int y, int width, int height) {
        // Вызов перегруженного конструктора
        this(x, y, width, height, Color.BLACK);
    }

    Rectangle(int width, int height) {
        // Вызов перегруженного конструктора
        this(0, 0, width, height, Color.BLACK);
    }

    // Методы 
}
```

### Объекты

Объекты класса создаются с помощью ключевого слова new, после которого следует вызов одного из доступных конструкторов.
```java
public class MyMainClass {
    public static void main(String[] args) {
        Rectangle rect1 = new Rectangle(0,0, 100, 200);
        Rectangle rect2 = new Rectangle(100,200);
        Rectangle rect3 = new Rectangle(10,20, 100, 100, Color.RED);
    }
}
```

С объектами можно взаимодействовать через их доступные поля и методы.
```java
import javax.imageio.ImageIO;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class MyMainClass {
    public static void main(String[] args) {
        // Создать прямоугольник
        Rectangle rect = new Rectangle(0,0, 400, 500);
        // Задать цвет
        rect.color = Color.RED;
        // Переместить прямоугольник
        rect.move(200, 300);
        // Уменьшить прямоугольник
        rect.scale(0.5);

        // Создать изображение и нарисовать на нем прямоугольник
        BufferedImage image = new BufferedImage(1000, 1000, 
                BufferedImage.TYPE_INT_RGB);
        Graphics g = image.getGraphics();
        rect.draw(g);
        try {
            File file = new File("image.png");
            ImageIO.write(image, "png", file);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Задание

**Часть I**

- Разработать класс «Ellipse» для представления эллипсов. В классе должны быть определены поля, методы и конструкторы.

**Часть II**

- Дополнить класс «Ellipse» перегрузкой методов и конструкторов.
- Создать несколько объект класса «Ellipse».
- Вывести созданные эллипсы в файл изображения.

**Часть III**

- Разработать класс для представления некоторых сущностей (за исключением любых графических фигур). В классе должны быть определены поля, методы и конструкторы, перегрузка методов и конструкторов.
- Продемонстрировать создание и использование объектов разработанного класса.

## Вопросы

1.	Класс
2.	Объект
3.	Объявление и реализация класса
4.	Поля
5.	Методы
6.	Передача параметров в методы
7.	Инструкция перехода return
8.	Конструкторы
9.	Перегрузка методов
10.	Перегрузка конструкторов
11.	Ключевое слово this
12.	Создание объектов и ключевое слово new
13.	Ссылочный тип данных
14.	Объектная ссылка
15.	Принципы ООП: Абстракция

## Ресурсы

1.	Г. Шилдт. Java Руководство для начинающих. Глава 4
2.	Г. Буч и др. Объектно-ориентированный анализ и проектирование с примерами приложений
3.	Принципы ООП
