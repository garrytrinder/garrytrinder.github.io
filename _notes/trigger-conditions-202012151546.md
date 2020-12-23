# Trigger Conditions 202012151546

When using the SharePoint Online 'When a file is created or modified (properties only)' we discussed in [[issues-with-polling-sharepoint-202012151523]] how it uses polling which is inefficient.

One way to improve the efficiencies of these triggers is to configure trigger conditions on the action.

A trigger condition allows us to set a defined criteria on the action that will stop the action from being triggered if that criteria is not met and so can add a huge increase in process efficiency.

When used in combination with [[trigger-concurrency-setting-202012081009]] this can help reduce the parallel number of executions, removing executions that potentially have no action to be taken on them, reducing the potential for runs to be queued.

#logicapps #triggerconditions #cost

