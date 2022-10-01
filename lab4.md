# 4. Обработка строк

## Методические указания

### Сравнение строк

Метод `compareTo` сравнивает две строки лексикографически

```java
String s1 = "aaa";
String s2 = "bbb";

// Сравнить две строки с учетом регистра
if (s1.compareTo(s2) > 0)
    System.out.println("s1 больше s2 (правее лексикографически)");
else if (s1.compareTo(s2) < 0)
    System.out.println("s1 меньше s2 (левее лексикографически)");
else
    System.out.println("s1 равна s2");
```

Метод `compareToIgnoreCase` сравнивает две строки лексикографически без учета регистра
```java
// Сравнить две строки без учета регистра
if (s1.compareToIgnoreCase(s2) > 0)
    System.out.println("s1 больше s2 (правее лексикографически)");
else if (s1.compareToIgnoreCase(s2) < 0)
    System.out.println("s1 меньше s2 (левее лексикографически)");
else
    System.out.println("s1 равна s2");
```

### Сортировка массива строк  лексикографически

```java
String s = "Hello planet earth, you are a great planet";

// Привести строку к нижнему регистру
s = s.toLowerCase();

// Разделить строку на токены
String tokens[] = s.split(" ");

// Упорядочить массив строк лексикографически
Arrays.sort(tokens);

// Напечатать массив строк
System.out.println(Arrays.toString(tokens));
```

### Регулярные выражения

_Регулярные выражения_ — это механизм для поиска и замены текста; шаблоны для сопоставления последовательностей символов в строках.

Регулярные выражения позволяют проверить соответствие строки шаблону.

```java
// Скомпилировать регулярное выражение
Pattern p = Pattern.compile("a*b");

// Сопоставить заданную строку с регулярным выражением
String s = "aaaab";
Matcher m = p.matcher(s);
boolean b = m.matches();
```

Альтернативно можно использовать метод matches класса Pattern.
```java
boolean b1 = Pattern.matches("a*b", "aaaab");
```
или метод matches объектов типа String
```java
boolean b2 = "aaaab".matches("a*b");
```

Регулярные выражения позволяют делать замены в тексте.
```java
// Удалить лишние пробелы
String s = "bla      bla      bla      bla      bla      bla";
s = s.replaceAll("\\s+", " ");
System.out.println(s);
```

Выполнить токенизацию с учетом дополнительных символов-разделителей.
```java
// Разделить строку на токены 
String s = "bla,      bla. bla; bla bla bla...";
String tokens[] = s.replaceAll("[.,;]", "").split("\\s+");
System.out.println(Arrays.toString(tokens));
```

Пример валидации телефонных номеров с помощью регулярных выражений.
```java
String phones[] = {
        "+7-902-111-22-33",
        "8 902 111 2233",
        "+7 (495) 123-22-33",
        "+1 000 000 00 00"
};

for (String phone: phones) {
    String replaced = phone.replaceAll("[-() ]", "");
    boolean validPhone = Pattern.matches("(\\+7|8)\\d{10}", replaced);
    
    if (validPhone)
        System.out.println(phone + " is a valid phone number");
    else
        System.out.println(phone + " is not a valid phone number");
}
```

## Задание

**Часть I**

- Сравнить две строки с помощью компаратора
- Упорядочить массив слов по алфавиту
- Найти палиндромы среди слов некоторой строки

**Часть II**

- Исключить из строки все символы, кроме чисел и пробелов, с помощью регулярных выражений
- Заменить в строке все знаки препинания на пробел с помощью регулярных выражений
- Реализовать валидацию адресов электронной почты по регулярному выражению
- Реализовать валидацию арифметических выражений по регулярному выражению

**Часть III**

- Вычислить расстояние Левенштейна между всеми парами слов в строке
- Определить степень схожести двух слов по звучанию (произношению) с помощью фонетического алгоритма (слова задаются пользователем)

## Вопросы

1.	Создание объектов типа String
2.	Сравнение строк
3.	Неизменяемость строк
4.	Регулярные выражения

## Ресурсы

1.	Г. Шилдт. Java Руководство для начинающих. Глава 5
2.	[Лексикографический порядок](https://ru.wikipedia.org/wiki/%D0%9B%D0%B5%D0%BA%D1%81%D0%B8%D0%BA%D0%BE%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D0%BA)
3.	[Регулярные выражения](https://ru.wikipedia.org/wiki/%D0%A0%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D1%8B%D0%B5_%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F)
4.	[Синтаксис регулярных выражений](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)
5.	[Онлайн редактор регулярных выражений](https://regexr.com/)
6.	[Расстояние Левенштейна](https://ru.wikipedia.org/wiki/%D0%A0%D0%B0%D1%81%D1%81%D1%82%D0%BE%D1%8F%D0%BD%D0%B8%D0%B5_%D0%9B%D0%B5%D0%B2%D0%B5%D0%BD%D1%88%D1%82%D0%B5%D0%B9%D0%BD%D0%B0)
7.	[LevenshteinDistance](https://commons.apache.org/proper/commons-text/apidocs/org/apache/commons/text/similarity/LevenshteinDistance.html) — класс для вычисления расстояния Левенштейна из [Apache Commons Text](https://commons.apache.org/proper/commons-text/)
8.	[Фонетический алгоритм](https://en.wikipedia.org/wiki/Phonetic_algorithm)
9.	[Soundex](https://commons.apache.org/proper/commons-codec/apidocs/org/apache/commons/codec/language/Soundex.html) — класс реализации фонетического алгоритма Soundex из [Apache Commons Codec](https://commons.apache.org/proper/commons-codec/)
