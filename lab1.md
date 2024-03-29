# 1. Инструментальные средства разработки

## Методические указания

### Платформа разработки JDK

[Java Development Kit](https://ru.wikipedia.org/wiki/Java_Development_Kit) (JDK) — комплект инструментальных средств для разработки приложений на языке [Java](https://ru.wikipedia.org/wiki/Java). Включает компилятор [javac](https://ru.wikipedia.org/wiki/Javac), утилиты, библиотеки классов Java API, документацию и примеры, среду исполнения приложений — [Java Runtime Environment](https://ru.wikipedia.org/wiki/Java_Runtime_Environment) (JRE).

JRE включает виртуальную машину [Java Virtual Machine](https://ru.wikipedia.org/wiki/Java_Virtual_Machine) (VM) и откомпилированные библиотеки классов Java API. Позволяет запускать Java приложения на любых устройствах или операционных системах.

Существует три редакции JDK:

- SE (Standard Edition) — стандартная редакция JDK, которая используется для разработки консольных и настольных приложений.
- EE (Enterprise Edition) — редакция для разработки распределенных приложений масштаба предприятий.
- ME (Micro Edition) — редакция для разработки приложений мобильных устройств и встраиваемых систем.

### Интегрированная среда разработки

Integrated Development Environment (IDE) — комплекс программных средств, используемый программистами для разработки программного обеспечения (ПО), в том числе, текстовый редактор, средства автоматизации сборки, отладчик.

Существует несколько популярных IDE для разработки Java приложений:
- [IntelliJ IDEA](https://www.jetbrains.com/idea/)
- [Eclipse](https://eclipseide.org/release/)
- [NetBeans](https://netbeans.apache.org/)

Для выполнение заданий необходимо установить следующие инструментальные средства:

- [Oracle JDK SE](https://www.oracle.com/java/technologies/downloads/) или [OpenJDK](https://openjdk.org/install/) (версию 8 или выше).
- [IntelliJ IDEA Community Edition](https://www.jetbrains.com/ru-ru/idea/download/#section=windows)

### Main-класс

Main-класс — класс, в котором есть main-метод. Main-метод запускает поток исполнения приложения, вызывается вирутальной машиной Java VM:
```java
public class MyMainClass {
    // main-метод
    public static void main(String[] args) {
        // инструкции
    }
}
```

Вывод текста в командную строку осуществляется через встроенный поток вывода:
```java
public class MyMainClass {
    // main-метод  
    public static void main(String[] args) {  
        // Вывести сообщение "my text" в командную строку
        System.out.println("my text");  
    }  
}
```

### Создание, сборка и запуск проекта

#### Создать новый проект

Запустить «IntelliJ IDEA». Если открыт приветственный экран «Welcome to IntelliJ IDEA», нажать кнопку «New Project». Если открыто основное окно, выбрать пункт меню «File | New | Project».

![Снимок экрана: создание нового проекта](https://github.com/proglangsys/java/blob/main/images/lab1_1.png)

Выбрать пункт «New Project» из списка слева. Задать имя нового проекта «Name» и изменить его месторасположение «Location», если необходимо. В списке «Languages» должен быть выбран язык «Java». В списке «JDK» должна быть выбрана JDK версии 8 или выше.

#### Создать пакет и класс

В окне «Project» щелкнуть правой кнопкой мыши папку «src», выбрать пункт «New | Java Class» (Alt+Insert).

![Снимок экрана: создание нового класса](https://github.com/proglangsys/java/blob/main/images/lab1_2.png)

Задать полное имя класса следующим образом: «ru.isu.math.example.MyMainClass» и нажать кнопку «OK». В результате будет создан пакет «ru.isu.math.example» и класс «MyMainClass» внутри этого пакета.

```java
package ru.isu.math.example;  

public class MyMainClass {  
}
```

#### Написать код

Добавить в созданный класс main-метод с необходимыми инструкциями.
```java
package ru.isu.math.example;  

public class MyMainClass {  
    public static void main(String[] args) {  
        System.out.println("Hello World!");  
    }  
}
```

#### Собрать и запустить приложение

Выбрать пункт меню «Run | Run…» или нажать кнопку «Run» на панели инструментов сверху — «зеленый треугольник» (Alt+Shift+F10). В раскрывшемся списке выбрать «MyMainClass».

Запустится компиляция исходного кода программы в байт-код и затем исполнение приложения в Java VM. Результат выполнения программы, сообщение «Hello World!», будет выводиться во встроенной командной строке.

![Снимок экрана: проект (слева) и редактируемый класс (справа)](https://github.com/proglangsys/java/blob/main/images/lab1_3.png)

### Компиляция и запуск из командной строки

Для того чтобы откомпилировать класс из командной строки, необходимо перейти в директорию, в которой находится файл с исходным кодом:
```bash
cd <path to the scr directory>
```
запустить компилятор javac, указав в качестве параметра название файла с исходным кодом с расширением:
```bash
javac -d target ru/isu/math/example/MyMainClass.java
```

В результате компилятор создаст файл с байт-кодом с тем же именем класса, но расширением «class» — «MyMainClass.class» в папке «target/ru/isu/math/example».

Для того чтобы исполнить откомпилированный класс необходимо перейти в директорию, в которой находится файл с байт-кодом:
```bash
cd <path to the target directory>
```
и запустить Java VM, указав в качестве параметра название файла с байт-кодом без расширения:
```bash
java ru.isu.math.example.MyMainClass
```

> Когда переменная среды JAVA_HOME не настроена, следует указывать полный путь к компилятору javac и виртуальной машине java соответственно:
```bash
<path to JDK>/bin/javac -d target ru/isu/math/example/MyMainClass.java
<path to JDK>/bin/java ru.isu.math.example.MyMainClass
```

### Дизассемблирование байт-кода

Для того чтобы дизассемблировать откомпилированный класс необходимо перейти в директорию, в которой находится файл с байт-кодом:
```bash
cd <path to the target directory>
```
запустить дизассемблер javap, указав в качестве параметра название файла с байт-кодом:
```bash
javap -c ru/isu/math/example/MyMainClass.class
```

> Когда переменная среды JAVA_HOME не настроена, следует указывать полный путь к дизассемблеру javap:
```bash
<path to JDK>/bin/javap -c ru/isu/math/example/MyMainClass.class
```

Результат дизассемблирования байт-кода выводится в командную строку.

![Снимок экрана: результат дизассемблирования байт-кода](https://github.com/proglangsys/java/blob/main/images/lab1_4.png)

### Инструкции и блоки кода

_Инструкция кода_ — команда для выполнения в Java VM. Инструкция заканчивается точкой с запятой `;`.
```java
// Объявить и инициализировать переменную целочисленного типа
int x = 1;
```

_Блок кода_ — набор инструкций, заключенный в пару симметричных фигурных скобок.
```java
{  
    int x = 1;
    x = x + 2;  
}
```

### Локальные переменные

_Локальная переменная_ — это переменная, объявленная внутри блока кода. Область видимости такой переменной ограничена блоком кода, в котором она объявлена.
```java
public static void main(String[] args) {  
    int x; // Объявить локальную переменную
    x = 1; // Присвоить значение локальной переменной
    System.out.println("x = " + x); // Вывести значение переменной
}
```

При объявлении переменной необходимо указать ее тип данных. Например, если переменная имеет тип `int`, то в качестве своих значений она может принимать только целые числа:
```java
int x = 2;
```
Переменная, объявленная с типом `double`, содержит только вещественные числа:
```java
double y = 2.5;
```
Переменная с типом String, будет ссылаться на строки
```java
String s = "my text";
```

### Цикл for

_Цикл_  — управляющая инструкция, которая определяет выполнение сопряженного блока кода (тела цикла) множество раз.

Цикл for имеет следующий синтаксис:
```java
for (инициализация счетчика; условие завершения; итерация) блок кода
```

Например, следующий цикл выполняет инструкции тела десять раз:
```java
for (int i = 0; i < 10; i++) {  
    System.out.println("i = " + i);  
}
```

### Аргументы командной строки

Аргументы командной строки передаются приложению в виде единственного параметра main-метода — массива строк:
```java
public class MyMainClass {  
    public static void main(String[] args) {
        // Вывести аргументы командной строки
        for (int i = 0; i < args.length; i++) {
            String arg = args[i];
            System.out.printf("Argument %d: %s%n", i, arg);
        }
    }
}
```

При запуске приложения из командной строки аргументы указываются после имени main-класса:
```bash
java ru.isu.math.example.MyMainClass p0 p1 p2
```

Для того чтобы задать аргументы командной строки в IDE, необходимо создать новую конфигурацию запуска следующим образом: выбрать пункт меню «Run | Edit Configurations…», добавить новую конфигурацию, выбрав в списке слева пункт «Application», задать имя при необходимости, указать main-класс, ввести значения аргументов в поле «Program Arguments», нажать кнопку «OK».

![Снимок экрана: создание конфигурации запуска приложения](https://github.com/proglangsys/java/blob/main/images/lab1_5.png)

Затем запустить программу с помощью созданной конфигурации, выбрав ее по имени в выпадающем списке слева от кнопки запуска «Run».

![Снимок экрана: результат запуска приложения](https://github.com/proglangsys/java/blob/main/images/lab1_6.png)


### Евклидово расстояние между заданными точками

Для двух точек двухмерного пространства

![p_1=\left(x_1,y_1\right)](https://bit.ly/3ReTrYQ) и ![p_2=\left(x_2,y_2\right)](https://bit.ly/3eg69b8)

евклидово расстояние вычисляется следующим:

![d\left( p1,p2 \right)=\sqrt[]{\left( x_1 - x_2 \right)^{2}+\left( y_1 - y_2 \right)^{2}}](https://bit.ly/3KKdr3i)

Для реализации этой формулы в Java можно использовать класс [Math](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html) (является частью Java API) который обеспечивает основные метаматематические операции над числами, например:
```java
double x = 4;  
Math.pow(x, 2); // Возведение x в степень 2
Math.sqrt(x); // Квадратный корень из x
```

Вышеприведенная формула может быть реализована следующим образом:
```java
double d = Math.sqrt(Math.pow(x1-x2, 2) + Math.pow(y1-y2, 2));
```

Другой способ реализации вычисления евклидова расстояния в Java состоит в том, чтобы воспользоваться готовым методом, поставляемом в составе сторонней библиотеки, например [Apache Commons Math](https://commons.apache.org/proper/commons-math).

### Создание и сборка проекта Maven

#### Создать новый проект

Если открыт приветственный экран «Welcome to IntelliJ IDEA», нажать кнопку «New Project». Если открыто основное окно, выбрать пункт меню «File | New | Project».

В качестве системы сборки «Build system» выбрать «Maven». Изменить имя проекта «Name» и месторасположение его файлов «Location» при необходимости, а также «GroupId» и «ArtifactId» в скрытой панели «Advanced Settings».

![Снимок экрана: создание Maven проекта](https://github.com/proglangsys/java/blob/main/images/lab1_7.png)

#### Добавить класс и собрать проект

Добавить пакет и класс с исходным кодом в папку «src/main/java». Раскрыть панель «Maven» справа, затем дважды щелкнуть пункт «install» в списке «Lifecycle». Запустится процесс сборки проекта. На панели «Run» внизу можно увидеть сообщение об успешном выполнении сборки «[INFO] BUILD SUCCESS». На панели «Project» (слева) можно увидеть результаты сборки — JAR файлы, раскрыв папку target.

![Снимок экрана: сборка Maven проекта](https://github.com/proglangsys/java/blob/main/images/lab1_8.png)

#### Добавить зависимость и импортировать класс

Открыть файл pom.xml, выбрав его на панели структуры проекта «Project». Добавить пару тегов `<dependencies></dependencies>` в конце перед закрывающимся тегом следующим образом:
```xml
<?xml version ="1.0" encoding="UTF-8"?>  
<project ...>  
...  
<dependencies>  
</dependencies>  
</project>
```

Добавить координаты зависимости от библиотеки [Apache Commons Math](https://commons.apache.org/proper/commons-math) в раздел dependencies следующим образом:
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<project ...>  
...
<dependencies>  
<dependency>  
<groupId>org.apache.commons</groupId>  
<artifactId>commons-math3</artifactId>  
<version>3.6.1</version>  
</dependency>  
</dependencies>  
</project>
```

> Актуальные координаты зависимости можно найти на веб-сайте [mvnrepository.com](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1).

После добавления зависимости, пакеты и классы библиотеки [Apache Commons Math](https://commons.apache.org/proper/commons-math) становятся доступными для импорта в разрабатываемые классы. Например, для того чтобы использовать готовую реализацию вычисления Евклидового пространства следует импортировать класс из данной библиотеки org.apache.commons.math3.ml.distance.EuclideanDistance как показано ниже:
```java
package ru.isu.math.example;

import org.apache.commons.math3.ml.distance.EuclideanDistance;

public class MyMainClass {
    public static void main(String[] args) {
        EuclideanDistance ed = new EuclideanDistance();
        double d = ed.compute(new double[]{10,20},new double[]{30.,40.});
        System.out.println("Euclidean distance: " + d);
    }
}
```

#### Собрать запускаемый  JAR файл

Для того чтобы собрать запускаемый, в файл pom.xml необходимо добавить следующий код:
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-assembly-plugin</artifactId>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>single</goal>
          </goals>
          <configuration>
            <archive>
              <manifest>
                <addClasspath>true</addClasspath>
                <mainClass>ru.isu.math.example.MyMainClass</mainClass>
              </manifest>
            </archive>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

Обновить Maven проект, нажав кнопку «Reload All Maven Projects», удалить предыдущую сборку — «clean» в списке «Lifecycle» и запустить новую сборку — «install» в списке «Lifecycle».

> В случае ошибки сборки «Source option 5 is no longer supported. Use 6 or later» добавьте в pom.xml версию Java в секции "properties", например, для Java 8, это будет выглядеть следующим образом:
```xml
<properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

### Создание и сборка проекта Gradle

#### Создать новый проект

Если открыт приветственный экран «Welcome to IntelliJ IDEA», нажать кнопку «New Project». Если открыто основное окно, выбрать пункт меню «File | New | Project».

В качестве системы сборки «Build system» выбрать «Gradle». Изменить имя проекта «Name» и месторасположение его файлов «Location» при необходимости, а также «GroupId» и «ArtifactId» в скрытой панели «Advanced Settings».

#### Добавить класс и собрать проект

Добавить пакет и класс с исходным кодом в папку src/main/java. Раскрыть панель «Gradle» справа, затем дважды щелкнуть пункт «build» в списке «Tasks | build». Запустится процесс сборки проекта. На панели «Run» внизу можно увидеть сообщение об успешном выполнении сборки «BUILD SUCCESSFUL». На панели «Project» (слева) можно увидеть результаты сборки — JAR файлы, раскрыв папку build/libs.

![Снимок экрана: сборка Gradle проекта](https://github.com/proglangsys/java/blob/main/images/lab1_9.png)

#### Добавить зависимость и импортировать класс

Открыть файл build.gradle, выбрав его на панели структуры проекта «Project». Добавить строку с координатами зависимости от библиотеки [Apache Commons Math](https://commons.apache.org/proper/commons-math):
```
implementation group: 'org.apache.commons', name: 'commons-math3', version: '3.6.1'
```
в раздел «dependencies» следующим образом:
```
plugins {
  id 'java'
}
group 'ru.isu.math'
version '1.0-SNAPSHOT'
repositories {
  mavenCentral()
}
dependencies {
  testImplementation 'org.junit.jupiter:junit-jupiter-api:5.8.1'
  testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.8.1'
  implementation group: 'org.apache.commons', name: 'commons-math3', version: '3.6.1'
}
test {
  useJUnitPlatform()
}

```

> Актуальные координаты зависимости можно найти на веб-сайте [mvnrepository.com](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1).

После этого можно импортировать пакеты и классы из библиотеки [Apache Commons Math](https://commons.apache.org/proper/commons-math) в разрабатываемые классы.

#### Собрать запускаемый JAR файл

Для того чтобы собрать запускаемый, в файл build.gradle необходимо добавить следующий код:
```xml
jar {
  manifest {
    attributes "Main-Class": "ru.isu.math.example.MyMainClass"
  }
  from {
    configurations.runtimeClasspath.collect {it.isDirectory() ? it: zipTree(it)}
  }
}
```

Обновить Gradle проект, нажав кнопку «Reload All Gradle Projects», удалить предыдущую сборку — «clean» в списке «Tasks | build» и запустить новую сборку — «build» в списке «Tasks | build».

#### Запуск JAR файла в командной строке

Необходимо перейти в папку с запускаемым JAR файлом.
```bash
cd <path to jar directory>
```

Запустить Java VM с флагом -jar, после которого указать имя JARфайла, например:
```bash
java -jar MyProject.jar
```

Командная строка отобразит результаты выполнения JAR файла.

## Задание

**Часть I**

 - Разработать Java программу: вычислить евклидово расстояние между заданными точками.
 -  Создать, собрать и запустить Java проект в IDE.

**Часть II**

 - Скомпилировать Java программу (исходный код) в командной строке.
-  Запустить файл Java программу (байт код) в командной строке.
- Считать параметры командной строки (некоторые точки евклидова пространства)
- Дизассемблировать Java программу (байт код)

**Часть III**

 - Создать, собрать и запустить Maven проект с зависимостью
   «Apache Commons Math»
 - Создать, собрать и запустить Gradle проект с зависимостью «Apache Commons Math»

## Вопросы

1. Платформа разработки JDK
2. Платформа исполнения JRE
3. Интерпретация байт-кода (Just-in-Time компиляция)
4. Main-метод и main-класс
5. Литералы
6. Идентификаторы
7. Локальные переменные
8. Блоки кода
9. Сборка мусора
10. Управляющие инструкции

## Ресурсы

- Г. Шилдт. Java Руководство для начинающих. Глава 1
- [Компилятор javac](https://docs.oracle.com/en/java/javase/13/docs/specs/man/javac.html)
- [Создание проекта в IntelliJIDEA](https://www.jetbrains.com/help/idea/new-project-wizard.html#new-project-no-frameworks)
- [Main-класс и main-метод](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
- [Евклидово расстояние](https://ru.wikipedia.org/wiki/%D0%95%D0%B2%D0%BA%D0%BB%D0%B8%D0%B4%D0%BE%D0%B2%D0%B0_%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%BA%D0%B0)
- [Библиотека «Apache Commons Math»](https://commons.apache.org/proper/commons-math/)
- [Класс Class EuclideanDistance из «Apache Commons Math»](https://commons.apache.org/proper/commons-math/javadocs/api-3.6.1/org/apache/commons/math3/ml/distance/EuclideanDistance.html)
- [Maven репозиторий](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1)
- [IntelliJIDEA на русском](https://www.jetbrains.com/ru-ru/idea/resources)
- [Maven в IntelliJ IDEA](https://www.jetbrains.com/help/idea/maven-support.html)
- [Gradle в IntelliJ IDEA](https://www.jetbrains.com/help/idea/gradle.html)
