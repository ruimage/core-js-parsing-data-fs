# Парсинг данных: из CSV в JS в CSV

## Введение

Когда мы запускаем наши приложения, создаются объекты JS, которые существуют в памяти нашего компьютера. Эти объекты хранят какую-либо информацию. Состояние «нахождения в памяти» теряется, когда наше приложение заканчивает работу, поэтому, если мы хотим сохранить информацию из приложения, то нам нужно записать его где-нибудь.

В дополнение к сохранению информации из наших программ для себя, мы иногда хотим поделиться этой информацией с другими системами или программами. Для этого, помимо простого сохранения данных, нам нужно сохранить их в формате, который совместим с этими другими системами, и который легко переносится.

Существует общий подход к сохранению информации в различных форматах - это преобразование информации в текст. XML, JSON, CSV и YAML - все это примеры текстовых форматов для обмена данными.

В этой задаче мы будем использовать [CSV][wikipedia csv] в качестве нашего формата для хранения данных. Мы будем представлять людей в JS в качестве экземпляров класса `Person`. Мы будем создавать объекты `Person`  из данных в CSV-файле, а также сохранять состояние объектов JS `Person` в CSV-файле.

### JS's CSV библиотека

Мы можем воспользоваться библиотекой `json2csv` для того, чтобы записать наши js объекты в csv-формате. 

```js
const json2csv = require('json2csv').parse;
```

## Releases
### Release 0: Представлять людей как объекты JS
Начнем с создания класса `Person`; в нашей программе js каждый экземпляр этого класса будет представлять человека. Наш класс должен быть предназначен для представления данных, найденных в файле `people.csv`. Другими словами, экземпляр класса `Person` должен иметь имя, фамилию и т. д.

Нам нужно будет написать тесты для нашего класса. Какое поведение должно быть у нашего класса `Person`? Для начала давайте убедимся, что мы можем создать экземпляр класса со всеми нужными аттрибутами: имя, фамилия и т.д.


### Release 1: Парсинг из CSV в JS

Теперь у нас есть пользовательский класс js, предназначенный для представления человека. Чтобы создать объект `Person`, нам нужно предоставить некоторые данные: имя, фамилию и т.д. Для создания объекта не имеет значения, откуда берутся эти данные. Данные могут предоставляться через пользовательский интерфейс, который может быть на веб-странице. Но в этой задаче данные поступают к нам из файла CSV.

Мы построим модуль `PersonParser`, ответственный за анализ текста в файле и получение объектов `Person` из него. Напишите метод `.parse`. Этот метод должен преобразовывать каждую строку из csv-файла в объект `Person`  и возвращать массив из этих объектов.


### Release 2: соответствующие типы данных в JS
В нашем CSV-файле все представлено в текстовом формате. Это означает, что вся информация из файла приходит в нашу программу в виде строки. Иногда это уместно. Названия, номера телефонов и адреса электронной почты легко представляются в виде строк. В других случаях может оказаться полезным преобразовать текст CSV в объект другого типа.

В `people.csv` дата и время рождения человека сохраняются в поле `born_at`. В CSV-файле это строка в формате `YYYY-MM-DD HH:MM:SS`. Эта строка представляет дату и время, js в свою очередь предоставляет нам такой класс, как [Date][], специально созданный для представления даты и времени.

Когда мы создаем объекты `Person`  из нашего CSV-файла, убедитесь, что их свойства `bornAt` являются объектами `Date`, а не строками. Также, возможно нам понадобится метод [Date.parse][].


### Release 3: Работа с объектами JS (Опционально)
![анимация](readme-assets/runner_animation.gif)

*Рисунок 1*. Фильтрация объектов js, созданных из файла CSV.

Одним из преимуществ загрузки данных из файла CSV в объекты js является то, что нам становится проще «фильтровать» коллекцию людей или манипулировать их атрибутами. Например, мы могли бы отсортировать людей по имени. Или мы можем обновить номер телефона человека.

Мы хотим, чтобы наша программа позволяла пользователям «фильтровать» людей, используя разные команды: фильтрацию людей по определенному региональному коду, по определенной фамилии, адресу электронной почты из определенного домена или родившихся после определенного года. Когда мы закончим эту процедуру, программа должна работать аналогично примеру на Рисунке 1.

Начните с разработки функции поиска людей по коду региона. Запустите программу и следуйте сообщениям об ошибках. После того, как пользователи смогут искать людей по региональному коду, выполните три другие функции: поиск по фамилии, по электронной почте и по году рождения. Затем придумайте и добавьте еще один параметр для поиска.

### Release 4: Сохранение информации из js в CSV
```js
let jane = new Person(...)
let john = new Person(...)

PersonWriter.write('friends.csv', [jane, john])
```

*Рисунок 1*. Создание людей в js и сохранение данных о них в CSV-файле.

Мы научились парсить данные из CSV в js-объекты, и теперь мы можем использовать их в наших программах. Теперь мы будем работать с объектами js и сохранить данные о них в CSV-файле. Для этого мы создадим модуль с классом `PeopleWriter` с методом `.write`. Мы можем создать массив объектов `People`, а затем записать их в файл. (см. Рисунок 1)


*Примечание:* Когда мы читаем и записываем файл, мы можем выбрать режим (например, `"r"` для чтения и `"w"` для записи). Режимы CSV такие же, как [режимы, доступные для файла] [режимы файла js].


### Release 5: Сбор и сохранение информации (Опционально)
Теперь, когда мы можем записать данные в CSV, давайте напишем скрипт, который позволит нам создать адресную книгу CSV на основе пользовательского ввода. Мы вводим имена людей, номера телефонов и т.д., а затем сохраняем данные в файл CSV. Давайте напишем такой файл `runner.js`, чтобы при его запуске нам предлагалось ввести информацию. Мы вводим данные как можно большего количества людей. И затем, как только мы закончим делать записи, данные, которые мы ввели, будут записаны в файл CSV.



## Заключение
Общая цель этой задачи - научиться манипулировать объектами js и CSV как частью одного приложения. Все данные, которые нам нужны для представления людей, были сохранены в CSV-файле, но CSV-файл был просто текстовым и, соответственно, был лишен индивидуального поведения (например, возврат имени). Создав объекты js на основе данных, мы смогли создать объекты, поведение которых соответствовало потребностям нашего приложения. Это общая схема разработки программного обеспечения: нужно изменить представление данных из формата A в формат B, чтобы упростить работу с X.

[Date]: https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Date
[Date.parse()]: https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Date/parse
[режимы файла js]: https://kuroikaze85.wordpress.com/2010/03/19/read-and-write-files-nodejs/
[wikipedia csv]: https://en.wikipedia.org/wiki/Comma-separated_values
[wikipedia lazy initialization]: https://en.wikipedia.org/wiki/Lazy_initialization
[wikipedia memoization]: https://en.wikipedia.org/wiki/Memoization


__________________________________________________________________________________


## Summary
When we run our applications, JS objects are created that exist in our computer's memory.  These objects have state, or information, associated with them.  In-memory state is lost when our application ends, so if we want to save this state, we need to record it somewhere.

In addition to saving the state of our programs for ourselves, we sometimes want to share this information with other systems or programs.  To accomplish this, in addition to merely saving the data, we need to save it in a format that is both compatible with these other systems and easily transfered.

One common approach to saving state in an exchangeable format is to translate the information to text.  XML, JSON, CSV, and YAML are all examples of text-based data exchange formats.

In this challenge, we'll use [CSV][wikipedia csv] as our format for storing data.  We'll be representing people in JS as instances of the class `Person`.  We'll both build `Person` objects from data in a CSV file and also save the state of JS `Person` objects in a CSV file.


### JS's CSV Library
JS provides a library for working with CSV files (see [JS docs][JS docs csv]).  It is part of JS's Standard Library, so we always have access to it.  However, it's not a part of JS's Core, so it's not automatically loaded for us when our programs run.  We need to explicitly require it.  This is done for us at the top of the `person_parser.rb` file.

We'll use this CSV library to both read and write CSV files.  The library provides the [`CSV.foreach`][docs foreach] method as the "primary interface for reading CSV files" and the [`CSV.open`][docs open] method as the "primary interface for writing a CSV file."

When we read a CSV file, the default behavior for `CSV.foreach` is to convert each row in the file to an array of strings.  However, we can change that behavior by specifying different options.  For example, specifying that our CSV file contains a header row changes the data structure used to represent each row from an array to a [`CSV::Row`][JS docs csv row] object.  For an overview of these options, read the blog post *[Parsing CSV with JS][technical pickles csv]*.

*Note:*  The blog post explains these options using the method `CSV.new`, but they are the same when using `CSV.foreach`.


## Releases
### Release 0: Represent People as JS Objects
We'll begin by creating a `Person` class; in our JS program, each instance of this class will represent a person.  Our person class should be designed to represent the data found in the file `people.csv`.  In other words, an instance of our `Person` class should have a first name, a last name, etc.

We'll need to write tests for our class.  What behaviors does our `Person` class need?  To start, let's ensure that we can ask an instance of the class for each of its attributes:  first name, last name, etc.


### Release 1: Parsing from CSV to JS
We now have a custom JS class designed to represent a person.  In order to build a `Person` object, we need to supply some data:  the first name, last name, etc.  It doesn't matter where that data comes from.  The data could be supplied through a user interface, it could exist on a webpage, anywhere.  In this challenge, the data comes from a CSV file.

We'll build a `PersonParser` module whose responsibility is to parse the text in a file into `Person` objects.  Write out the method body for the `.parse` method.  This method should convert each line in the file into a `Person` object and return those objects in an array.

We need to test the behavior of our `PersonParser` module.  Given a CSV file with specific data in it, when we tell our parser to parse that file, what do we expect to be returned?


### Release 2: Appropriate Data Types in JS
In our CSV file everything is text.  That means everything comes into our JS application as a string.  Sometimes this is appropriate.  Names, phone numbers, and e-mail addresses are represented well as strings.  In other cases, it can be beneficial to convert the CSV text into a different type of object.

In `people.csv` the date and time a person was born is saved in the `born_at` field.  In the CSV file this is a string formatted `YYYY-MM-DD HH:MM:SS`.  While this string does represent a date and time, JS provides classes like [DateTime][] specifically built for representing dates and times.  
 
When we create `Person` objects from our CSV file, ensure that their `born_at` attributes are `DateTime` objects, not strings. We might want to check out the [DateTime.parse][] method.

*Note:*  Like JS's CSV library, the `DateTime` class is not automatically loaded when our programs run.  We need to require it:  `require 'date'`.  


### Release 3: Working with the JS Objects
![runner animation](readme-assets/runner_animation.gif)  
*Figure 1*.  Filtering the JS objects created from the CSV file.

One of the advantages of loading the data from the CSV file into JS objects is that it becomes easier for us to filter the collection of people or to manipulate their attributes.  For example, we could order the people by first name.  Or, we could update a person's phone number.

Read through `runner.rb`. We want our program to allow users to filter people using different commands: filtering people from a specific area code, with a specific last name, with an e-mail address from a specific domain, or born after a given year.  When we're done, the program should operate similar to the example in Figure 1.

Begin by completing the feature for searching for people by area code.  Run the program and follow the error messages (Hint:  we'll be adding to our `Person` class).  Once users can search for people by area code, implement the other three features:  searching by last name, by e-mail domain, and by birth year.  Then think up and add another feature of our own.


### Release 4: Saving JS State to CSV
```JS
jane = Person.new(...)
john = Person.new(...)

PersonWriter.write('friends.csv', [jane, john])
```
*Figure 1*.  Creating people in JS and saving their data to a CSV file.

We can parse CSV data into JS objects which we can use in our programs.  Now we're going to take JS objects and save their state to a CSV file.  To do this, we'll build a `PeopleWriter` module with a `.write` method.  We can create a collection of `People` objects and then tell the writer to write them to a file.  (see Figure 1)

We do not need to write tests for the writing behavior.

*Note:* When we read and write to a file, we can choose a mode (like `"r"` for read and `"w"` for write).  The CSV modes are the same as the [modes available for File][JS file modes].


### Release 5: Collect and Save Information
Now that we can write data to CSV, let's write a script that will allow us to create a CSV address book based on user input.  We'll enter people's names, phone numbers, etc. and then save the data to a CSV file.  Let's modify the runner file so that when it runs, we're prompted to enter information.  We'll enter the data for as many people as we want.  And then, once we're done making entries, the data we've entered will be written to a CSV file.


## Conclusion
The overall goal of this challenge is to learn to manipulate JS objects and CSV as part of a single application. All the data we needed to represent people was held in a CSV file, but the CSV file is just text and lacks person-like behavior (e.g., returning a name).  By creating JS objects based on the data, we were able to create objects whose behaviors matched the needs of our application. This is a common pattern in software engineering: change the representation of data from Format A to Format B to make it easier to do X with it.

