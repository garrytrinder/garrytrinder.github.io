# Using @ symbol in Power Apps formulas

In many languages we can use ? when accessing properties on objects in a safe way

In JavaScript we can use

```js
myObject.?myproperty
```

Which either return the value or an empty string, instead of returning undefined and breaking our code.

We can also do the same in Power Apps formulas using the @ symbol

```js
myTable[@myobject].myproperty
```

#powerapps