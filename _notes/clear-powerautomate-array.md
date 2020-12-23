# How to clear a Power Automate array variable

You cannot directly set an array variable to empty using an expression in Power Automate and the Set variable action must accept a value so you cannot simply blank the array value.

To work around this limitation, create a new variable with the name `EmptyArray` with type `Array` and no initial value.

When you need to clear the your array use the `Set variable` action, selecting the Array variable you want to clear and pass the `EmptyArray` variable as the new value and thus clearing your array.

#powerautomate