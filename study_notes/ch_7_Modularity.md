## Часть 7. Java Platform Module System

Основным нововведением Java 9 было введение модульности.
[О модульности на русском](https://habr.com/ru/post/499872/)
[Baeldung modularity](https://www.baeldung.com/java-9-modularity)

В [JDK 9](https://openjdk.java.net/projects/jdk9/) было введено разделение на модули, а именно, JDK была разделена на 73 модуля. И с каждой новой версией количество этих модулей растет. В 11 версии это число близится к 100. Это разделение позволило разработчикам создать утилиту JLINK. С помощью JLINK можно создавать кастомные наборы JRE, которые будут включают только «нужные» модули, которые реально необходимы вашему приложению. Таким образом, простое приложение и какой-либо _customJRE_ с минимальным (или небольшим) набором модулей в итоге может уместиться в 20 Mb, что не может не радовать.

Список модулей можно посмотреть [здесь](https://cr.openjdk.java.net/~mr/jigsaw/jdk9-module-summary.html).
или выполнив команду `java --list-modules`

Модули поставляются в JAR файлах с пакетами и дескриптором модуля  
_module-info.java_. Файл _module-info.java_ содержит описание модуля:
- имя
- зависимости
-  экспортируемые пакеты
-  потребляемые и предоставляемые сервисы
-  разрешения для reflection доступа.

Команда `javac` принимает параметр `‐‐module‐path`. Вы должны запомнить, что краткая форма этого параметра - `-p`.(используется для указания путей, по которым java или javac будут искать определения модулей.)
`--module` или `-m`: используется для запуска или компиляции только указанного модуля.

Есть несколько допустимых форм параметра classpath:
```
-cp
-classpath 
-‐class-path.
```

### Типы модулей
-   System Modules — Java SE и JDK модули. Полный список можно посмотреть, используя команду `java --list-modules`
-   Application Modules(Named) — модули нашего приложения, которые мы написали, а также те зависимости (от сторонних библиотек), которые использует наше приложение.
-   Automatic Modules — это модули с открытым доступом, создаваемые Java автоматически из JAR-файлов. Допустим, мы хотим запустить наше приложение в модульном режиме, но оно использует какую-то библиотеку. В этом случае мы помещаем JAR-файл на _--module-path_ и Java автоматически создает модуль с именем, унаследованным от имени JAR-файла.
-   Unnamed Module —(модуль без module-info.java) безымянный модуль, автоматически создаваемый из всех JAR-файлов, которые загружены на _--class-path_. Это универсальный модуль для обеспечения обратной совместимости с ранее написанным Java кодом.

Когда мы создаём модуль - мы включаем туда файл-дескриптор, который определяет несколько аспектов нашего нового модулся

-   **Name** – имя
-   **Dependencies** – список всех зависимостей нашего модуля
-   **Public Packages** – список пакетов, которые будут доступны из-вне модуля
-   **Services Offered** – мы можем описать реализации сервисов, которые будут использованы другими модулями
-   **Services Consumed** – позволяет текущему модулю быть потребителем других сервисов
-   **Reflection Permissions** – явно позволяет другим классам использовать reflection чтобы дать доступ к приватным членам пакета

**by default all packages are module private.**
По умолчанию мы не можем использовать рефлексию.


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