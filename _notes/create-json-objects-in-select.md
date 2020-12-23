# Create JSON objects in select action

When using select to map an array of objects into another format, its very easy to do this using simple data types, but if you have to map the values inside and object based property it becomes more difficult.

In Dataverse, expanded objects are returned as strings, so we first have to convert them to JSON to access the property values

We can use concat() to construct a JSON string and then use json() to convert it to an object which will then be added to the new array object.

```js
json(concat('{ "Claims": "',json(item()?['modifiedby'])?['domainname'],'", "Department": "','','","DisplayName": "',json(item()?['modifiedby'])?['fullname'],'", "Email": "',json(item()?['modifiedby'])?['internalemailaddress'],'", "JobTitle": "',json(item()?['modifiedby'])?['jobtitle'],'" }'))
```

#powerautomate #logicapps #json