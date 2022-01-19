## Часть 2. CONTROLLING PROGRAM FLOW. LOOPS. IF/ELSE. SWITCH.
- `switch` работает с  `byte`, `short`, `char`, и `int` примитивными типами данных. Enum, `String` классом, и с врапперами: `Character`,`Byte`,`Short`, `Integer`
  **!!!ВНИМАНИЕ!!!!** - он не поддерживает типы примитив `double` и обертку `Double`, а так же `boolean` и `Boolean`
  Также в некоторых случая он разрешает `var` если он резолвится как тип из указанных выше!
- `switch` оператор _default_ может находиться на любом месте. Как первым, так и последним
- В `switch` значение в case должно быть **constant**, a **literal value**, или **final** перменной.
-  `switch` не поддерживает несколько вариантов в одном case.
- Цикл do while можно записать как
```java
	loop:
	do{
		//some actions
		break loop;
	} while(true)
```
- `for`  если более чем одна переменная инициализируется, то они должны разделяться запятой. также возможно их обоих изменять в третьей секции.
 ```java
 for(int i=0, j=1; i<x && j<y; i++, j++){
 	//some actions
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