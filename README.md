<a href="https://github.com/walmartlabs/blammo"><img src="https://raw.github.com/walmartlabs/blammo/master/images/from.png" align="right" /></a>
![hoek Logo](/images/hoek.png)

General purpose node utilities

[![Build Status](https://secure.travis-ci.org/walmartlabs/hoek.png)](http://travis-ci.org/walmartlabs/hoek)

# Table of Contents

* [Introduction](#introduction "Introduction")
* [Object](#object "Object")
  * [clone](#clone "clone")
  * [merge](#merge "merge")
  * [applyToDefaults](#applyToDefaults "applyToDefaults")
  * [unique](#unique "unique")
  * [mapToObject](#mapToObject "mapToObject")
  * [intersect](#intersect "intersect")
  * [flatten](#flatten "flatten")
  * [removeKeys](#removeKeys "removeKeys")
  * [inheritAsync](#inheritAsync "inheritAsync")
  * [rename](#rename "rename")
* [Timer](#timer "Timer")


# Introduction

The *Hoek* general purpose node utilities library is used to aid in a variety of manners. It comes with useful methods for Ararys (clone, merge, applyToDefaults), Objects (removeKeys, copy), Asserting and more. 

For example, to use Hoek to set configuration with default options:
```javascript
var Hoek = require('hoek');

var default = {url : "www.github.com", port : "8000", debug : true}

var config = Hoek.applyToDefaults(default, {port : "3000", admin : true});

// In this case, config would be { url: 'www.github.com', port: '3000', debug: true, admin: true }
```

Under each of the sections (such as Array), there are subsections which correspond to Hoek methods. Each subsection will explain how to use the corresponding method. In each js excerpt below, the var Hoek = require('hoek') is omitted for brevity.

## Object

Hoek provides several helpful methods for objects and arrays.

### clone(obj)

This method is used to clone an object or an array. A *deep copy* is made (duplicates everything, including values that are objects). 

```javascript

var nestedObj = {
        w: /^something$/ig,
        x: {
            a: [1, 2, 3],
            b: 123456,
            c: new Date()
        },
        y: 'y',
        z: new Date()
    };

var copy = Hoek.clone(nestedObj);

copy.x.b = 100;

console.log(copy.y)        // results in 'y'
console.log(nestedObj.x.b) // results in 123456
console.log(copy.x.b)      // results in 100
```

### merge(target, source, isNullOverride, isMergeArrays)
isNullOverride, isMergeArrays default to true

Merge all the properties of source into target, source wins in conflic, and by default null and undefined from source are applied


```javascript

var target = {a: 1, b : 2}
var source = {a: 0, c: 5}
var source2 = {a: null, c: 5}

var targetArray = [1, 2, 3];
var sourceArray = [4, 5];

var newTarget = Hoek.merge(target, source);     // results in {a: 0, b: 2, c: 5}
newTarget = Hoek.merge(target, source2);        // results in {a: null, b: 2, c: 5}
newTarget = Hoek.merge(target, source2, false); // results in {a: 1, b:2, c: 5}

newTarget = Hoek.merge(target, source)              // results in [1, 2, 3, 4, 5]
newTarget = Hoek.merge(target, source, true, false) // results in [4, 5]




```

### applyToDefaults(defaults,options)

Apply options to a copy of the defaults

```javascript

var defaults = {host: "localhost", port: 8000};
var options = {port: 8080};

var config = Hoek.applyToDefaults(defaults, options); // results in {host: "localhost", port: 8080};


```

### unique(array,key)

Remove duplicate items from Array

### mapToObject(array,key)

### intersect(array1,array2)

### flatten(array,target)

### removeKeys(object,keys)


