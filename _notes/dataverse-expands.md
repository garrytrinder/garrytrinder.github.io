# Dataverse Expands

Can be added like so, using `$select` we can return specific properties

```js
cps_Event($select=cps_eventnumber),createdby($select=domainname,fullname,internalemailaddress,jobtitle),modifiedby($select=domainname,fullname,internalemailaddress,jobtitle)
```

#powerautomate #dataverse