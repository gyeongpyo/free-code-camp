## Introduction

* Regular expression: to match parts of strings.
* ```.test()```: takes the regex, applies it to a string, and return ```true``` or ```false``` if your pattern finds something or not.

## Match Literal strings

  ```js
  let testStr = "freeCodeCamp";
  let testRegex = /Code/; // find "Code"
  testRegex.test(testStr);
  // Returns true
  ```

  ```js
  let testStr = "Hello, my name is Kevin.";
  let testRegex = /Kevin/;
  testRegex.test(testStr);
  // Returns true
  let wrongRegex = /kevin/;
  wrongRegex.test(testStr);
  // Returns false
  ```

## Search for multiple patterns using the alternation or OR operator: ```|```

  ```js
  let petString = "James has a pet cat.";
  let petRegex = /dog|cat|bird|fish/; // Change this line
  let result = petRegex.test(petString);
  
  ```

## Ignore case while matching

  * use `i`flag

  ```js
    let myString = "freeCodeCamp";
    let fccRegex = /freecodecamp/i; // Change this line
    let result = fccRegex.test(myString);
  ```

## Extract match

  * `.match()` : extract the actual matches you found

    ```js
    "Hello, World!".match(/Hello/);
    // Returns ["Hello"]
    let ourStr = "Regular expressions";
    let ourRegex = /expressions/;
    ourStr.match(ourRegex);
    // Returns ["expressions"]
    ```

## To search or extract a pattern more than once, use the `g` flag.

  ```js
  let repeatRegex = /Repeat/g;
  testStr.match(repeatRegex);
  // Returns ["Repeat", "Repeat", "Repeat"]
  ```

## Wildcard character

  * `.`: called `dot` and `period`, will match any one character

    ```js
    let humStr = "I'll hum a song";
    let hugStr = "Bear hug";
    let huRegex = /hu./;
    huRegex.test(humStr); // Returns true
    huRegex.test(hugStr); // Returns true
    ```

## character class

  * allow you to define a group of characters you wish to match by placing them inside square(`[]`) bracket.

  ```js
  let bigStr = "big";
  let bagStr = "bag";
  let bugStr = "bug";
  let bogStr = "bog";
  let bgRegex = /b[aiu]g/;
  bigStr.match(bgRegex); // Returns ["big"]
  bagStr.match(bgRegex); // Returns ["bag"]
  bugStr.match(bgRegex); // Returns ["bug"]
  bogStr.match(bgRegex); // Returns null
  ```

## hyphen character: `-`

  ```js
  let catStr = "cat";
  let batStr = "bat";
  let matStr = "mat";
  let bgRegex = /[a-e]at/; // a to e
  catStr.match(bgRegex); // Returns ["cat"]
  batStr.match(bgRegex); // Returns ["bat"]
  matStr.match(bgRegex); // Returns null
  ```

  ```js
  let jennyStr = "Jenny8675309";
  let myRegex = /[a-z0-9]/ig;
  // matches all letters and numbers in jennyStr
  jennyStr.match(myRegex);
  ```

## `+` : match a character that appears one or more times in a row.

  * ex. `/a+/g` would find a single match in "aabc" and return `["aa"]`.

## `*` : matches characters that occur zero or more times

  ```js
  let soccerWord = "gooooooooal!";
  let gPhrase = "gut feeling";
  let oPhrase = "over the moon";
  let goRegex = /go*/;
  soccerWord.match(goRegex); // Returns ["goooooooo"]
  gPhrase.match(goRegex); // Returns ["g"]
  oPhrase.match(goRegex); // Returns null
  ```

## Negated Character

* To create a negated character set, you place a caret character (`^`) after the opening bracket and before the characters you do not want to match.

  ```js
  /* matches all characters that are not a number or a vowel */
  let quoteSample = "3 blind mice.";
  let myRegex = /[^0-9aeiou]/gi; // Change this line
  let result = quoteSample.match(myRegex); // Change this line
  ```

  

## Lazy Matching `?`

* *greedy* match: find the longest possible part of a string that fits the regex pattern and returns it as a match.

  * ex. `/t[a-z]*i/` is applied to `"titanic"`, return `["titani"]`

* *lazy* match: finds the smallest possible part of the string that satisfies the regex pattern.

  * ex. `/t[a-z]?*i/` is applied to `"titanic"`, return `["ti"]`

  > Parsing HTML with regular expressions should be avoided, but pattern matching an HTML string with regular expressions is completely fine.

  ```js
  let text = "<h1>Winter is coming</h1>";
  let myRegex = /<.*?>/; // Change this line
  let result = text.match(myRegex); // return "<h1>"
  ```

## Match Beginning String patterns `^`

* Outside of a character set, the caret is used to search for patterns at the beginning of strings.

```js
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString);
// Returns true
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst);
// Returns false
```

## Match Ending String Patterns `$`

```js
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding);
// Returns true
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding);
// Returns false
```

## Match All Letters and Numbers

* `\w`: shortcut is equal to `[A-Za-z0-9_]`, known as  *shorthand character classes*.

  ```js
  let longHand = /[A-Za-z0-9_]+/;
  let shortHand = /\w+/;
  let numbers = "42";
  let varNames = "important_var";
  longHand.test(numbers); // Returns true
  shortHand.test(numbers); // Returns true
  longHand.test(varNames); // Returns true
  shortHand.test(varNames); // Returns true
  ```

## Match Everything But Letters and Numbers

* `\W`: `[^A-Za-z0-9_]`

  ```js
  let shortHand = /\W/;
  let numbers = "42%";
  let sentence = "Coding!";
  numbers.match(shortHand); // Returns ["%"]
  sentence.match(shortHand); // Returns ["!"]
  ```

## Match All Numbers

* `/d`: `[0-9]`

## Match All Non-Numbers

* `\D`: `[^0-9]`

## Match Whitespace

* `\s`: whitespace
  * `\r`: carriage return;
  * `\t`: tab
  * `\f`: form feed
  * `\n`: new line

## Match Non-Whitespace Characters

* `\S`: Search for non-whitespace
  * `[^\r\t\f\n\v]`

## Specify Upper and Lower Number of Matches

* `{lower, upper}` : *quantity specifiers*

  ```js
  let A4 = "aaaah";
  let A2 = "aah";
  let multipleA = /a{3,5}h/;
  multipleA.test(A4); // Returns true
  multipleA.test(A2); // Returns false
  ```

## Specify Only the Lower Number of Matches

```js
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/; // at least 3
multipleA.test(A4); // Returns true
multipleA.test(A2); // Returns false
multipleA.test(A100); // Returns true
```

## Specify Exact Number of Matches

```js
let A4 = "haaaah";
let A3 = "haaah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleHA = /ha{3}h/;
multipleHA.test(A4); // Returns false
multipleHA.test(A3); // Returns true
multipleHA.test(A100); // Returns false
```

## Check for All or None `?`

* This checks for zero or one of the preceding element. 

  ```js
  let american = "color";
  let british = "colour";
  let rainbowRegex= /colou?r/;
  rainbowRegex.test(american); // Returns true
  rainbowRegex.test(british); // Returns true
  ```

## Positive and Negative Lookahead

* *positive lookahead*: look to make sure the element in the search pattern is there, but won't actually match it. `(?=...)` where the `...` is the required part that is not matched.

* *negative lookahead*: look to make sure the element in the search pattern is not there. `(?!...)` where the `...` is the pattern that you do not want to be there.

  ```js
  let american = "color";
  let british = "colour";
  let rainbowRegex= /colou?r/;
  rainbowRegex.test(american); // Returns true
  rainbowRegex.test(british); // Returns true
  ```

  * A more practical use of lookaheads is to check two or more patterns in one string. Here is a (naively) simple password checker that looks for between 3 and 6 characters and at least one number:
  
  ```js
  let password = "abc123";
  let checkPass = /(?=\w{3,6})(?=\D*\d)/;
  checkPass.test(password); // Returns true
  ```

## Check For Mixed Grouping of Characters

* use `()`

  ```js
  let testStr = "Pumpkin";
  let testRegex = /P(engu|umpk)in/;
  testRegex.test(testStr);
  // Returns true
  ```

## Reuse Patterns Using Capture Groups

* *capture groups*: `()` 

* To specify where that repeat string will appear, you use a `\` and then a number which starts at 1 and increase with each additional capture group.

  ```js
  let repeatStr = "regex regex";
  let repeatRegex = /(\w+)\s\1/;
  repeatRegex.test(repeatStr); // Returns true
  repeatStr.match(repeatRegex); // Returns ["regex regex", "regex"]
  ```

* Using the `.match()` method on a string will return an array with the string it matches, along with its capture group **(the number of capture groups)**.

## Use Capture Groups to Search and Replace

* first parameter: regex pattern, second parameter: string to replace the match

  ```js
  let wrongText = "The sky is silver.";
  let silverRegex = /silver/;
  wrongText.replace(silverRegex, "blue");
  // Returns "The sky is blue."
  ```

  * You can also access capture groups in the replacement string with dollar signs (`$`).

  ```js
  "Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1');
  // Returns "Camp Code"
  ```

  ```js
  let str = "one two three";
  let fixRegex = /(\w+)\s(\w+)\s(\w+)/; // Change this line
  // let fixRegex = /(\w+)\s\1\s\1/; it's not work.
  let replaceText = "$3 $2 $1"; // Change this line
  let result = str.replace(fixRegex, replaceText);
  ```

## Remove Whitespace from Start and End

```js
let hello = "   Hello, World!  ";
let wsRegex = /^\s+|\s+$/g; // Change this line
let result = hello.replace(wsRegex, ""); // Change this line
```

* `String.prototype.trim()` method would work here.