# Data parsing: CSV into JS and back into CSV

## Introduction

When you run your applications, JS objects are created and stored in memory on your computer. The "in-memory" state is lost when the application finishes running, so if you want to save information from the application, you need to write it down somewhere.

In addition to saving information from your applications for your needs, you sometimes have to share that information with other systems or programs. To do that, except just saving the data, you need to save it in a format that is compatible with those other systems, and that is easily portable.

A common approach to saving information in different formats is to convert the information to text. XML, JSON, CSV and YAML are all examples of text formats for data exchange. We recommend that you familiarize yourself with all of these formats, they will be useful to you in the future.
In this task you are going to use [CSV][wikipedia csv] as a format for storing data. You have to represent people in JS as instances of the class `Person`. That means, you have to pull the data from the CSV file, and then create a `Person` object based on each row of data from the file. And finally, you need to save the objects related to the class `Person` into a new CSV file.


## Releases
### Release 0. People as JS objects
Start by creating the class `Person`. Your class should be designed to represent the data found in `people.csv` file. In other words, an instance of `Person` class must have a name, surname, etc.

You need to write tests to make sure the `Person` class functions correctly.


### Release 1. Парсинг из CSV в JS

Now we have a class designed to represent a person. To create a Person object, you need to provide some data: first name, last name, etc. It doesn't matter where the data comes from to create the object. The data can be provided through a user interface, which might be on a web page. But in this task, the data comes from a CSV file.

Now write a `PerfectParser` class responsible for parsing the text in the file and generating `Person` objects from its data. Implement a method `.parse()`. This method should convert each line from the csv file into an object of Person class and return an array of these objects.

```js
const parser = new PerfectParser();
const people = parser.parse('people.csv');
console.log(people);
// => [Person {...}, Person {...}, Person {...}]
console.log(people[0] instanceof Person);
// => true

```
*Figure 1*. A call of method `parse`, which returns an array of `Person` objects based on data from the CSV file.


### Release 2. Corresponding data types in JS
In your CSV file, information is stored in text format. This means that all the information from the file comes into the program as a string. Sometimes this is correct. Names, phone numbers, and email addresses are easily represented as strings. In other cases, it may be useful to transform the CSV text into more appropriate type.

In `people.csv` the date and time a person was born is saved in the field `bornAt`. In CSV file, this is a string in format `YYYYY-MM-DD HH:MM:SS`. This string represents date and time, but JS provides us with such a tool like [Date][Date], specifically created to represent the date and time.

When you create `Person` objects from a CSV file, make the `bornAt` property the `Date` "type". Also, you may need the [Date.parse()][Date.parse()] method or other methods related to [Date][Date].

### Release 3. Saving information from JS to CSV

>**JavaScript's npm modules**
You can use a library (for example, an npm module `json2csv`) to write js objects to csv. This approach is easier and maybe more correct in some cases. However, you should understand how to solve this problem without third-party npm modules. `const json2csv = require('json2csv').parse;`


```js
let jane = new Person(...)
let john = new Person(...)

PerfectParser.write('friends.csv', [jane, john])
```

*Figure 2*. Creating people in JS and saving their data in a CSV file.

You have learned how to parse data from CSV to js, convert string data to objects, and now you can use this data in your programs. Suppose you have got the data from the file, worked with it, edited it a bit, added something, deleted something, and now you would like to save everything to a new csv-file. Now you have to convert your array of `Person` objects to the right format (string, csv). You already have the method `.write()` of `PerfectParser` prepared for this release. Fill it up with your beautiful code!

## Conclusion.
The overall goal of this task is to learn how to manipulate js and CSV objects as a part of the same application. All of the data needed to represent people was stored in a CSV file, but the CSV file was just a text file. By creating js objects based on the data, we were able to create objects whose behavior matched the needs of our application. This is a common software development scheme: we need to change the representation of data from format A to format B in order to make it easier to work with X.


Translated with www.DeepL.com/Translator (free version)
[Date]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Date
[Date.parse()]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Date/parse
[wikipedia csv]: https://en.wikipedia.org/wiki/Comma-separated_values
[wikipedia lazy initialization]: https://en.wikipedia.org/wiki/Lazy_initialization
[wikipedia memoization]: https://en.wikipedia.org/wiki/Memoization
