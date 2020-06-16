## AIML ES5

AIML Interpreter written in node.js

AIMLInterpreter is a module that allows you to parse AIML files and to find the correct answer to a given message.<br/>

## Installation

    $ npm install github:nazimboudeffa/aiml-es5

## Running / Building

To run the example:

    $ npm install
    $ node examples/movie.js

## Usage

`new AIMLInterpreter(botAttributes)` create a new interpreter object.

botAttributes is an JSON-Object that

can contain attributes of the bot one wants to use in AIML files, e.g. ({name: "Bot", age:"42"})

This object has a function called `loadAIMLFilesIntoArray(fileArray)` which receives an array of AIML files. This function loads the AIML file into memory.

Furthermore, the object has a function called `findAnswerInLoadedAIMLFiles(clientInput, cb)` which receives a message and a callback. The callback is called when an answer was found.

The callback of `findAnswerInLoadedAIMLFiles` should look like this: `callback(result, wildCardArray, input)`

Result is the answer from the AIML file and wildCardArray stores the values of all wildcardInputs passed previously from the client. The original input which triggered the answer is given back via input

## Example

```javascript
AIMLInterpreter = require('./AIMLInterpreter');
var aimlInterpreter = new AIMLInterpreter({name:'WireInterpreter', age:'42'});
aimlInterpreter.loadAIMLFilesIntoArray(['./test.aiml.xml']);

var callback = function(answer, wildCardArray, input){
    console.log(answer + ' | ' + wildCardArray + ' | ' + input);
};

aimlInterpreter.findAnswerInLoadedAIMLFiles('What is your name?', callback);
aimlInterpreter.findAnswerInLoadedAIMLFiles('My name is Ben.', callback);
aimlInterpreter.findAnswerInLoadedAIMLFiles('What is my name?', callback);
```

## Supported AIML tags

```
<bot name="NAME"/>
<get name="NAME"/>
<set name="NAME">TEXT</set>
<random><li>A</li><li>B</li><li>C</li></random>
<srai>PATTERN TEXT</srai>
<sr/>
<star/>
<that>TEXT</that>
<condition name="NAME" value="VALUE">TEXT</condition>
<condition><li name="NAME" value="VALUE">TEXT</li><li name="NAME" value="VALUE">TEXT</li><li>TEXT</li></condition>
<condition name="NAME"><li value="VALUE">TEXT</li><li value="VALUE">TEXT</li><li>TEXT</li></condition>

<think><set name="NAME">TEXT</set></think>
<anyElement/><random><li>A</li><li>B</li><li>C</li></random><anyElement/>
<random><li><think><set name="NAME">TEXT</set></think></li><li>B</li></random>
<random><li><srai>PATTERN TEXT</srai></li><li>B</li></random>
<condition name="NAME" value="VALUE"><srai>PATTERN TEXT</srai></condition>
<condition><li name="NAME" value="VALUE"><srai>PATTERN TEXT</srai></li><li name="NAME" value="VALUE">TEXT</li></condition>
<condition name="NAME"><li value="VALUE"><srai>PATTERN TEXT</srai></li><li value="VALUE">TEXT</li></condition>
```

## About

This is a fork of [AIML Interpreter](https://github.com/raethlein/AIML.js), I just review the code and make it more ES5
