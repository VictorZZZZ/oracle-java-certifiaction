# Chapter 12. Localization
Локали обычно представлены сокращением языка, страны и варианта, разделенными подчеркиванием.
-   de (German)
-   it_CH (Italian, Switzerland)
-   en_US_UNIX (United State, UNIX platform)

We have already learned that **_Locale_ consists of language code, country code, and variant. There are two more possible fields to set: script and extensions**.

Let's have a look through a list of fields and see what the rules are:

-   **Language** can be an _ISO 639 alpha-2 or alpha-3_ code or registered language subtag.
-   **Region** (Country) is _ISO 3166 alpha-2_ country code or _UN numeric-3_ area code.
-   **Variant** is a case-sensitive value or set of values specifying a variation of a _Locale_.
-   **Script** must be a valid _ISO 15924 alpha-4_ code.
-   **Extensions** is a map which consists of single character keys and _String_ values.

The [IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) contains possible values for _language_, _region_, _variant_ and _script_.

There is no list of possible _extension_ values, but the values must be well-formed [_BCP-47_](https://docs.oracle.com/javase/tutorial/i18n/locale/extensions.html) subtags. The keys and values are always converted to lower case.

### **Default Locale**[](https://www.baeldung.com/java-8-localization#7-default-locale)

### [](https://www.baeldung.com/java-8-localization#7-default-locale)

While working with localization, we might need to know what the default _Locale_ on our _JVM_ instance is. Fortunately, there's a simple way to do that:

```java
Locale defaultLocale = Locale.getDefault();
```

Also, we can specify a default _Locale_ by calling a similar setter method:

```java
Locale.setDefault(Locale.CANADA_FRENCH);
```

It's especially relevant when we'd like to create _JUnit_ tests that don't depend on a _JVM_ instance.

### Resource Bundles
Важнейшей частью интернационализации JVM является механизм Resource Bundle.
Назначение ResourceBundle - предоставить приложению локализованные сообщения / описания, которые могут быть перенесены в отдельные файлы.

Первое, что мы должны знать, это то, что все файлы в одном пакете ресурсов должны находиться в одном пакете / каталоге и иметь общее базовое имя. Они могут иметь суффиксы, зависящие от локали, обозначающие язык, страну или платформу, разделенные символом подчеркивания.

Важно, чтобы мы могли добавить код страны, если код языка уже есть, или платформу, если есть коды языка и страны.

Давайте посмотрим на примеры имен файлов:

ExampleResource  
ExampleResource_en  
ExampleResource_en_US  
ExampleResource_en_US_UNIX

Файл по умолчанию для каждого пакета данных всегда один без суффиксов - ExampleResource. Поскольку существует два подкласса ResourceBundle: PropertyResourceBundle и ListResourceBundle, мы можем взаимозаменяемо хранить данные в файлах свойств, а также в файлах Java.

Каждый файл должен иметь зависящее от локали имя и правильное расширение файла, например ExampleResource_en_US.properties или Example_en.java.

#### PropertyFiles
Файлы свойств представлены PropertyResourceBundle. Они хранят данные в виде пар ключ-значение с учетом регистра.

```java
# Buttons 
continueButton продолжить  
cancelButton = отменить  
  
! Этикетки  
helloLabel: привет  
```

Как мы видим, существует три разных стиля определения пар 'ключ-значение'.  
Стоит знать, что мы также можем помещать комментарии в файлы свойств. Комментарии всегда начинаются с символа `#` или `!`.

#### Файлы Java - ListResourceBundle
Прежде всего, чтобы хранить данные, относящиеся к нашему языку, нам нужно создать класс, который расширяет ListResourceBundle и переопределяет метод getContents (). Соглашение об именах классов такое же, как и для файлов свойств.   
Для каждого Locale нам нужно создать отдельный класс Java.

Вот образец класса:

```java
public class ExampleResource_pl_PL extends ListResourceBundle {

    @Override
    protected Object[][] getContents() {
        return new Object[][] {
          {"currency", "polish zloty"},
          {"toUsdRate", new BigDecimal("3.401")},
          {"cities", new String[] { "Warsaw", "Cracow" }} 
        };
    }
}
```

У файлов Java есть одно важное преимущество перед файлами свойств, которое заключается в том, что они могут содержать любой объект, который мы хотим, а не только строки.

С другой стороны, каждая модификация или введение нового java-класса, зависящего от локали, требует перекомпиляции приложения, тогда как файлы свойств могут быть расширены без каких-либо дополнительных усилий.

#### Использование ResourceBundles
```java
Locale locale = new Locale("pl", "PL");
ResourceBundle exampleBundle = ResourceBundle.getBundle("package.ExampleResource", locale);

assertEquals(exampleBundle.getString("currency"), "polish zloty");
assertEquals(exampleBundle.getObject("toUsdRate"), new BigDecimal("3.401")); 
assertArrayEquals(exampleBundle.getStringArray("cities"), new String[]{"Warsaw", "Cracow"});
```

#### Наследование
пары 'ключ-значение', включенные в менее конкретные файлы, наследуются теми, которые находятся выше в дереве наследования.
```plaintext
#resource.properties
cancelButton = cancel

#resource_pl.properties
continueButton = dalej

#resource_pl_PL.properties
backButton = cofnij
```