# Avoid App Studio save Data Errors

Power Apps that use the SaveData formula will through errors when editing in App Studio as it can only be used when running on a mobile device.

We can suppress these errors by stopping SaveData from being run by using a global variable and wrapping the SaveData formulas in an if statement.

```js
Set(gblIsBrowser, IsBlank(Acceleration.X));
If(!gblIsBrowser,SaveData(colEEGLogs,gblEEGLogs));
```

As `Acceleration.X` is only populated on a mobile device, when the app is being edited in the App Studio, it will return a blank value.