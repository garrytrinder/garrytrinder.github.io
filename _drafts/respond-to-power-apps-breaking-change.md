# Respond to Power Apps breaking change

This one threw me this morning when re-importing a Flow that uses the Respond to Power Apps action in Power Automate, as it looks like at some point the behaviour of the action has changed to support returning multiple values.

When re-importing an existing Flow that used this action, although the UI shows the potential to return multiple values from the Power App side it is just expecting a single value. I got invalid type errors thrown where the Flow was used in the Power App like below.

```js
Set(gblUploadEvidenceReceived,EEGEvidenceSync.Run(EvidenceJSON,SelectedRemitLabel))
```

As the new Flow is now returning a Record and not a boolean, the fix was to state the property in the record to use to fix the broken formulas.

```js
Set(gblUploadEvidenceReceived,EEGEvidenceSync.Run(EvidenceJSON,SelectedRemitLabel).evidenceuploadreceived)
```