# JavaScript Style Guide
### version 0.0.1 - ES5

## Table of Contents
1. [Overview](#overview)
1. [Spacing](#spacing)
1. [Declarations](#declarations)
1. [Types](#types)
1. [Constants](#constants)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Properties](#properties)
1. [Comparison Operators & Equality](#comparison-operators--equality)
1. [Blocks](#blocks)
1. [Comments](#comments)
1. [Commas](#commas)
1. [Semicolons](#semicolons)
1. [Constructors](#constructors)
1. [Accessors](#accessors)
1. [Type Casting & Coercion](#type-casting--coercion)
1. [Naming Convention](#naming-convention)
1. [For-in loops](#for-in-loops)
1. [Events](#events)
1. [jQuery](#jquery)
1. [Testing](#testing)

## Overview

The goal of this style guide is to enhance the readability and debugging ability of JavaScript codebases. Good reading in prep for this style guide would be the [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml) and the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md) as both are the basis for this style guide. Inside this guide, you will find links to other style guides. This means that you should follow what they say unless otherwise specificed in this guide.

## Spacing

Indentation should be done with hard tabs (use the tab-character). No soft tabs and no spaces used to indent or align items ever. When indenting an item further down, use a singular tab. Never have a difference of indentation between lines be more than one tab. At most it should be one tab.

```javascript
// bad
function() {
∙∙var name;
}

// bad
function() {
∙var name;
}

// bad
function() {
....var name;
}

//bad; double indentation
function() {
    var myObj = {
            prop1 : "lolololol",
            prop2 : "yayayaya",
    };
}

// good
function() {
    var name;
}

// good
function() {
    var name;
    if (name) {
        callAFunctionWithALotOfParametersThatWontFitOnOneLine(
            parameter1,
            parameter2,
            parameter3,
            parameter4,
            parameter5
        );
    } else {
        // do something else
    }
    var myObj = {
        a: 'b',
        b: 'c',
        c: 'd',
        d: 'e',
        e: 'f'
    };
}
```

Place 1 space before leading brace. Never leave whitespace at the end of a line.

```javascript
// bad
function test(){
    console.log('test');.
}.

// good
function test() {
    console.log('test');
}

// bad
dog.set('attr', {.
    age: '1 year',.
    breed: 'Bernese Mountain Dog'
});

// good
dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog'
});
```

Place 1 space before the opening paranthesis in control statements (if, while, etc.). Place no space before the argument list in function calls and declarations.

```javascript
// bad
if(isJedi) {
    fight ();
}

// good
if (isJedi) {
    fight();
}

// bad
function fight () {
    console.log ('Swooosh!');
}

// good
function fight() {
    console.log('Swooosh!');
}
```

Set off operators with spaces.

```javascript
// bad
var x=y+5;

// good
var x = y + 5;
```

End files with a single newline character.

```javascript
// bad
(function(global) {
    // ...stuff...
})(this);
```

```javascript
// bad but might be unavoidable with a Windows text encoding environment
(function(global) {
    // ...stuff...
})(this);↵
↵
```

```javascript
// good/best
(function(global) {
    // ...stuff...
})(this);↵
```

Use indentation when making long method chains. Use a leading dot, which emphasizes that the line is a method call, not a new statement. Use single indent after first line. Allowed to chain more than one method call per line up to 4 calls. Safe default is one call per line. Use your best judgement.

```javascript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// good
$('#items')
    .find('.selected')
    .highlight()
    .end()
    .find('.open')
    .updateCount();

// good-ish?
$('#items')
    .find('selected').highlight().end()
    .find('.open').updateCount();

// bad
var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
    .call(tron.led);

// good
var leds = stage.selectAll('.led')
    .data(data)
    .enter()
    .append('svg:svg')
    .classed('led', true)
    .attr('width', (radius + margin) * 2)
    .append('svg:g')
    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
    .call(tron.led);
```


## Declarations

Always declare variables with a var unless you're explicitly putting something on the global scope.

```javascript
// bad
aNumber = 123;

// good
var aNumber = 123;

// good
SUPER_SPECIAL_CONSTANT_FOR_ALL_THE_WORLD_TO_SEE = 1;
```

Always declare variables on separate lines with each variable using a var and ending with a semicolon.

```javascript
// bad
var a = 1,
    b = 2,
    c = 3;
    
// bad
var a = 1, b = 2, c = 3;

// good
var a = 1;
var b = 2;
var c = 3;
```

Declare variables as close as possible to when they'll get a value. Try to avoid declaring variables with no value. JavaScript automatically hoists the variables to top of scope anyway. Try to avoid declaring a variable twice (e.g. multiple var i = 0's because of for loops). Ideally, we'd be using let with ES6 but that's not the world we live in.

```javascript
// bad
function() {
    var i;
    var j;
    var thing2;
    var sum;
    var specialMultiplier;
    thing2 = getThatWeirdArray();
    sum = 0;
    if (thing2) {
        specialMultiplier = specialFunc();
        for (i = 0; i < thing2.length; i++) {
            for (j = 0; j < thing2.length; j++) {
                sum += thing2[i][j] * specialMultiplier;
            }
        }
    }
    return sum;
}

// good
function() {
    var thing2 = getThatWeirdArray();
    var sum = 0;
    if (thing2) {
        var specialMultiplier = specialFunc();
        for (var i = 0; i < thing2.length; i++) {
            for (var j = 0; j < thing2.length; j++) {
                sum += thing2[i][j] * specialMultiplier;
            }
        }
    }
    return sum;
}

// good
function() {
    var thing2 = getThatWeirdArray();
    var thing3 = getAnotherThing();
    var sum = 0;
    var i;
    var j;
    if (thing2) {
        var specialMultiplier = specialFunc();
        for (i = 0; i < thing2.length; i++) {
            for (j = 0; j < thing2.length; j++) {
                sum += thing2[i][j] * specialMultiplier;
            }
        }
    }
    if (thing3) {
        for (i = 0; i < thing3.length; i++) {
            for (j = 0; j < thing3.length; j++) {
                sum += thing2[i][j];
            }
        }
    }
    return sum;
}
```

## Types

[Airbnb - Types](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#types)

## Constants

[Google - Constants](https://google.github.io/styleguide/javascriptguide.xml?showone=Constants#Constants)

## Objects

[Airbnb - Objects](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#objects)

There is a specific declaration style that we use for objects. If the declaration is short (less than 4 properties and fits on a 80 character line), go for it. If it doesn't, each property gets its own line. No whitespace after property name, single whitespace after colon. Single line declarations should have a space after the comma. Multiline declarations should have the first bracket on the variable assignment line and the closing bracket on its own line with the semicolon at the same indentation level as the variable assignment (similar to if, while, etc.). Properties should be indented one level. Properties should also be alphabetically declared. Avoid declaring functions inline for properties. If it must be done, all non-function declaring properties go first (alphabetically) and then all function declaring properties go last (alphabetically).
```javascript
// bad
var myObj = {thing1:'rara',thing3:'yadda', thing2:'blahblh',thing4:'whaaaaaaaaaaaaaaaaaaaaaaaaaat'};

// good
var myObj = {
    thing1: 'rara',
    thing2: 'blahblh',
    thing3: 'yadda',
    thing4: 'whaaaaaaaaaaaaaaaaaaaaaaaaaat'
};

// good, spacing doesn't matter too much. Although, please be consistent. Prefer first line style.
var myObj = {howdy: 'partner', whaaaat: 'isthisfeeling'};
var myObj = { howdy: 'partner', whaaat: 'isthisfeeling' };

// bad
var myObj = {
    a: function(arg1) {
        //do stuff
    },
    b: 'willyouseeme',
    c: function(arg1, arg2) {
        //do stuff
    },
    d: 'hereIam!',
    e: 'hereisanother!',
    f: function() {
        //do stuff
    }
};

// better
var myObj = {
    b: 'willyouseeme',
    d: 'hereIam!',
    e: 'hereisanother!',
    a: function(arg1) {
        //do stuff
    },
    c: function(arg1, arg2) {
        //do stuff
    },
    f: function() {
        //do stuff
    }
};

// best
function aFunction(arg1) {
    //do stuff
}

function cFunction(arg1, arg2) {
    //do stuff
}

function fFunction() {
    //do stuff
}

var myObj = {
    a: aFunction,
    b: 'willyouseeme',
    c: cFunction,
    d: 'hereIam!',
    e: 'hereisanother!',
    f: fFunction
};
```

## Arrays

[Airbnb - Arrays](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#arrays)

## Strings

[Airbnb - Strings](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#strings)

## Functions

[Airbnb - Functions](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#functions)

## Properties

[Airbnb - Properties](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#properties)

## Comparison Operators & Equality

[Airbnb - Comparison Operators & Equality](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#comparison-operators--equality)

## Blocks

[Airbnb - Blocks](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#blocks)

## Comments

[Airbnb - Comments](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#comments)  
[Google - Comments](https://google.github.io/styleguide/javascriptguide.xml#Comments)

Use JSDoc.

## Commas

[Airbnb - Commas](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#commas)

## Semicolons

Yes.
[Airbnb - Semicolons](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#semicolons)  
[Google - Semicolons](https://google.github.io/styleguide/javascriptguide.xml?showone=Semicolons#Semicolons)

## Constructors

[Airbnb - Constructors](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#constructors)

## Accessors

[Airbnb - Accessors](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#accessors)

## Type Casting & Coercion

[Airbnb - Type Casting & Coercion](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#type-casting--coercion)

## Naming Convention

[Airbnb - Naming Convention](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#naming-conventions)

Constants should be all capital letters and words separated by underscores. Include documentation for each constant.

```javascript
// bad
var SUPERMANISBETTERTHANBATMAN = false;

// good
// Superman is never better than batman. NEVER!
var SUPERMAN_IS_BETTER_THAN_BATMAN = false;
```

## For-in loops

Be careful and avoid these unless you know what you're doing.  
[Google - For-in loop](https://google.github.io/styleguide/javascriptguide.xml?showone=for-in_loop#for-in_loop)

## Events

[Airbnb - Events](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#events)

## jQuery

[Airbnb - jQuery](https://github.com/airbnb/javascript/tree/es5-deprecated/es5/README.md#jquery)

Prefer using constants for CSS Selectors. Although, this is not a hard rule.
```javascript
// okay
$('.my-lovely-thing').attr('title', 'whaaat!');

// better
var MY_LOVELY_THING_SELECTOR = '.my-lovely-thing';
// ...
$(MY_LOVELY_THING_SELECTOR).attr('title', 'whaaat!');
```


## Testing

Please.

