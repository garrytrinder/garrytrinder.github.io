# Microsoft Graph Metadata

```
GET https://graph.microsoft.com/v1.0/$metadata
```

Example response with Graph alias
```xml
<?xml version="1.0" encoding="utf-8"?>
<edmx:Edmx Version="4.0" xmlns:edmx="http://docs.oasis-open.org/odata/ns/edmx">
  <edmx:DataServices>
    <Schema Namespace="microsoft.graph" Alias="graph" xmlns="http://docs.oasis-open.org/odata/ns/edm">
      <EnumType Name="appliedConditionalAccessPolicyResult">
        <Member Name="success" Value="0" />
        <Member Name="failure" Value="1" />
        <Member Name="notApplied" Value="2" />
        <Member Name="notEnabled" Value="3" />
        <Member Name="unknown" Value="4" />
        <Member Name="unknownFutureValue" Value="5" />
      </EnumType>
```

> EnumTypes are the possible return values for properties in the response

> If I look at the <EntityType Name="[resource]Root"> I should be able to correctly get all the sub-resources available for the root resource

EntityTypes define a resource on the top level alias
