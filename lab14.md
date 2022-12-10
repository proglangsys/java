# 14. Пользовательский интерфейс Java FX

## Методические указания

### JavaFX приложение

_Stage_ — платформа, это контейнер верхнего уровня для размещения сцен.

_Scene_ — сцена, это контейнер для размещения UI-элементов (кнопки, текстовые поля, меню и др.).

Каждый UI-элемент сцены представляется узлом — объектом типа Node. У любого узла могут быть _дочерние узлы_. Узел, имеющий дочерние узлы, называется _родительским_. Узлы, не имеющие дочерних узлов, являются оконечными и называются _листьями_. Совокупность всех узлов сцены называется _графом сцены_ и образует _дерево_, т.е. иерархическую структуру узлов.

Панель компоновки осуществляет размещение UI-элементов внутри сцены. Стандартные панели компоновки — `FlowPane`, `GridPane`, `BorderPane`.

Приложение JavaFX — объект подкласса класса `Application`.

**Жизненный цикл приложения JavaFX:**

Метод `init()` вызывается в начале выполнения приложения и служит для инициализации всех необходимых переменных.

Метод `start()` вызывается при запуске приложение; его можно использовать для конструирования и установки параметров сцены. В качестве аргумента ему передается ссылка на объект Stage — основную платформа, которую предоставляет исполняющая среда.

Метод `stop()` вызывается по завершении работы приложения; используется для освобождения ресурсов, захваченных приложением.

Метод `launch()` запускает приложение.

### Создание JavaFX приложения

Стартовое приложение.
```java
package proglangsys.javafx;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;
import java.io.IOException;

public class HelloApplication extends Application {
    @Override
    public void start(Stage stage) throws IOException {
        FXMLLoader fxmlLoader = new FXMLLoader(HelloApplication.class.getResource("hello-view.fxml"));
        Scene scene = new Scene(fxmlLoader.load(), 320, 240);
        stage.setTitle("Hello!");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

Простой текстовый редактор.
```java
package proglangsys.javafx;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.BorderPane;
import javafx.stage.FileChooser;
import javafx.stage.Stage;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;

public class MySimpleTextEditor extends Application {
    TextArea textArea = new TextArea();

    @Override
    public void start(Stage stage) {
        Menu menuFile = new Menu("File");

        MenuItem miNew = new MenuItem("New");
        miNew.setOnAction(e -> clear());
        MenuItem miOpen = new MenuItem("Open");
        miOpen.setOnAction(e -> open());
        MenuItem miSave = new MenuItem("Save");
        miSave.setOnAction(e -> save());
        menuFile.getItems().addAll(miNew, miOpen, miSave);

        Menu menuEdit = new Menu("Edit");

        MenuItem miCut = new MenuItem("Cut");
        MenuItem miCopy = new MenuItem("Copy");
        MenuItem miPaste = new MenuItem("Paste");

        menuEdit.getItems().addAll(miCut, miCopy, miPaste);

        MenuBar mb = new MenuBar();
        mb.getMenus().add(menuFile);
        mb.getMenus().add(menuEdit);

        BorderPane rootNode = new BorderPane() ;
        rootNode.setTop(mb);
        rootNode.setCenter(textArea);

        Scene scene = new Scene(rootNode, 600, 400);
        stage.setTitle("My Simple Text Editor");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }

    public void clear() {
        textArea.setText("");
    }

    public void open() {
        FileChooser fileChooser = new FileChooser();
        File file = fileChooser.showOpenDialog(null);

        if (file == null) return;

        try {
            String text = Files.readString(file.toPath());
            textArea.setText(text);
        } catch (IOException e) {
            new Alert(Alert.AlertType.INFORMATION, e.getMessage()).showAndWait();
        }
    }

    public void save() {
        FileChooser fileChooser = new FileChooser();
        File file = fileChooser.showSaveDialog(null);

        if (file == null) return;

        try {
            String text = textArea.getText();
            Files.writeString(file.toPath(), text);
        } catch (IOException e) {
            new Alert(Alert.AlertType.INFORMATION, e.getMessage()).showAndWait();
        }
    }
}
```

### FXML

FXML язык разметки на основе XML, позволяющий определить интерфейс JavaFX приложения декларативным способом.

**Простой текстовый редактор с помощью FXML**

Структура проекта.
```
java 
|--proglangsys.javafx 
|   |-- Controller.java 
|   L-- MySimpleTextEditor.java
L-- module-info.java 

resources 
L-- proglangsys 
    L-- view.fxm
```

Приложение `MySimpleTextEditor.java`.

```java
package proglangsys.javafx;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;
import java.io.IOException;
import java.net.URL;

public class MySimpleTextEditor extends Application {
    @Override
    public void start(Stage stage) throws IOException {
        URL fxml = MySimpleTextEditor.class.getResource("view.fxml");
        FXMLLoader fxmlLoader = new FXMLLoader(fxml);
        Scene scene = new Scene(fxmlLoader.load(), 600, 400);
        stage.setTitle("My Simple Text Editor");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

Контроллер `Controller.java`.

```java
package proglangsys.javafx;

import javafx.event.ActionEvent;
import javafx.scene.control.Alert;
import javafx.scene.control.TextArea;
import javafx.stage.FileChooser;

import java.io.*;
import java.nio.file.Files;

public class Controller {
    public TextArea textArea;

    public void clear(ActionEvent event) {
        textArea.setText("");
    }


    public void open(ActionEvent event) {
        FileChooser fileChooser = new FileChooser();
        File file = fileChooser.showOpenDialog(null);

        if (file == null) return;

        try {
            String text = Files.readString(file.toPath());
            textArea.setText(text);
        } catch (IOException e) {
            new Alert(Alert.AlertType.INFORMATION, e.getMessage()).showAndWait();
        }
    }

}
```

Представление `view.fxm`.

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>

<BorderPane xmlns="http://javafx.com/javafx/10.0.2-internal" xmlns:fx="http://javafx.com/fxml/1"
            fx:controller="proglangsys.javafx.Controller">
    <top>
        <MenuBar>
            <Menu text="File">
                <MenuItem text="New" onAction="#clear"/>
                <MenuItem text="Open" onAction="#open"/>
                <MenuItem text="Save" onAction="#save"/>
            </Menu>
            <Menu text="Edit">
                <MenuItem text="Open" onAction="#open"/>
                <MenuItem text="Save" onAction="#save"/>
            </Menu>
        </MenuBar>
    </top>
    <center>
        <TextArea fx:id="textArea" editable="true"/>
    </center>
</BorderPane>
```

Модуль `module-info.java`.

```java
module proglangsys.javafx {
    requires javafx.controls;
    requires javafx.fxml;
    requires java.logging;
    
    opens proglangsys.javafx to javafx.fxml;
    exports proglangsys.javafx;
}
```

## Задание

_Можно выбрать и сделать только один вариант._

_Реализация пользовательского интерфейса должна быть выполнена только с помощью библиотеки JavaFX._

**Часть I**

_Вариант 1_: текстовый редактор без форматирования открытием/сохранением файлов в формат TXT.

_Вариант 2_: графический редактор с возможностью добавления графических фигур на полотно.

**Часть II**

_Вариант 1_: текстовый редактор с форматированием.

_Вариант 2_: графический редактор с drag&drop.

**Часть III**

_Вариант 1_: текстовый редактор с форматированием и открытием/сохранением файлов в формат HTML. Форматированный текст представлять с помощью [HTML тегов форматирования текста](https://www.w3schools.com/html/html_formatting.asp).

_Вариант 2_: графический редактор с drag&drop и сохранением файлов в графический формат.

## Вопросы

1.	Компоненты
2.	MVC
3.	Контейнеры
4.	Обработка событий

## Ресурсы

1.	[Openjfx: Getting Started with JavaFX](https://openjfx.io/openjfx-docs)
2.	[Jenkov: JavaFX Tutorial](https://jenkov.com/tutorials/javafx/index.html)
3.	[GeeksForGeeks: JavaFX | TextFlow Class](https://www.geeksforgeeks.org/javafx-textflow-class/?ref=gcse)
4.	[GeeksForGeeks: JavaFX | Canvas Class](https://www.geeksforgeeks.org/javafx-canvas-class/?ref=gcse)
