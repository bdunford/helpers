# helpers

Node helper extensions to Object, Array, and String

Requires Nodejs http://nodejs.org


## Installing

__From the Command Line__<br />
npm install git+https://github.com/bdunford/helpers.git

__package.json as a dependency__<br />
add "helpers": "git+https://github.com/bdunford/helpers.git" to dependencies <br />
```json
{
    "name": "your-app",
    "version": "0.0.0",
    "private": true,
    "description": "just another node app",
    "dependencies": {
        "helpers": "git+https://github.com/bdunford/helpers.git"
    }
}

```
__Raw__<br />
```git clone https://github.com/bdunford/helpers```<br />
Be sure to run npm install from with in the __helpers__ directory


## Usage

require helpers in your javascript. Helpers are all extensions methods so there is no need to set a variable.
```javascript
require('helpers');
```

### Object Helpers
__merge__ will merge the contents of the passed object with the object the extension was called on
```javascript
var first = {
    color: "green",
    size: "big"
};

var second = {
    color: "yellow",
    age: 10
};

first.merge(second);
//will return  { color: "yellow", size: "big", age: 10}
```

<br />
__isEqualTo__ returns true if the object values are equal since == will always return false unles comaring the same object
<br />

```javascript
var first = {
    color: "green",
    size: "big"
};

first.isEqualTo({color: "green", size: "big"});
// will return true
```

### Array Helpers
__first__ returns the first item of an array, the default value if passed or null
```javascript
var ar = ["blue","green","red"]
ar.first(); // will return "blue"
[].first("black"); // will return black;
```
<br />
<br />
__where__ returns a new array containing the values that met the passed condition.
<br />
```javascript
var ar = [
    {name: "apple", color: "red"},
    {name: "banana", color: "yellow"},
    {name: "lemon", color: "yellow"},
    {name: "plum", color: "purple"},
    {name: "grape", color: "purple"}
];
ar.where(function(x){return x.color == "purple"});
/* will return [
    {name: "plum", color: "purple"},
    {name: "grape", color: "purple"}
]
```
<br />
__group_by__ will return an an object that contains the resulting arrays described by the values of the groupBy parameter that was passed.
<br />
```javascript
var ar = [
    {name: "apple", color: "red"},
    {name: "banana", color: "yellow"},
    {name: "lemon", color: "yellow"},
    {name: "plum", color: "purple"},
    {name: "grape", color: "purple"}
];

ar.group_by("color");
/* will return {
    red: [
        {name: "apple", color: "red"}
    ],
    purple: [
        {name: "plum", color: "purple"},
        {name: "grape", color: "purple"}
    ],
    yellow: [
        {name: "plum", color: "purple"},
        {name: "grape", color: "purple"}
    ]
}*/
```
__pushUnique__ will only add an object to the array if it does not exit using Object.isEqualTo
```javascript
var ar = [{color: "blue"},{color: "green"},{color: "red"}]
ar.pushUnique({color: "blue"}); // will not add {color: "blue"} to the array.
```
<br />
###String Helpers
__tryJsonParse__ will attempt to parse the string as json to an object using JSON.parse. If the JSON.parse fails tryJsonParse will return false. If returnException = true is passed ```myString.tryJsonParse(true)``` and the parse fails the JSON.parse exception will be returned.
<br />
```javascript
var s = '{"color": "blue"}'
s.tryJsonParse(); // will return {color: "blue"}
```

__capitalize__ returns a new string with the first letter capitalized
<br />
```javascript
var s = "dayton"
s.capitalize(); // will return "Dayton"
```
