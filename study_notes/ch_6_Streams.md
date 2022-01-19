## Часть 6. Working with Streams and Lambda Expressions

`Streams` делятся на источник(`source`), промежуточные операции(`intermediate operation`), терминальные операции(`terminal operation`)
**Проемужточные операции**:
```java
	filter()
	map()
	flatMap()
	distinct()  
	sorted()  
	peek()  
	limit()  
	skip()
```
`peek` - промежуточная операция(альтернатива терминально  `foreach`)
На странице Javadoc peek () говорится: «Этот метод существует в основном для поддержки отладки, когда вы хотите видеть, как элементы проходят через определенную точку в Стриме».

**Терминальные операции**:
```java
	toArray()
	collect()
	count()
	reduce() 
	forEach() 
	forEachOrdered() 
	min()
	max()
	anyMatch()
	allMatch() 
	noneMatch()
	findAny()
	findFirst()
```

`Stream<?>` - можно выполнить только один раз. Например такой метод выполнится на второй строке, но на третьей строке выдаст
`IllegalStateException: stream has already been operated upon or closed`
```java
Stream<Integer> integerStream = Stream.of(1, 2, 3);  
integerStream.forEach(System.out::println);  
integerStream.forEach(System.out::println);
```

Лямбда выражение - сокращённая форма записи функционального интерфейса.
Функциональный интерфейс - интерфейс с одним методом.

Базовые Функциональные интерфейсы:
`Supplier` - Функциональный интерфейс, который не принимает никаких параметров, но возвращает некоторый объект типа T
```java
@FunctionalInterface
public interface Supplier<T> {
   T get();
}
```

`Consumer` - функциональный интерфейс, который на вход принимает объект типа T а на выход ничего не отдаёт
```java
@FunctionalInterface
public interface Consumer<T> {
   void accept(T t);
}
```

`Predicate` - функ. интерфейс, для проверки некоторого условия. Возвращает **примитивный** тип boolean
```java
@FunctionalInterface
public interface Predicate<T> {
   boolean test(T t);
}
```

`Function` — этот функциональный интерфейс принимает аргумент T и приводит его к объекту типа R, который и возвращается как результат:
```java
@FunctionalInterface
public interface Function<T, R> {
   R apply(T t);
}
```

`UnaryOperator` — функциональный интерфейс, принимает в качестве параметра объект типа T, выполняет над ним некоторые операции и возвращает результат операций в виде объекта того же типа T:

```java
@FunctionalInterface
public interface UnaryOperator<T> {
   T apply(T t);
}
```


```BiFunction``` ялвяется **functional interface**, представляющим оператор, который принимает два входных значения и возвращает одно значение.
```java
@FunctionalInterface
public interface BiFunction<T, U, R> {
    R apply(T t, U u);
 
    default <V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t, U u) -> after.apply(apply(t, u));
    }
}
```