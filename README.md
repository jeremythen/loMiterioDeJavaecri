# loMiterioDeJavaecri

## String startsWith method weirdness:

```javascript
"David".startsWith(); // false
"David".startsWith(""); // true
"David".startsWith("D"); // true
```

## String replace method weirdness

```javascript
"David".replace("", "X"); // XDavid
```

## String split and join method weirdness

```javascript
"David".split(); // Array ["David"]
"David".split(""); // Array(5) ["D", "a", "v", "i", "d"]

const test = "David".split("");

test.join(); // "D,a,v,i,d"
test.join(""); // "David"
```

## Prototype indirect immutability

JavaScript supports Prototype Inheritance. We can create an object with default properties and functions to be used a prototype for other objects.
When we try to access a property on an object, and that property is not present in object, the JavaScript engine tries to find it in any of the prototypes that object has and if it finds it it uses it.


```javascript

const obj1 = {val: 1};
const obj2 = Object.create(obj1); // Creates a new object making obj1 it's prototype

console.log(obj1); // {val: 1}
console.log(obj2); // {}

console.log(obj1.val); // 1
console.log(obj2.val); // 1

obj1.hasOwnProperty('a'); // returns true because the val property is declared in obj1 object.
obj2.hasOwnProperty('a'); // returns false because the val property is not declared on obj2. The val property belongs to obj1.

obj2.a = 5; // Up to this point, obj2 doesn't have an own property 'val'. But this line will create it to avoid changing the 'val' property in the prototype obj1.

console.log(obj1.val); // 1
console.log(obj2.val); // 5

```

At this point, whenever the 'val' property is accessed in the `obj2` object, it will use the now owned property.

This behavior main happens because a prototype object is usually designed to be used with multiple objects or instances.
And is not a good idea for other instances to see the changes some other instance did on their prototype.

You could actually access and modify the prototype of an object through it like this:

```javascript
obj2.__proto__.val = 15;
```

But accessing and modifying the prototype through the __proto__ property is not recommended at all.
The __proto__ points to the object prototype (in this case to obj1). And it's in between double underscores for a reason. DON'T DO THIS.

We can now say that trying to modify the property (`val`) defined in the prototype (`obj1`) though the object (`obj2`) is not possible. We can say that is an Indirect Immutability.
