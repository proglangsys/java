# 8. UML диаграммы классов

> UML (Unified Modeling Language) — язык визуального моделирования в области разработки программного обеспечения.

## Инструментальные средства

### Подключаемый модуль «PlantUML Integration»

Для того чтобы установить подключаемый модуль PlantUML в IDE, необходимо открыть меню «File -> Settings», выбрать вкладку «Plugins» на панели слева, затем напечатать «PlantUML» в строке поиска, выбрать пункт «PlantUML Integration» и нажать кнопку «Install».

![Снимок экрана:](https://github.com/proglangsys/java/blob/main/images/lab8_1.png)

Если подключаемый модуль «PlantUML Integration» был успешно установлен, то IDE следует перезапустить, либо нажав кнопку «Restart» напротив пункта «PlantUML Integration», либо закрыв и повторно открыв IDE.

Для того чтобы создать новую диаграмму классов, щёлкните правой кнопкой мыши по панели проекта, в контекстном меню выберите пункт «New -> PlantUML File». В открывшемся окне «New PlantUML File» укажите имя новой диаграммы (например, «MyClassDiagram») и выберите пункт «Class», щелкнув по нему дважды.

Созданный файл (например, «MyClassDiagram.puml») содержит пример диаграммы классов. Слева настоящая диаграмма представлена в текстовом формате на предметно-ориентированном языке PlantUML. Справа отображается визуальное представление диаграммы. Текстовый файл можно редактировать, для того чтобы представить на ней необходимые классы, интерфейсы и отношения между ними.

![Снимок экрана:](https://github.com/proglangsys/java/blob/main/images/lab8_2.png)

![Снимок экрана:](https://github.com/proglangsys/java/blob/main/images/lab8_3.png)

### PlantUML онлайн

Официальный веб-сайт PlantUML — [http://www.plantuml.com](http://www.plantuml.com) предоставляет редактирование и визуализацию UML диаграмм онлайн. Можно использовать для создания диаграмм классов без установки подключаемого модуля «PlantUML Integration» в IDE.

## Диаграмма классов

_Диаграмма классов_ демонстрирует структуру классов и интерфейсов и отношений между ними.

### Декларирующий элемент
```java
@startuml
abstract class  "abstract class"
class           "class"
enum            "enum"
interface       "interface"
@enduml
```
![Декларирующий элемент](https://github.com/proglangsys/java/blob/main/images/lab8_4.png)

### Отношения между элементами
|    **Тип**          | **Оператор**       |
|:-------------------:|:-------------------:|
|     Наследование    |     <\|--           |
|     Реализация      |     <\|..           |
|     Ассоциация      |     <--             |
|     Композиция      |     *--             |
|     Агрегация       |     o--             |
|     Зависимость     |     <..             |

Наследование и реализация:

```java
@startuml
class Person
class Student
Person <|-- Student

abstract class Shape
class Rectangle
Shape <|-- Rectangle

interface Scalable
Scalable <|.. Rectangle
@enduml
```

![Наследование и реализация](https://github.com/proglangsys/java/blob/main/images/lab8_5.png)

Суперкласс Person наследуется подклассом Student. Класс Rectangle Person наследует абстрактный класс Shape и реализует интерфейс Scalable.

Иерархия наследования:

```java
@startuml
abstract class AbstractList
abstract AbstractCollection
interface List
interface Collection
class ArrayList

Collection <|.. AbstractCollection
List <|.. AbstractList

Collection <|-- List
AbstractCollection <|-- AbstractList
AbstractList <|-- ArrayList
@enduml
```

![Иерархия наследования](https://github.com/proglangsys/java/blob/main/images/lab8_6.png)

Ассоциация, агрегация, композиция, зависимость:

```java
@startuml
class Student
class Course
Course -- Student

class Postgraduate
class Supervisor
Supervisor <-- Postgraduate

class Rectangle
class Point
Point <.. Rectangle

class House
class Room
House *-- Room

class Car
class Engine
Car o-- Engine
@enduml
```

![Ассоциация, агрегация, композиция, зависимость](https://github.com/proglangsys/java/blob/main/images/lab8_7.png)

-	**Ассоциация** — класс A связан с классом B, если можно перемещаться от объектов класса A к объектам класса B; возникает, когда в классе A объявлены поля типа B или на основе B (массивы, коллекции объектов типа B). Например, студент может посещать несколько курсов и на курсе могут обучаться несколько студентов — двунаправленная ассоциация.  Другой пример: аспирант должен иметь руководителя (профессора), но (профессор) руководитель не обязательно имеет аспирантов — может быть реализовано как однонаправленная ассоциация. 
-	**Зависимость** — класс A зависит от класса B если изменение спецификации класса B может повлиять на работу класса A, но не наоборот; возникает, когда объект класса B является локальной переменной в классе A. Например, прямоугольник (Rectangle) зависит от точки (Point), например, если имеет метод, получающий точку в качестве параметра — move(Point p).
-	**Композиция** — отношение ассоциации между целым и его частями, когда часть не может существовать без целого. Например, комната является неотъемлемой частью дома; т.е. конкретная комната не может существовать без дома.
-	**Агрегация** — отношение ассоциации между целым и его частями, когда часть может существовать без целого. Например, двигатель является частью автомобиля, но может существовать и отдельно от него.

### Кардинальность отношения

```java
@startuml
class Student
class Course
Course "0..*" -- "0..*" Student

class Postgraduate
class Supervisor
Supervisor <-- "1" Postgraduate

class House
class Room
House *-- "1..*" Room

class Car
class Engine
Car o-- "1" Engine
@enduml
```

![Кардинальность отношения](https://github.com/proglangsys/java/blob/main/images/lab8_8.png)

-	**Ассоциация**: один студент может быть связан со многими курсами (0..*), один курс может быть связан со многими студентами (0..*).
-	**Ассоциация**: один аспирант связан со одним руководителем.
-	**Композиция**: один дом связан с одной или более комнатами (1..*).
-	**Агрегация**: один автомобиль связан с одним двигателем.

### Поля и методы

При описании полей и методов можно использовать нотацию Java (слева) или UML (справа).  Абстрактные методы задаются ключевым словом `abstract`, заключенным в пару фигурных скобок. Статические поля и методы обозначаются ключевым словом `static` внутри фигурных скобок.

![Поля и методы](https://github.com/proglangsys/java/blob/main/images/lab8_9.png)

```java
@startuml
abstract class Shape {
    int x
    int y
    {abstract} void move(int x, int y)
    {abstract} void draw(Graphics g)
}
class Rectangle {
    int width
    int height
    int area()
    void move(int x, int y)
    void draw(Graphics g)
    {static} Ellipse toEllipse(Rectangle rect)
}
Shape <|-- Rectangle

class Person {
    firstName: String
    lastName: String
    birthDate: Date
    email: EmailAddress
    notifyByEmail(message: String)
}
class Student {
    faculty: Faculty
    courses: Course[]
    book: RecordBook
    hasAcademicDebt(): boolean
    getCompletedCourses(): Course[]
}
Person <|-- Student
@enduml
```

### Указание видимости

|   **Уровень доступа**   | **Символ** |
|:------------------------------:|:-----------------:|
|     Закрытый                   |     -             |
|     Пакетный (по умолчанию)    |     ~             |
|     Защищенный                 |     #             |
|     Открытый                   |     +             |

![Указание видимости](https://github.com/proglangsys/java/blob/main/images/lab8_10.png)

```java
@startuml
abstract class Shape {
    - int x
    - int y
    + {abstract} void move(int x, int y)
    + {abstract} void draw(Graphics g)
}
class Rectangle {
    - int width
    - int height
    + int area()
    + void move(int x, int y)
    + void draw(Graphics g)
    ~ {static} Ellipse toEllipse(Rectangle rect)
}
Shape <|-- Rectangle

class Person {
    - firstName: String
    - lastName: String
    - birthDate: Date
    # email: EmailAddress
    # notifyByEmail(message: String)
}
class Student {
    - faculty: Faculty
    - courses: Course[]
    - book: RecordBook
    ~ hasAcademicDebt(): boolean
    ~ getCompletedCourses(): Course[]
}
Person <|-- Student
@enduml
```

## Задание

**Часть I**

- Создать диаграмму классов, описывающую следующие взаимосвязанные сущности: персона, студент, преподаватель, зачетная книжка, курс, факультет (только концептуальный уровень).

**Часть II**

- Дополнить диаграмму классов кардинальностью отношений, полями, методами, и уровнями доступа.

**Часть III**

- Создать диаграмму классов, описывающую взаимосвязанные сущности учебной базы данных [Chinook](https://github.com/lerocha/chinook-database/wiki/Chinook-Schema). 
- Дополнить диаграмму классов кардинальностью отношений, полями, методами, и уровнями доступа.

## Вопросы

1.	UML
2.	Диаграмма классов
3.	Наследование
4.	Реализация
5.	Ассоциация
6.	Композиция
7.	Агрегация
8.	Зависимость

## Ресурсы

1. [UML](https://ru.wikipedia.org/wiki/UML)
2. [UML Class Diagram Tutorial](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial)
3. [Руководство пользователя PlantUML](https://plantuml.com/ru/guide)
4. [Диаграмма классов](https://ru.wikipedia.org/wiki/%D0%94%D0%B8%D0%B0%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0_%D0%BA%D0%BB%D0%B0%D1%81%D1%81%D0%BE%D0%B2)
5. [Схема базы данных Chinook](https://schemaspy.org/sample/relationships.html)
