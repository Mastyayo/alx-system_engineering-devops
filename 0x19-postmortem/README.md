# 0x19. Postmortem

### Issue Summary:

On April 30, 2023, between 2:00 PM and 4:00 PM EST, our web application experienced a partial outage, affecting approximately 70% of our users. During this time, users were unable to access certain features of the application, resulting in reduced functionality.

### Timeline:

*   2:00 PM: Our monitoring system detected a spike in error rates on the web servers.
*   2:05 PM: Our in-house engineer received a notification from the monitoring system and began investigating.
*   2:10 PM: The engineer noticed that the database was experiencing high CPU usage and suspected a query was causing the issue.
*   2:15 PM: The engineer began investigating slow query logs and optimizing the queries.
*   3:00 PM: After optimizing the queries, the issue persisted. The engineer escalated the issue to the database team.
*   3:15 PM: The database team identified a deadlock between two queries and resolved the issue.
*   3:30 PM: The application was tested and verified to be functioning properly.
*   3:00 PM: The incident was declared and marked resolved.

### Root Cause and Resolution:

The root cause of the partial outage was a deadlock between two queries in the database, which caused high CPU usage and slowed down the entire system. The deadlock occurred due to a race condition that was triggered by a recent code change which also requires additional RAM space that was unavailable.

To resolve the issue, the database team analyzed the deadlock and identified the queries that were causing it. They then optimized the queries to eliminate the race condition and prevent similar issues from occurring in the future and the allocated RAM memory for the web server was increased.

### Corrective and Preventative Measures:

To prevent similar incidents from occurring in the future, we will take the following actions:

*   Implement a more robust testing process for code changes to catch potential race conditions before deployment.
*   Increase monitoring and alerting for database performance metrics to detect issues before they impact users.
*   Improve documentation and communication among teams to facilitate faster incident resolution.
*   Permanently increase the allocated memory by a ratio that can accommodate the current volume of processing load.

### Specific tasks to address the issue include:

*   Review recent code changes and identify potential race conditions.
*   Implement more extensive testing for code changes that involve database queries.
*   Implement additional monitoring and alerting for database performance metrics.
*   Document the incident and share the lessons learned with the team to improve incident response and prevent similar incidents from occurring in the future.

### Misleading Investigation/Debugging Paths:

During the initial investigation, the engineer suspected that slow queries were causing the issue and spent considerable time optimizing them. However, this turned out to be a misleading path, as the root cause was a deadlock between two queries that were not detected by the slow query logs. In retrospect, more extensive testing and monitoring could have caught the issue earlier and saved time on investigation.

### Escalation:

The incident was initially handled by our in-house engineer, who escalated it to the database team when they were unable to resolve the issue. The database team was able to quickly identify the root cause and resolve the issue, resulting in a speedy resolution.

### Conclusion:

We take incidents like this very seriously and are committed to improving our processes to prevent similar incidents from occurring in the future. We apologize for any inconvenience this may have caused our users and will continue to work towards providing a stable and reliable service.
