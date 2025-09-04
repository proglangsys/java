# 12. Многопоточное программирование

## Методические указания

### Жизненный цикл потока исполнения

1. Создать собственный класс, реализующий интерфейса `Runnable`.
2. Реализовать абстрактный метод `run()` в собственном классе.
3. Создать поток объект типа `Runnable`, экземпляр собственного класса.
4. Создать поток объект класса `Thread`, передав ему в качестве параметра объект типа `Runnable` — экземпляр собственного класса.
5. Вызвать у созданного объекта класса `Thread` метод `start()`. После этого новый поток запуститься. При вызове у этого потока метода `sleep(millis)` он перейдет в режим ожидания на заданное количество миллисекунд `millis` (т.е. данный поток это время не выполняется).
6. Запущенный поток исполняется параллельно с другими запущенными патоками.
7. Поток завершится, когда будет выполнена его последняя инструкция.

![Жизненный цикл потока исполнения](https://www.tutorialspoint.com/java/images/Thread_Life_Cycle.jpg)

### Создание и запуск потоков

Поток исполнения реализуется на основе объекта класса реализующего интерфейс `Runnable`.
```java
public class MyThread implements Runnable {
    String name;

    MyThread( String name) {
        this.name = name;
        System.out.println(this.name + ": CREATED");
    }

    public void run() {
        System.out.println(name + ": RUNNING");
        try {
            for(int i = 0; i < 20; i++) {
                System.out.println(name + ": " + i);
                // Усыпить поток
                Thread.sleep(50);
            }
        } catch (InterruptedException e) {
            System.out.println(name + ": INTERRUPTED");
        }
        System.out.println(name + ": FINISHED");
    }
}
```

Создание и запуск нескольких потоков.
```java
public class DemoApp {
    public static void main(String[] args) {
        // Создать 1-й объект типа Runnable
        MyThread mt1 = new MyThread("Thread-1");
        // Создать 1-й поток
        Thread t1 = new Thread(mt1);
        System.out.println(mt1.name + ": CREATED");
        // Запустить 1-й поток
        t1.start();
        System.out.println(mt1.name + ": STARTED");

        // Создать 2-1 объект типа Runnable
        MyThread mt2 = new MyThread( "Thread-2");
        // Создать 2-й поток
        Thread t2 = new Thread(mt2);
        System.out.println(mt2.name + ": CREATED");
        // Запустить 2-й поток
        t2.start();
        System.out.println(mt2.name + ": STARTED");
    }
}
```

Собственный класс, реализующий интерфейс `Runnable`, можно дополнить для удобства методом запуска потока.
```java
public class MyThread implements Runnable {
    Thread t;
    String name;

    MyThread( String name) {
        this.name = name;
        System.out.println(name + ": CREATED");
    }

    public void run() {
        System.out.println(name + ": RUNNING");
        try {
            for(int i = 0; i < 20; i++) {
                System.out.println(name + ": " + i);
                // Усыпить поток
                Thread.sleep(50);
            }
        } catch (InterruptedException e) {
            System.out.println(name + ": INTERRUPTED");
        }
        System.out.println(name + ": FINISHED");
    }

    public void start() {
        System.out.println(name + ": STARTED");
        if (t == null) {
            t = new Thread(this, name);
            t.start ();
        }
    }
}
```

В этом случае упроститься создание и запуск нескольких потоков.
```java
public class DemoApp {
    public static void main(String[] args) {
        MyThread mt1 = new MyThread( "Thread-1");
        mt1.start();

        MyThread mt2 = new MyThread( "Thread-2");
        mt2.start();
    }
}
```

По умолчанию основной поток завершается, не дожидаясь других потоков, запущенных из него.
```java
public class DemoApp {
    public static void main(String[] args) {
        MyThread mt1 = new MyThread( "Thread-1");
        mt1.start();

        MyThread mt2 = new MyThread( "Thread-2");
        mt2.start();

        // Основной поток завершен
        System.out.println("MAIN THREAD FINISHED");
    }
}
```

Для того чтобы основной поток ожидал завершения порожденных, их можно присоединить к основному следующим образом.
```java
public class DemoApp {
    public static void main(String[] args) {
        MyThread mt1 = new MyThread( "Thread-1");
        mt1.start();
        MyThread mt2 = new MyThread( "Thread-2");
        mt2.start();
        
        try {
            mt1.t.join(); // Присоединить 1-й поток к основному потоку
            mt2.t.join(); // Присоединить 2-й поток к основному потоку
        } catch (InterruptedException e) {
            // Прерывание основного потока
            System.out.println("MAIN THREAD INTERRUPTED");
        }

        // Теперь основной поток ждет завершения присоединенных к нему потоков
        System.out.println("MAIN THREAD FINISHED");
    }
}
```

### Синхронизация потоков

#### Синхронизированный метод
По умолчанию к синхронизированному методу могут обращаться несколько потоков одновременно. Но только один поток имеет доступ к синхронизированному методу. Для того чтобы синхронизировать метод, в его объявление включается ключевое слово `synchronized`.
```java
public class Speaker extends Thread {
    static Microphone microphone = new Microphone();
    String voice;

    Speaker(String voice) {
        this.voice = voice;
    }

    public void run() {
        microphone.say(voice);
    }
}
```

```java
class Microphone {
    // Синхронизированный метод
    synchronized void say(String voice) {
        try {
            for (int i = 0; i < 20; i++) {
                System.out.println(voice + " ");
                Thread.sleep(10);
            }
        } catch (InterruptedException e) {
        }
    }
}
```

```java
public class DemoApp {
    public static void main(String[] args) {
        Speaker cat = new Speaker("meow");
        Speaker dog = new Speaker("woof");
        Speaker cow = new Speaker("moo");
        Speaker pig = new Speaker("oink");

        cat.start();
        dog.start();
        caw.start();
        pig.start();
    }
}
```

## Задание

**Часть I**

- Разработать многопоточное приложение: генератор случайных последовательностей ДНК. 
- Создать 4 потока для генерации текста ДНК, каждый из которых печатает одну из букв ДНК: «T», «C», «G», «A» в командную строку. Созданные потоки должны выполняться одновременно.

_Примеры онлайн генераторов:_
[https://www.bioinformatics.org/sms2/random_dna.html](https://www.bioinformatics.org/sms2/random_dna.html) [http://www.faculty.ucr.edu/~mmaduro/random.htm](http://www.faculty.ucr.edu/~mmaduro/random.htm)

**Часть II**

- Доработать многопоточное приложение: генератор случайных последовательностей ДНК. 
- Создать 4 потока для генерации текста ДНК, каждый из которых печатает одну из букв ДНК: «T», «C», «G», «A» в общую строку типа `StringBuilder`. Созданные потоки должны выполняться одновременно. 
- Пользователем должна настраиваться длинна генерируемой последовательности ДНК. Для каждого потока должен автоматически настраиваться лимит итераций печати для буквы, исходя из заданной длинны последовательности ДНК, также случайным образом должна настраиваться задержка итерации в миллисекундах. По завершении порожденных потоков печати букв, текст ДНК должен быть записан в файл из основного потока.

**Часть III**

- Вариант 1: реализовать многопоточный полнотекстовый поиск заданной подстроки в наборе текстовых файлов.
- Вариант 2: разработать класс микрофон. Класс спикеров, которые могут использовать микрофон. Одновременно только один спикер может говорить в один микрофон. Создать несколько спикеров. Количество микрофонов, доступных для всех спикеров, должно настраиваться.

_Можно выбрать и сделать только один вариант самостоятельно._

## Вопросы

1.	Многозадачность
2.	Многопоточность
3.	Создание потока
4.	Определение момента завершения потока
5.	Приоритеты
6.	Синхронизация
7.	Синхронизированные методы
8.	Синхронизированные блоки кода
9.	Ожидание и нотификация потоков

## Ресурсы

1.	Г. Шилдт. Java Руководство для начинающих. Глава 11.	
2. https://www.tutorialspoint.com/java/java_multithreading.htm
