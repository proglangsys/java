# 10. Обобщенное программирование

## Методические указания

### Обобщенные типы

_Обобщение_ — параметризированный тип. При объявлении класса, интерфейса, метода и конструктора можно указать один или несколько параметров типа, вместо которых при создании объекта будут подставляться реально существующие ссылочные типы.

Когда один алгоритм можно реализовать для различных типов данных, то предпочтительнее создать обобщенный класс, который получает тип данных в качестве параметра. Это позволит реализовать такой алгоритм в обобщенном виде для всех поддерживаемых типов. Обычно параметры типа записываются заглавными буквами, например, `T`, `V`, `K`.

В следующем примере приводится обобщенный класс `Box`  с параметром типа `T`, вместо которого при создании объекта класса `Box`  будет подставляться реально существующий ссылочный тип.
```java
public class Box<T> {
    private T thing;

    public T get() {
        return thing;
    }
    public void put(T thing) {
        this.thing = thing;
    }
}
```

Например, можно создать объект типа `Box<Integer>`, который будет хранить только целые числа типа `Integer`.
```java
Box<Integer> box = new Box<>(); // Здесь аргумент типа --- Integer 
box.put(1); // Вложить целое число
Integer x = box.get(); // Получить целое число
box.put(1.0); // Ошибка компиляции: невозможно добавить вещественное число
box.put("1"); // Ошибка компиляции: невозможно добавить строку
```

Можно создать объект типа `Box<String>`, который будет хранить только строки типа `String`.
```java
Box<String> box = new Box<>(); // Здесь аргумент типа --- String
box.put("my text"); // Вложить строку
String s = box.get(); // Получить строку
box.put(1.0); // Ошибка компиляции: невозможно добавить вещественное число
box.put(1); // Ошибка компиляции: невозможно добавить целое число
```

Параметров типа может быть несколько. В следующем примере приводится обобщенный класс `Pair`  с двумя параметром типа `K` и `V`.
```java
public class Pair<K,V> {
    K key;
    V value;
    Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
}
```

При создании объектов обобщенного класса передаются аргументы типов, в том количестве и порядке, в котором параметры типов используются при объявлении этого класса.
```java
Pair<Integer, String> pair1 = new Pair<>(1, "Ivanov");
Pair<String, String> pair2 = new Pair<>("+79081112233", "Petrov");
```

В обобщенном классе параметр типа может также использоваться для объявления массивов. В следующем примере реализуется обобщенный список на основе статистического массива.
```java
public class StaticArrayList<I> {
    private I items[];
    private int last;

    public StaticArrayList(int size) {
        items = (I[]) new Object[size];
    }

    public boolean add(I item) {
        if (last < items.length) {
            items[last] = item;
            ++last;
            return true;
        } else {
            return false;
        }
    }

    public I get(int index) {
        if (index >= 0 && index < items.length)
            return items[index];
        else
            return null;
    }

    public int size() {
        return items.length;
    }
}
```

При создании объекта данного списка указывается аргумент типа. Например, в следующем примере создается обобщенный список прямоугольников типа `Rectangle`.
```java
StaticArrayList<Rectangle> list = new StaticArrayList<>(3);
list.add(new Rectangle(0,0,10,10));
list.add(new Rectangle(10,10,20,10));
list.add(new Rectangle(20,20,10,30));

for (int i = 0; i < list.size(); i ++)
    System.out.println(list.get(i));
```

### Ограниченные типы

Параметр типа можно ограничить, указав суперкласс. В результате, параметр типа может заменяться на сам суперкласс или любой из его подклассов. Например, в следующем примере, параметр типа органичен суперклассом `Number`. Это означает, что при создании объектов данного обобщенного класса в качестве аргументов можно указывать только сам суперкласс `Number` и его подклассы `Byte`, `Double`, `Float`, `Integer`, `Long`, `Short` и другие.
```java
public class NumericBox<N extends Number> {
    private N number;

    NumericBox(N number) {
        this.number = number;
    }

    public N get() {
        return number;
    }

    // Квадратный корень
    public double sqrt() {
        return Math.sqrt(number.doubleValue());
    }

    // Возведение в степень
    public double pow(int n) {
        return Math.pow(number.doubleValue(), n);
    }
}

public class MyMainClass {
    public static void main(String[] args) {
        NumericBox<Integer> nb1 = new NumericBox<>(100);
        System.out.println(nb1.sqrt());
        System.out.println(nb1.pow(2));

        NumericBox<Float> nb2 = new NumericBox<>(4F);
        System.out.println(nb2.sqrt());
        System.out.println(nb2.pow(2));
    }
}
```

### Обобщенные методы

Можно объявлять обобщенные методы, при этом сам класс, в котором они объявляются не обязательно будет обобщенным.
```java
import java.util.*;

public class MyMainClass {
    public static void main(String[] args) {
        List<Number> numbers = Arrays.asList(1.5, 2, 3L, 4F);
        System.out.println(sum(numbers));
    }

    public static <T extends Number> double sum(Collection<T> numbers) {
        double sum = 0;

        for (Number n : numbers)
            sum += n.doubleValue();

        return sum;
    }
}
```

### Шаблоны аргументов

Для того чтобы метод мог поддерживать параметры различных обобщенных типов можно использовать метасимвол `<?>`.
```java
import java.util.*;

public class MyMainClass {
    public static void main(String[] args) {
        List<Number> numbers = Arrays.asList(10, 20, 30, 40, 50);
        printCollection(numbers);
    }

    public static void printCollection(Collection<?> c) {
        for (Object e : c)
            System.out.println(e);
    }
}
```

### Коллекции

_Коллекция_ — структура данных, предназначенная для хранения набора значений одного или различных типов, и обеспечивающая доступ к ним.

«Java Collections Framework» — набор связанных классов и интерфейсов, реализующих широко используемые структуры данных — коллекции: список, очередь, множество, отображение и др. Основные интерфейсы:

| Коллекция  | Описание                                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------|
| Collection | Позволяет работать с группами объектов. Находится на вершине иерархии   коллекций                             |
| Deque      | Двусторонняя очередь                                                                                          |
| List       | Список хранит последовательность однотипных объектов                                                          |
| Queue      | Односторонняя очередь управляет специальными типами списков, где   элементы удаляются только из начала списка |
| Set        | Множество содержит уникальные элементы                                                                        |
| Map        | Отображение сопоставляет уникальным ключам значения                                                           |

![Иерархия коллекций](https://upload.wikimedia.org/wikipedia/commons/a/ab/Java.util.Collection_hierarchy.svg)

Пример использования списка на основе динамического массива.
```java
import java.util.*;

public class MyMainClass {
    public static void main(String[] args) {
        // Создать список строк на основе динамического массива
        List<String> countryNames = new ArrayList<>();

        //
        countryNames.add("France");
        countryNames.add("Russia");
        countryNames.add("Angola");

        for (int i = 0; i < countryNames.size(); i ++) {
            String countryName = countryNames.get(i);
            System.out.printf("element %d = %s%n", i, countryName);
        }

        // Упорядочить список в естественном порядке 
        // (лексикографически для строк)
        Collections.sort(countryNames);

        // Получить итератор для перебора элементов списка
        Iterator<String> iterator = countryNames.iterator();
        while(iterator.hasNext()) {
            String countryName = iterator.next();
            System.out.println(countryName);
        }
    }
}
```

Пример использования списка на основе связанного списка.
```java
import java.util.*;

public class MyMainClass {
    public static void main(String[] args) {
        // Создать список строк на основе связанного списка
        List<Number> numbers = new LinkedList<>();

        // Наполнить список
        numbers.add(10);
        numbers.add(15.0);
        numbers.add(3L);

        // Перебрать список
        for (Number n: numbers)
            System.out.printf("%s is %s%n", n, n.getClass());
     }
}
```

### Стек

_Стек_ — абстрактный тип данных, список однотипных элементов, организованных по принципу «*Last  In, First  Out*» (LIFO) — «*последним пришёл, первым вышел*».

![Организация стека в виде одномерного упорядоченного по адресам массива. Показаны операции вталкивания и выталкивания данных из стека операциями push и pop.](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Lifo_stack.svg/2560px-Lifo_stack.svg.png)

## Задание

**Часть I**

- Разработать обобщенный стек на основе статического массива (методы `push`, `pop`, `size`).
- Продемонстрировать работу стека следующим образом: создать стек чисел любых типов, наполнить его числами разных типов.

**Часть II**

- Разработать обобщенный стек на основе динамического массива (методы `push`, `pop`, `peek`, `size`, `clear`, `empty`). Стек должен хранить только числа: использовать ограниченное обобщение от `Number`. 
- Дополнить класс (стек) статическим обобщенным методом вычисления среднего значения элементов стека. 
- Дополнить класс (стек) статическим обобщенным методом с ограниченным метасимволом (`<? extends Number>`) для печати элементов стека в командную строку.
- Продемонстрировать работу стека следующим образом: создать стек чисел любых типов, наполнить его числами разных типов.

**Часть III**

- Разработать обобщенный стек на основе связанного списка (методы `push`, `pop`, `peek`, `size`, `clear`, `empty`).
- Дополнить класс (стек) статическим методом создания связанного списка из элементов стека.
- Продемонстрировать работу стека следующим образом: создать стек чисел любых типов, наполнить его числами разных типов.

## Вопросы

1.	Обобщенные типы
2.	Ограниченные типы
3.	Шаблоны аргументов
4.	Обобщенные методы
5.	Обобщенные конструкторы
6.	Обобщенные интерфейсы
7.	Коллекции
8.	Список
9.	Очередь
10.	Стек
11.	Множество
12.	Отображение

## Ресурсы

1. Г. Шилдт. Java  Руководство для начинающих. Главы 9-10.
2. Г. Шилдт (2015) Java 8 Полное руководство (Девятое издание). Глава 18. Пакет java. util, часть 1. Collections Framework
