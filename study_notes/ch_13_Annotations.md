# Часть 13. Аннотации
Аннотации Java - это механизм для добавления информации метаданных в наш исходный код. Это мощная часть Java, которая была добавлена в JDK5. Аннотации предлагают альтернативу использованию дескрипторов XML и интерфейсов маркеров.

Хотя мы можем прикреплять их к пакетам, классам, интерфейсам, методам и полям, аннотации сами по себе не влияют на выполнение программы.

По сути, аннотация назначает дополнительные метаданные исходному коду, к которому она привязана. Добавляя аннотацию к методу, интерфейсу, классу или полю, мы можем:
- Сообщать компилятору о предупреждениях и ошибках
- Манипулировать исходным кодом во время компиляции
- Изменить или изучить поведение во время выполнения

Тип элемента аннотации должен быть примитивным типом, String, Class, enum, другой аннотацией или массивом любого из этих типов.

Чтобы аннотацию можно было использовать без имени параметра, то она должна содержать в себе параметр `value()`, тогда её можно использовать как `@SomeAnn("text")`, иначе надо указывать название параметра `@SomeAnn(param="someParam")`. Также аннотация value считается опциональной.

## @Native
Начиная с Java 8, в пакете java.lang.annotation появилась новая аннотация под названием Native. Аннотация @Native применима только к полям. Он указывает, что аннотированное поле является константой, на которую можно ссылаться из собственного кода. Например, вот как он используется в классе Integer:
```java
public final class Integer {
    @Native public static final int MIN_VALUE = 0x80000000;
    // omitted
}
```
Эта аннотация также может служить подсказкой для инструментов для создания некоторых вспомогательных файлов заголовков.

## Мета аннотации
Мета аннотации - это аннотации, которые можно применять к другим аннотациям(для конфигурации)

### @Target
Чтобы определить целевые элементы пользовательской аннотации, нам нужно пометить ее аннотацией @Target.
```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD})
public @interface SafeVarargs {
}
```

Варианты:
```
	ElementType.TYPE  
	ElementType.FIELD
	ElementType.METHOD
	ElementType.PARAMETER
	ElementType.CONSTRUCTOR 
	ElementType.LOCAL_VARIABLE
	ElementType.ANNOTATION_TYPE
	ElementType.PACKAGE  
	ElementType.TYPE_USE
	ElementType.MODULE
```

### @Retention
Некоторые аннотации предназначены для использования в качестве подсказок для компилятора, а другие используются во время выполнения.

Мы используем аннотацию @Retention, чтобы указать, где в жизненном цикле нашей программы применяется наша аннотация.

Для этого нам нужно настроить @Retention с одной из трех политик хранения:

1. _RetentionPolicy.SOURCE_ - не виден ни компилятором, ни средой выполнения
2. _RetentionPolicy.CLASS_ - виден компилятором
3. _RetentionPolicy.RUNTIME_ - отображается компилятором и средой выполнения.

Если в объявлении аннотации нет аннотации @Retention, то по умолчанию используется политика хранения RetentionPolicy.CLASS.

### @Inherited
В некоторых ситуациях нам может потребоваться подкласс, чтобы аннотации были привязаны к родительскому классу.

Мы можем использовать аннотацию @Inherited, чтобы наша аннотация распространялась от аннотированного класса к его подклассам.
```java
@Inherited
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface InheritedAnnotation {
}

@InheritedAnnotation
public class BaseClass {
}

public class DerivedClass extends BaseClass {
}
```

### @Documented
По умолчанию Java не документирует использование аннотаций в документации Javadocs.  
Но мы можем использовать аннотацию @Documented, чтобы изменить поведение Java по умолчанию.  
Если мы создадим настраиваемую аннотацию, в которой используется @Documented:

### @Repeatable
Иногда бывает полезно указать одну и ту же аннотацию более одного раза для данного элемента Java.  
До Java 7 нам приходилось группировать аннотации в одну аннотацию контейнера:
```java
@Schedules({
    @Schedule(time = "15:05"),
    @Schedule(time = "23:00")
})
void scheduledAlarm() {
}
```

Теперь можно так:
```java
@Repeatable(Schedules.class)
public @interface Schedule {
    String time() default "09:00";
}
```

```java
public @interface Schedules {
    Schedule[] value();
}
```

```java
@Schedule
@Schedule(time = "15:05")
@Schedule(time = "23:00")
void scheduledAlarm() {
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