# Using Azure DevOps at OFSTED

- Project Overview
  - OFSTED invested in a Power App to run Inspections, uses SharePoint Online, the goal was to move from SharePoint to Dataverse back end
- CPS Project Team
  - EL: Justine
  - TL: Mike
  - Garry
  - Jack
  - Eugene
- OFSTED Project Team
  - PO: Karen
  - TL: Tim
  - PM: Min
  - Lewis
  - Shaz

- Project Phases
  - Development
    - Replacing the back end, this was done but needed verifying
  - Testing
    - Ensure that things worked as it did before, raise issues for the team to resolve

- Problem
  - Multiple communication channels
    - CPS Teams (Internal & External), OFSTED Teams (External), Email
  - An Excel spreadsheet had been created in the OFSTED Teams channel
    - All communication was in Teams chats
    - Excel spreadsheet was not being updated
  - No defined way of working for how testing issues would be picked up

- Solution
  - Azure Boards
    - If an issue was mentioned, it was immediately logged, a description added to and severity set
    - This helped build an initial backlog of issues in a single place
    - Enabled bugs to be prioritised by severity so we could decide where to concentrate our efforts
  - A Team Project already existed
    - Created by Eugene H to store some exported versions of apps in Azure Repos
    - We created a new Team for the project
      - Granted access to the Team to OFSTED team, so they can be assigned and mentioned in comments
  - At the end of day one, we had a prioritised backlog of bugs that could be worked on
  - A visual representation of the work to be done and progress made
  - Conversations still took place in Teams but the Board always reflected the current state

- Board Flow
  - Each bug moves across the board, left to right.
  - Using out of the box statuses we can define the state
    - New - Not Worked On
    - Active - In Progress 
    - Resolved - Fix applied, awaiting verification
    - Complete - Fix verified
  - Each state is represented by a column on the board

- Board Customisation
  - As we used the board to talk through progress updates, visuals become important
    - Added styling rule to make Critical bugs show up in Red to make them more visible on the board
  - Added column state descriptions to give context of the state
  - Added extra fields to the card display such as State Changed Date

- Reporting
  - As all bugs are being tracked as work items it was easy to create a Bug Report query
  - Created a shared query that returned all bugs, including states, ordered by severity and state, open & high bugs to the top
  - Using the Azure DevOps Email function it became very easy to send updates to all stakeholders as a progress update

- Increasing Communications
  - As we had a Microsoft Team already setup it was easy to configure the Azure DevOps connector in the Team to display the activity within the Team Project
  - Created a new channel called Azure DevOps and configured the connector
  - All activity in DevOps was now visible in Teams
    - Ask Justine to add a comment here?
  - Where discussions were needed outside of DevOps, we could use the Azure DevOps message extensions

- Tracking new requirements
  - New requirements appeared in conversations
  - We were able to record those conversations as user stories in the new state and define as not ready
    - Used tags to help give context around the card, `Needs Discussion, Needs Design`
  - Helped us understand what the requirement was, how it would work and define acceptance criteria before starting the work

 - Summary
   - A single view of the current state
   - Increase communications
   - Easier reporting
   - Better auditing, tracking updates and commenting