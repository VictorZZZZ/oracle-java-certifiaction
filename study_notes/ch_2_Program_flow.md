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