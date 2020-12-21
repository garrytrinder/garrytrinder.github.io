# Drawback of Using Concurrency Control in Logic App Triggers 202012081257

When setting the Concurrency Control on a Logic App trigger there can be side effects introduced into the workflow.

As discussed in [[logic-app-executions-are-queued-202012081017]], when Logic App executions are queued, the time in which they are executed becomes dependant on the speed at which the running Logic App instances complete.

This can become an problem when Logic App executions are batched, as discussed in [[drop-off-library-trigger-202012080949]] and [[main-library-trigger-202012111433]] we know that the SharePoint Online trigger will run every three minutes and batch changes together increasing the likelihood that Logic Apps will be executed in parallel and potentially be queued.

As the queued instances wait for execution, if the sum of the total execution time of the batch (including queue time) is greater than the interval window and the system is under high usage, the scenario of adding more queued Logic App instances can occur which results in Logic Apps waiting more and more until the queue has been processed.

#logicapps #concurrency
