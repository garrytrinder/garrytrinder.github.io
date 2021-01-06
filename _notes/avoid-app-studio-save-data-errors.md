# Avoid App Studio save Data Errors

Power Apps that use the SaveData formula will throw errors when editing in App Studio as it can only be used when running on via the Power Apps mobile app or windows desktop app.

We can suppress these errors by stopping SaveData from being run by using a global variable and wrapping the SaveData formulas in an if statement.

```js
Set(gblIsBrowser, IsBlank(Acceleration.X));
If(!gblIsBrowser,SaveData(<record>,<name>));
```

As `Acceleration.X` is only populated on a mobile device, when the app is being edited in the App Studio, it will return a blank value.

However, this will not work if using the Power Apps Windows Desktop app, so to solve the issue for both mobile and desktop, we can perform a test to see if SaveData returns an error by passing it an empty table and checking to see if an error is returned.

```js
Set(gblIsBrowser, IsError(SaveData(Table({}),"_SaveDataCheck")));
```