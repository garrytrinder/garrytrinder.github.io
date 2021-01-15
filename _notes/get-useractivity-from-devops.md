# Get user activity from Azure DevOps API

Requires a PAT token with `vso.work` scope

```http
GET https://dev.azure.com/cpsglobal/_apis/work/accountmyworkrecentactivity?api-version=6.1-preview.2
```

Returns an unsorted array of activity

```json
{
    "assignedTo": {
        "id": "68bba99b-0004-6c42-9e18-c4816928b35d",
        "name": "Garry Trinder <Garry.Trinder@CPS.co.uk>",
        "displayName": "Garry Trinder",
        "uniqueName": "Garry.Trinder@CPS.co.uk",
        "descriptor": "aad.NjhiYmE5OWItMDAwNC03YzQyLTllMTgtYzQ4MTY5MjhiMzVk"
    },
    "id": 7104,
    "workItemType": "Bug",
    "title": "Template pre-defined tags",
    "state": "Resolved",
    "changedDate": "2021-01-14T20:19:12.103Z",
    "teamProject": "OFSTED",
    "activityDate": "2021-01-14T20:19:12.103Z",
    "activityType": "edited",
    "identityId": "00000000-0000-0000-0000-000000000000"
}
```
