# Часть 10. Secure coding at Java SE

**distributed denial-of-service attack** (**DDoS attack**) связана с перегрузкой системы слишком большим объемом данных или слишком большим количеством запросов для обработки законных входящих запросов.

Инклюзиваня уязвимость
[File inclusion vulnerability](https://en.wikipedia.org/wiki/File_inclusion_vulnerability)
- уязвимсоть связанная с загрузкой файлов с вредоносным кодом на сервер.

Интерфейс `Cloneable` – это так называемый интерфейс-маркер, который не содержит никаких методов. Он используется, чтобы маркировать (помечать) некоторые классы.
Метод clone () унаследован от класса Object. По этой причине его можно вызывать для любого объекта, не вызывая ошибки компилятора. С другой стороны, если класс реализует Cloneable, но не переопределяет clone (), то Java по умолчанию выполнит неглубокое копирование(Если копируемый объект содержит ссылки на другие объекты, то ссылки будут скопированы, дубликаты тех объектов не создаются) Если класс реализует Cloneable и переопределяет clone (), то поведение метода clone () полностью зависит от реализации.

Чтобы сделать объект клонируемым, то необходимо переопределить реализацию метода clone(). Т.к. у Object этот метод является protected.

```java
class Point implements Cloneable
{
 int x;
 int y;

 public Object clone()
 {
  return super.clone();
 }
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