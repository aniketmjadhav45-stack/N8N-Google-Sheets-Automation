# N8N-Google-Sheets-Automation

n8n Workflow Documentation
This repository contains four automated n8n workflows designed to streamline data management and communication tasks using Google Sheets integration.
Workflows Overview
Flow 1 - WebLink Auto-Fill
Purpose: Automatically processes and enriches data from Google Sheets with external API information.
Workflow Steps:

Google Sheets Trigger - Monitors sheet for row updates (3 items)
Code Node - Processes and transforms the triggered data
HTTP Request - Fetches external data from web APIs (1 item)
Code1 Node - Processes API response
Code2 Node - Further data transformation
Update Row in Sheet - Writes enriched data back to Google Sheets
If Node - Conditional logic for flow control

Use Case: Ideal for automatically enriching spreadsheet data with external information (e.g., fetching company details, validating URLs, or gathering additional metadata).

Flow 2 - Assign Project to Developer
Purpose: Automates project assignment workflow from Google Sheets to team members.
Workflow Steps:

Google Sheets Trigger - Detects new or updated project entries (3 items)
Get row(s) in sheet - Retrieves related project data (3 items)
Code Node - Processes assignment logic
Update row in sheet - Updates assignment status in Google Sheets
Append row in sheet - Logs assignment history

Use Case: Perfect for project management scenarios where tasks need to be automatically assigned to developers based on predefined criteria (availability, skills, workload).

Flow 3 - Sync Developer Sheets
Purpose: Synchronizes data across multiple Google Sheets for developer tracking.
Workflow Steps:

Google Sheets Trigger - Monitors main sheet for updates (5 items)
Dev_MK Sheet - Reads developer-specific data (25 items)
Master Sheet - Accesses central data repository (25 items)
Code Node - Synchronization logic processing
Master sheet1 - Updates primary tracking sheet
Master sheet - Final data consolidation

Use Case: Maintains data consistency across multiple sheets, ensuring all stakeholders have up-to-date information about developer activities, project status, and resource allocation.

Flow 4 - Daily Pending Reminder
Purpose: Sends automated reminders for pending tasks via Gmail.
Workflow Steps:

Schedule Trigger - Runs at predetermined intervals (daily)
Get row(s) in sheet - Fetches pending task data (3 items)
Code Node - Processes reminder logic and formats messages
Get row(s) in sheet1 - Retrieves additional context data
Code1 Node - Prepares email content
Code2 Node - Final message formatting
Send a message - Dispatches reminder emails via Gmail

Use Case: Ensures team members receive timely notifications about pending deliverables, approaching deadlines, or tasks requiring attention.

Setup Requirements
Prerequisites

n8n instance (self-hosted or cloud)
Google Sheets API credentials
Gmail API credentials (for Flow 4)
Valid OAuth2 authentication for Google services

Configuration Steps

Import Workflows

Download the workflow JSON files from this repository
Import into your n8n instance via Settings > Import from File


Configure Google Sheets Credentials

Navigate to Credentials in n8n
Add Google Sheets OAuth2 credentials
Authorize access to your Google account


Configure Gmail Credentials (for Flow 4)

Add Gmail OAuth2 credentials
Grant necessary permissions for sending emails


Update Sheet References

Open each workflow
Update Google Sheets nodes with your specific sheet IDs
Configure column mappings as per your data structure


Customize Code Nodes

Review and modify code nodes based on your specific business logic
Adjust data transformation rules as needed


Set Schedule (for Flow 4)

Configure the Schedule Trigger with your preferred timing
Recommended: Daily at 9:00 AM for pending task reminders




Workflow Triggers
FlowTrigger TypeFrequencyFlow 1Google Sheets - Row UpdateReal-timeFlow 2Google Sheets - Row UpdateReal-timeFlow 3Google Sheets - Row UpdateReal-timeFlow 4ScheduleDaily (configurable)

Data Flow Architecture
Google Sheets → n8n Trigger → Data Processing → External APIs (if needed) → 
Data Transformation → Update Google Sheets / Send Notifications

Best Practices

Error Handling: All workflows include conditional nodes for error management
Data Validation: Code nodes validate data before processing
Logging: Consider adding logging nodes to track workflow execution
Testing: Test each workflow with sample data before production deployment
Backup: Maintain backup copies of your Google Sheets


Troubleshooting
Common Issues
Workflow not triggering:

Verify Google Sheets credentials are valid and not expired
Check that the correct sheet and tab are selected
Ensure row updates are being made to monitored columns

HTTP Request failures:

Verify API endpoints are accessible
Check authentication headers and API keys
Review rate limiting policies

Email not sending:

Confirm Gmail API is enabled
Check OAuth2 token validity
Verify recipient email addresses


Security Considerations

Store all credentials securely in n8n's credential management system
Never commit credentials to version control
Use environment variables for sensitive configuration
Regularly rotate API keys and OAuth tokens
Implement row-level security in Google Sheets where applicable


Maintenance

Weekly: Review workflow execution logs
Monthly: Update dependencies and check for n8n updates
Quarterly: Audit credential expiration dates
As Needed: Optimize code nodes for performance
