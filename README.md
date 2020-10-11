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
