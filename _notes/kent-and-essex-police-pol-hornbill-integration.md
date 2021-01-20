# Kent and Essex Police POL Hornbill Integration

## Estimation Request

Description:
Project Online integration with Hornbill that will read / write data associated to Projects & Tasks between the two systems based on event driven updates. Both systems to house information relating to the links, an example being Tasks to have a Hornbill_GUID column to indicate a link to the item in Hornbill and vice versa.

Key Points:
Hornbill has no timephased data
Hornbill api's are not restful
Hornbill is cloud based
Queue service likely needed (Customer understands a service account will be required)
Not all projects / tasks to go into Hornbill (custom fields within Project Online to flag relevant items)
Two way synchronisation (Hornbill > Proj Online, Proj Online > Hornbill)

Size:
Jubilee House

Associated Documents:
https://cpsglobal.sharepoint.com/:u:/t/KentEssexPolice/Ec0qtqBZ0B9FgUVwGgZndfkBf03xKFY4fLDPlJxJ9ywM3w?e=TK5f7U

Other Information:
Eugene has been involved in initial discovery and further workshops to be completed at the end of Jan on this topic.

## Questions

- We have inexperience with Hornbill API, will support be provided?
  - *Support is on hand from customer (internal knowledge) and Hornbill Developer*
- What authentication methods fo Hornbill use?
  - Does it use OAuth, certificates?
- How do we map a Project user to a Hornbill user for Assignments?
  - Will the customer provide mappings or have SSO configured?
- Unsure as to the areas of responsibility for integration
  - Is the integration direct through API or indirect via file exchange?
- Are there any hosting requirements? 
  - Is using Azure services a possibility or on-prem only?
  - *Azure has been determined as a possible hosting location*
- How are deletes expected to be handled in either POL or Hornbill?
- Do we need only sync specific scheduled tasks or all tasks?
  - If specific tasks, task with activity, payment milestones, key milestones etc?
  - *Only Technical Activities defined as a Custom Field need to be synced (Requirement)*
- What do we do if the plan is checked out in POL when the sync happens?
  - What is the proposed schedule for the sync?
  - Is it on demand?
  - The customer would like it to be event driven (Requirement)
- Does Hornbill have a check-out facility like POL?
  - How do we handle these issues at sync time?
- How do we expect to receive data from Hornbill?
  - Webhook, SFTP, Queue message?
- Are there development environments available for testing against Hornbill?
  - We would require DEV POL and Hornbill, potentially development O365 tenant
  - *A development POL environment is available, a Hornbill trial environment can be spun up (Dependency)*
- Do any technical designs need to be signed off by an internal security team?

### Complexity scale

The following complexity scale has been used in the estimation process.

1. Obvious, Known
2. Complicated, Known Unknowns
3. Complex, Unknown Unknowns

## Creating Project (2)

- Remote Event Receiver - OnProjectCreated
 - WCF Service as event handler
- MSMQ or Service Bus/Azure Storage Queue
- Read from queue - Windows Service/Logic App/Azure Function
- Call Hornbill API (known unknown)
- Update Project Level metadata with Hornbill identifier using custom field

3 days + 2 for Hornbill API (1 week)

## Creating and Assigning Activities 

### POL On Plan Publish (2)

- Remote Event Receiver - OnProjectPublish
 - Reuse WCF Service as event handler
- Reuse MSMQ or Service Bus/Azure Storage Queue
- Read from queue - Windows Service/Logic App/Azure Function
- Determine add or update for Hornbill records
- Call Hornbill API to update or add records (known unknown)
- Update POL Tasks

3 days + 2 for Hornbill API (1 week)

### Hornbill Activity Allocation (3)

- Receive data from unknown source with unknown authentication to unknown location (Unknown Unknowns)
- Script to read from data file of unknown type and populate POL (Unknown Unknowns)

Needs discovery - ??

### Hornbill Updating Activities (3)

- Receive data from unknown source with unknown authentication to unknown location (Unknown Unknowns)
- Script to read from data file of unknown type (Unknown Unknowns)

Needs discovery - ??

### Notifications sent to Project Manager (3)

- Unsure as to what the requirements are, assumption is email?

## Remarks

Would suggest that one way population from POL to Hornbill would be 3-4 weeks of work, broken down into the following. 

- 2 weeks development to deliver
  - Creating a project in POL and creating a project in POL
  - Creating POL tasks in Hornbill
- 1 week testing, deployment and documentation
- 1 week lag
  - Project management
  - Technical management, 
  - Unforeseen Hornbill issues

Delivering these first two pieces will give us an idea of velocity and help us gain a greater understanding of the environment we are working in, the internal & third party teams and weed out any initial teething problems with the external API, removing some of the unknowns around how the integration between Hornbill -> POL will work, so that more refined estimates can be gained.

To give an idea of relativity, it took 8 days to develop, test and document a single PowerShell script to export data stored in InfoPath XML files from a SharePoint library for GDST, which was a relatively simple export with known understanding for integrating with a third party defined schema and did not require event handling or deployments.
