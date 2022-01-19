# Часть 9. Java I/O API
![](img/IO_streams_diagrams.jpg)

`InputStream` - абстрактный класс
в нём есть метод
`mark()` - помечает элемент, и в случае использования метода reset(), переходит к элементу, на котором был вызван метод mark().
Но не все реализации `InputStream` поддерживают метод `mark()`. Нужно это помнить, и всегда вызывать `markSupported()` перед использованием `mark()`, чтобы не получить исключение.

`InputStream` - это необработанный метод получения информации из ресурса. Он захватывает данные побайтно, не выполняя никакого преобразования. Если вы читаете данные изображения или любой двоичный файл, то следует использовать этот поток.

`Reader` разработан для символьных потоков. Если информация, которую вы читаете, представляет собой весь текст, то Reader позаботится о декодировании символов за вас и предоставит вам символы Unicode из необработанного входного потока. Если вы читаете текст любого типа, то следует использовать `Reader`.

Вы можете обернуть `InputStream` и превратить его в `Reader` с помощью класса `InputStreamReader`.

Интерфейс `Comparable`:
```java
public interface Comparable<T> {
	public int compareTo(T o);	
}
```

Основные понятия классы и интерфейсы
`Path` - Интерфейс в котором есть много методов для работы с Путями
- сравнение
- объединение
- конвертация
- нормализация
- получение разной информации
  подробнее [Baedung Path API](https://www.baeldung.com/java-nio-2-path)
```java
 interface Path extends Comparable<Path>, Iterable<Path>, Watchable
```
**!!!ВАЖНО!!!** все объекты типа Path являются immuteble. Его методы не изменяют сам объект а возвращают новое значение.


Методы:
```java
 Path resolve(Path other)
```
Строит новый абсолютный путь из абсолютного и относительного.
[Подробнее](https://www.baeldung.com/java-nio-2-path#joining-paths)
_Если в качестве аргумента передаётся абсолютный путь. То метод вернёт его. А если относительный, то метод просто склеит 2 пути._

```java
 Path realtivize(Path other)
```
Термин _relativizing_ означает создание  прямого пути между двумя имеющимися путями
ВАЖНО!
**Чтобы `relativize` не выбросил исключение, то оба пути должны быть или абсолютные или относительные.**

Метод relativize (Path other) в java.nio.file.Path используется для создания относительного пути между текущим путем и заданным путем в качестве параметра.
Релятивизация - это обратное разрешение. Этот метод создает относительный путь, который при разрешении относительно этого объекта пути дает путь, которыйпомогает нам найти тот же файл, что и указанный путь.

Например, если этот путь - `/dir1/dir2`, а указанный путь в качестве параметра - `/dir1/dir2/dir3/file1`, то этот метод создаст относительный путь `dir3/file1`. Если текущий путь и данный путь не имеют корневого компонента, можно построить относительный путь.
Если какой-либо из путей имеет корневой компонент, то относительный путь не может быть построен. Если оба пути имеют корневой компонент, то возможность построения относительного пути зависит от реализации. Если текущий путь и данный путь равны, возвращается пустой путь.


`Paths` - класс всего с двумя статическими методами
```java
public final class Paths {  
    private Paths() { }  
  
 public static Path get(String first, String... more) {  
        return Path.of(first, more);  
 }  
  
 public static Path get(URI uri) {  
        return Path.of(uri);  
 }  
}
```

`Files` - Класс, который производит действия с файлами. [Baeldung File API](https://www.baeldung.com/java-nio-2-file-api)
- проверка на директорию
- открыт ли файл для записи/чтения
- сущестует ли файл
- исполняемый ли файл
- создаёт файлы и директории из Path
- позволяет создавать временные файлы в home директории одной командой
```java
	Files.createTempFile(p, prefix, suffix);
```
- Удаление файлов
- копирование с разными опциями
- перемещение с разными опциями
- Поиск файлов по параметрам
  `find` - задаёт параметры поиска и посщения файлов, глубину обхода, опции посещения
 ```java
 public static Stream<Path> find(Path start, int maxDepth, BiPredicate<Path, BasicFileAttributes> matcher, FileVisitOption... options)
 ```

```walk()``` - обход файлового дерева с указанием глубины и опциями посещения файлов. Есть 2 реализации
```java
public static Stream<Path> walk(Path start, int maxDepth, FileVisitOption... options)
 
 public static Stream<Path> walk(Path start, FileVisitOption... options) throws IOException {  
    return walk(start, Integer.MAX_VALUE, options);  
}
```

`Files.lines() method returns Stream<String>`
`Files.readAllLines() method returns List<String>`
`Files.walk() returns Stream<Path>`

**Сериализация** — это процесс сохранения состояния объекта в последовательность байт.
**Десериализация** — это процесс восстановления объекта из этих байт.

Интерфейс `Serializable` - marker interface
Интерфейс сериализации не имеет методов или полей и служит только для определения сериализации.

_serialPersistentFields_ - переменная, в которую можно положить _whiteList_ список полей для сериализции

_transient_ - модификатор доступа, для создания blackList полей для сериализации.

```java
	class List implements Serializable {
    List next;

    private static final ObjectStreamField[] serialPersistentFields
                 = {new ObjectStreamField("next", List.class)};

}
```

# Конспект по Java SE 11
- [Часть 1. Типы данных](ch_1_DataTypes.md)
- [Часть 2. Program Flow. Loops](ch_2_Program_flow.md)
- [Часть 3. ООП](ch_3_Oop.md)
- [Часть 4. Исключения](ch_4_Exceptions.md)
- [Часть 5. Arrays](ch_5_Arrays.md)
- [Часть 6. Streams](ch_6_Streams.md)
- [Часть 7. Модульность](ch_7_Modularity.md)
- [Часть 8. Concurrency](ch_8_Concurrency.md)
- [Часть 9. IO](ch_9_IO.md)
- [Часть 10. Secure coding](ch_10_Secure_coding.md)
- [Часть 11. JDBC](ch_11_JDBC.md)
- [Часть 12. Локализации](ch_12_Localization.md)
- [Часть 13. Аннотации](ch_13_Annotations.md)