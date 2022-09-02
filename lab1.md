# 1. ���������������� �������� ����������

## ������������ ��������

### ��������� ���������� JDK

[Java Development Kit](https://ru.wikipedia.org/wiki/Java_Development_Kit) (JDK) � �������� ���������������� ������� ��� ���������� ���������� �� ����� [Java](https://ru.wikipedia.org/wiki/Java). �������� ���������� [javac](https://ru.wikipedia.org/wiki/Javac), �������, ���������� ������� Java API, ������������ � �������, ����� ���������� ���������� � [Java Runtime Environment](https://ru.wikipedia.org/wiki/Java_Runtime_Environment) (JRE).

JRE �������� ����������� ������ [Java VirtualMachine](https://ru.wikipedia.org/wiki/Java_Virtual_Machine) (VM) � ����������������� ���������� ������� Java API. ��������� ��������� Java ���������� �� ����� ����������� ��� ������������ ��������.

���������� ��� �������� JDK:

- SE (Standard Edition) � ����������� �������� JDK, ������� ������������ ��� ���������� ���������� � ���������� ����������.
- EE (Enterprise Edition) � �������� ��� ���������� �������������� ���������� �������� �����������.
- ME (Micro Edition) � �������� ��� ���������� ���������� ��������� ��������� � ������������ ������.

### ��������������� ����� ����������

Integrated Development Environment (IDE) � �������� ����������� �������, ������������ �������������� ��� ���������� ������������ ����������� (��), � ��� �����, ��������� ��������, �������� ������������� ������, ��������.

���������� ��������� ���������� IDE ��� ���������� Java ����������:
- [IntelliJ IDEA](https://www.jetbrains.com/idea/)
- [Eclipse](https://eclipseide.org/release/)
- [NetBeans](https://netbeans.apache.org/)

��� ���������� ������� ���������� ���������� ��������� ���������������� ��������:

- [Oracle JDK SE](https://www.oracle.com/java/technologies/downloads/) ��� [OpenJDK](https://openjdk.org/install/) (������ 8 ��� ����).
- [IntelliJ IDEA Community Edition](https://www.jetbrains.com/ru-ru/idea/download/#section=windows)

### Main-�����

Main-����� � �����, � ������� ���� main-�����. Main-����� ��������� ����� ���������� ����������, ���������� ����������� ������� Java VM:
```java
public class MyMainClass {
    // main-����� 
    public static void main(String[] args) {
        // ����������
    }
}
```

����� ������ � ��������� ������ �������������� ����� ���������� ����� ������:
```java
public class MyMainClass {
    // main-__�����_  
    public static void main(String[] args) {  
        // ������� ��������� "my text" � ��������� ������
        System.out.println("my text");  
    }  
}
```

### ��������, ������ � ������ �������

#### ������� ����� ������

��������� �IntelliJ IDEA�. ���� ������ �������������� ����� �Welcome to IntelliJ IDEA�, ������ ������ �New Project�. ���� ������� �������� ����, ������� ����� ���� �File | New | Project�.

![������ ������: �������� ������ �������](https://github.com/proglangsys/java/blob/main/images/lab1_1.png)

������� ����� �New Project� �� ������ �����. ������ ��� ������ ������� �Name� � �������� ��� ����������������� �Location�, ���� ����������. � ������ �Languages� ������ ���� ������ ���� �Java�. � ������ �JDK� ������ ���� ������� JDK ������ 8 ��� ����.

#### ������� ����� � �����

� ���� �Project� �������� ������ ������� ���� ����� �src�, ������� ����� �New | Java Class� (Alt+Insert).

![������ ������: �������� ������ ������](https://github.com/proglangsys/java/blob/main/images/lab1_2.png)

������ ������ ��� ������ ��������� �������: �ru.isu.math.example.MyMainClass� � ������ ������ �OK�. � ���������� ����� ������ ����� �ru.isu.math.example� � ����� �MyMainClass� ������ ����� ������.

```java
package ru.isu.math.example;  
  
public class MyMainClass {  
}
```

#### �������� ���

�������� � ��������� ����� main-����� � ������������ ������������.
```java
package ru.isu.math.example;  
  
public class MyMainClass {  
    public static void main(String[] args) {  
        System.out.println("Hello World!");  
    }  
}
```

#### ������� � ��������� ����������

������� ����� ���� �Run | Run�� ��� ������ ������ �Run� �� ������ ������������ ������ � �������� ����������� (Alt+Shift+F10). � ������������ ������ ������� �MyMainClass�.

���������� ���������� ��������� ���� ��������� � ����-��� � ����� ���������� ���������� � Java VM. ��������� ���������� ���������, ��������� �HelloWorld!�, ����� ���������� �� ���������� ��������� ������.

![������ ������: ������ (�����) � ������������� ����� (������)](https://github.com/proglangsys/java/blob/main/images/lab1_3.png)

### ���������� � ������ �� ��������� ������

��� ���� ����� ��������������� ����� �� ��������� ������, ���������� ������� � ����������, � ������� ��������� ���� � �������� �����:
```bash
cd <path to the scr directory>
```
��������� ���������� javac, ������ � �������� ��������� �������� ����� � �������� ����� � �����������:
```bash
javac -d target ru/isu/math/example/MyMainClass.java
```

� ���������� ���������� ������� ���� � ����-����� � ��� �� ������ ������, �� ����������� �class� � �MyMainClass.class� � ����� �target/ru/isu/math/example�.

��� ���� ����� ��������� ����������������� ����� ���������� ������� � ����������, � ������� ��������� ���� � ����-�����:
```bash
cd <path to the target directory>
```
� ��������� Java VM, ������ � �������� ��������� �������� ����� � ����-����� ��� ����������:
```bash
java ru.isu.math.example.MyMainClass
```

� ������ ����, ���������� ����� JAVA_HOME �� ���������, ������� ��������� ������ ���� � ����������� javac � ����������� ������ java ��������������:
```bash
<path to JDK>/bin/javac -d target ru/isu/math/example/MyMainClass.java
<path to JDK>/bin/java ru.isu.math.example.MyMainClass
```

### ������������������ ����-����

��� ���� ����� ����������������� ����������������� ����� ���������� ������� � ����������, � ������� ��������� ���� � ����-�����:
```bash
cd <path to the target directory>
```

��������� ������������ javap, ������ � �������� ��������� �������� ����� � ����-�����:
```bash
javap -c ru/isu/math/example/MyMainClass.class
```

� ������ ����, ���������� ����� JAVA_HOME �� ���������, ������� ��������� ������ ���� � ������������� javap:
```bash
<path to JDK>/bin/javap -c ru/isu/math/example/MyMainClass.class
```

��������� ������������������ ����-���� ��������� � ��������� ������.

![������ ������: ��������� ������������������ ����-����](https://github.com/proglangsys/java/blob/main/images/lab1_4.png)

### ���������� � ����� ����

_���������� ����_ � ������� ��� ���������� � Java VM. ���������� ������������� ������ � ������� `;`.
```java
// �������� � ���������������� ���������� �������������� ����
int x = 1; 
```

_���� ����_ � ����� ����������, ����������� � ���� ������������ �������� ������.
```java
{  
    int x = 1;
    x = x + 2;  
}
```

### ��������� ����������

_��������� ����������_ � ��� ����������, ����������� ������ ����� ����. ������� ��������� ����� ���������� ���������� ������ ����, � ������� ��� ���������.
```java
public static void main(String[] args) {  
    int x; // �������� ��������� ����������
    x = 1; // ��������� �������� ��������� ����������
    System.out.println("x = " + x); // ������� �������� ����������
}
```

��� ���������� ���������� ���������� ������� �� ��� ������. ��������, ���� ���������� ����� ��� `int`, �� � �������� ����� �������� ��� ����� ��������� ������ ����� �����:
```java
int x = 2;
```
����������, ����������� � ����� `double`, �������� ������ ������������ �����:
```java
double y = 2.5;
```
���������� � ����� String, ����� ��������� �� ������
```java
String s = "my text";
```

### ���� for

_����_  � ����������� ����������, ������� ���������� ���������� ������������ ����� ���� (���� �����) ��������� ���.

���� for ����� ��������� ���������:
```java
for (������������� ��������; ������� ����������; ��������) ���� ����
```

��������, ��������� ���� ��������� ���������� ���� ������ ���:
```java
for (int i = 0; i < 10; i++) {  
    System.out.println("i = " + i);  
}
```

### ��������� ��������� ������

��������� ��������� ������ ���������� ���������� � ���� ������������� ��������� main-������ � ������� �����:
```java
public class MyMainClass {  
    public static void main(String[] args) {
        // ������� ��������� ��������� ������
        for (int i = 0; i < args.length; i++) {
            String arg = args[i];
            System.out.printf("Argument %d: %s%n", i, arg);
        }
    }
}
```

��� ������� ���������� �� ��������� ������ ��������� ����������� ����� ����� main-������:
```bash
java ru.isu.math.example.MyMainClass p0 p1 p2
```

��� ���� ����� ������ ��������� ��������� ������ � IDE, ���������� ������� ����� ������������ ������� ��������� �������: ������� ����� ���� �Run | Edit Configurations��, �������� ����� ������������, ������ � ������ ����� ����� �Application�, ������ ��� ��� �������������, ������� main-�����, ������ �������� ���������� � ���� �Program Arguments�, ������ ������ �OK�.

![������ ������: �������� ������������ ������� ����������](https://github.com/proglangsys/java/blob/main/images/lab1_5.png)

����� ��������� ��������� � ������� ��������� ������������, ������ �� �� ����� � ���������� ������ ����� �� ������ ������� �Run�.

![������ ������: ��������� ������� ����������](https://github.com/proglangsys/java/blob/main/images/lab1_6.png)


### ��������� ���������� ����� ��������� �������

��� ���� ����� ����������� ������������ ![p_1=\left(x_1,y_1\right)](https://bit.ly/3ReTrYQ) � ![p_2=\left(x_2,y_2\right)](https://bit.ly/3eg69b8) ��������� ���������� ����������� ���������:
![d\left( p1,p2 \right)=\sqrt[]{\left( x_1 - x_2 \right)^{2}+\left( y_1 - y_2 \right)^{2}}](https://bit.ly/3KKdr3i) 
��� ���������� ���� ������� � Java ����� ������������ ����� [Math](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html) (�������� ������ Java API) ������� ������������ �������� ������������������ �������� ��� �������, ��������:
```java
double x = 4;  
Math.pow(x, 2); // ���������� x � ������� 2 
Math.sqrt(x); // ���������� ������ �� x
```

��������������� ������� ����� ���� ����������� ��������� �������:
```java
double d = Math.sqrt(Math.pow(x1-x2, 2) + Math.pow(y1-y2, 2));
```

������ ������ ���������� ���������� ��������� ���������� � Java ������� � ���, ����� ��������������� ������� �������, ������������ � ������� ��������� ����������, �������� [Apache Commons Math](https://commons.apache.org/proper/commons-math).

### �������� � ������ ������� Maven

#### ������� ����� ������

���� ������ �������������� ����� �Welcome to IntelliJ IDEA�, ������ ������ �New Project�. ���� ������� �������� ����, ������� ����� ���� �File | New | Project�.

� �������� ������� ������ �Build system� ������� �Maven�. �������� ��� ������� �Name� � ����������������� ��� ������ �Location� ��� �������������, � ����� �GroupId� � �ArtifactId� � ������� ������ �Advanced Settings�.

![������ ������: �������� Maven �������](https://github.com/proglangsys/java/blob/main/images/lab1_7.png)

#### �������� ����� � ������� ������

�������� ����� � ����� � �������� ����� � ����� �src/main/java�. �������� ������ �Maven� ������, ����� ������ �������� ����� �install� � ������ �Lifecycle�. ���������� ������� ������ �������. �� ������ �Run� ����� ����� ������� ��������� �� �������� ���������� ������ �[INFO] BUILD SUCCESS�. �� ������ �Project� (�����) ����� ������� ���������� ������ � JAR �����, ������� ����� target.

![������ ������: ������ Maven �������](https://github.com/proglangsys/java/blob/main/images/lab1_8.png)

#### �������� ����������� � ������������� �����

������� ���� pom.xml, ������ ��� �� ������ ��������� ������� �Project�. �������� ���� ����� `<dependencies></dependencies>` � ����� ����� ������������� ����� ��������� �������:
```xml
<?xml version ="1.0" encoding="UTF-8"?>  
<project ...>  
...  
<dependencies>  
</dependencies>  
</project>
```

�������� ���������� ����������� �� ���������� [Apache Commons Math](https://commons.apache.org/proper/commons-math) � ������ dependencies ��������� �������:
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

> ���������� ���������� ����������� ����� ����� �� ���-����� [mvnrepository.com](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1).

����� ���������� �����������, ������ � ������ ���������� [Apache Commons Math](https://commons.apache.org/proper/commons-math) ���������� ���������� ��� ������� � ��������������� ������. ��������, ��� ���� ����� ������������ ������� ���������� ���������� ����������� ������������ ������� ������������� ����� �� ������ ���������� org.apache.commons.math3.ml.distance.EuclideanDistance ��� �������� ����:
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

#### ������� �����������  JAR ����

��� ���� ����� ������� �����������, � ���� pom.xml ���������� �������� ��������� ���:
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

�������� Maven ������, ����� ������ �Reload All Maven Projects�, ������� ���������� ������ � �clean� � ������ �Lifecycle� � ��������� ����� ������ � �install� � ������ �Lifecycle�.

### �������� � ������ ������� Gradle

#### ������� ����� ������

���� ������ �������������� ����� �Welcome to IntelliJ IDEA�, ������ ������ �New Project�. ���� ������� �������� ����, ������� ����� ���� �File | New | Project�.

� �������� ������� ������ �Build system� ������� �Gradle�. �������� ��� ������� �Name� � ����������������� ��� ������ �Location� ��� �������������, � ����� �GroupId� � �ArtifactId� � ������� ������ �Advanced Settings�.

#### �������� ����� � ������� ������

�������� ����� � ����� � �������� ����� � ����� src/main/java. �������� ������ �Gradle� ������, ����� ������ �������� ����� �build� � ������ �Tasks | build�. ���������� ������� ������ �������. �� ������ �Run� ����� ����� ������� ��������� �� �������� ���������� ������ �BUILD SUCCESSFUL�. �� ������ �Project� (�����) ����� ������� ���������� ������ � JAR �����, ������� ����� build/libs.

![������ ������: ������ Gradle �������](https://github.com/proglangsys/java/blob/main/images/lab1_9.png)

#### �������� ����������� � ������������� �����

������� ���� build.gradle, ������ ��� �� ������ ��������� ������� �Project�. �������� ������ � ������������ ����������� �� ���������� [Apache Commons Math](https://commons.apache.org/proper/commons-math):
```
implementation group: 'org.apache.commons', name: 'commons-math3', version: '3.6.1'
```
� ������ �dependencies� ��������� �������:
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

> ���������� ���������� ����������� ����� ����� �� ���-����� [mvnrepository.com](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1).

����� ����� ����� ������������� ������ � ������ �� ���������� [Apache Commons Math](https://commons.apache.org/proper/commons-math) � ��������������� ������.

#### ������� ����������� JAR ����

��� ���� ����� ������� �����������, � ���� build.gradle ���������� �������� ��������� ���:
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

�������� Gradle ������, ����� ������ �Reload All Gradle Projects�, ������� ���������� ������ � �clean� � ������ �Tasks | build� � ��������� ����� ������ � �build� � ������ �Tasks | build�.

#### ������ JAR ����� � ��������� ������

���������� ������� � ����� � ����������� JAR ������.
```bash
cd <path to jar directory>
```

��������� Java VM � ������ -jar, ����� �������� ������� ��� JAR�����, ��������:
```bash
java -jar MyProject.jar
```

��������� ������ ��������� ���������� ���������� JAR �����.

## �������

����� I. 

 - ����������� Java ���������: ��������� ��������� ���������� ����� ��������� �������. 
 -  �������, ������� � ��������� Java ������ � IDE.

����� II. 

 - �������������� Java ��������� (�������� ���) � ��������� ������.
-  ��������� ���� Java ��������� (���� ���) � ��������� ������. 
- ������� ��������� ��������� ������ (��������� ����� ��������� ������������)
- ����������������� Java ��������� (���� ���) 
- ������������� ������������ Java ��������� �� doc-�����������

����� III. 

 - �������, ������� � ��������� Maven ������ � ������������
   �Apache Commons Math� 
 - �������, ������� � ��������� Gradle ������ � ������������ �Apache Commons Math�

## �������

1. ��������� ���������� JDK
2. ��������� ���������� JRE
3. ������������� ����-���� (Just-in-Time ����������)
4. Main-����� � main-�����
5. ��������
6. ��������������
7. ��������� ����������
8. ����� ����
9. ������ ������
10. ����������� ����������

## �������

- �. �����. Java ����������� ��� ����������. ����� 1
- [���������� javac](https://docs.oracle.com/en/java/javase/13/docs/specs/man/javac.html)
- [�������� ������� � IntelliJIDEA](https://www.jetbrains.com/help/idea/new-project-wizard.html#new-project-no-frameworks)
- [Main-����� � main-�����](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
- [��������� ����������](https://ru.wikipedia.org/wiki/%D0%95%D0%B2%D0%BA%D0%BB%D0%B8%D0%B4%D0%BE%D0%B2%D0%B0_%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%BA%D0%B0)
- [���������� �Apache Commons Math�](https://commons.apache.org/proper/commons-math/)
- [����� Class EuclideanDistance �� �Apache Commons Math�](https://commons.apache.org/proper/commons-math/javadocs/api-3.6.1/org/apache/commons/math3/ml/distance/EuclideanDistance.html)
- [Maven �����������](https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6.1)
- [IntelliJIDEA �� �������](https://www.jetbrains.com/ru-ru/idea/resources)
- [Maven � IntelliJ IDEA](https://www.jetbrains.com/help/idea/maven-support.html)
- [Gradle � IntelliJ IDEA](https://www.jetbrains.com/help/idea/gradle.html)
