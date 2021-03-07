# TA_VeloCloud

Splunk VeloCloud Event Log - Extract VeloCloud Event Log to Splunk via REST API via Splunk Modular Input. 

The API call to VeloCloud Orchestrator (VCO) specifies an interval to minimize the performance impact to VCO of frequent API calls. It is recommended an interval of 120-600 seconds to poll VCO.

There is some overlap between API calls to VCO (interval x 2) to ensure no records are missed. We assume the record ID associated with each VCO event record is ascending and we save the last record ID written and only write records to Splunk which are greater than the saved record ID.

We mask and encrypt the VCO password and save to the Splunk Password DB. We encrypt the VCO session cookie and also save to the Splunk Password DB.

# Author
Dwayne Sinclair / VMware 

# Change Log
- Tested ok with VCO Version 4.2
- Updated to Python3
- Added Support for VCO API Tokens Replacing Passwords

# Version
1.0.9

# With thanks to:
Ken Guo, Andrew Lohman, Kevin Fletcher

# Installation / Setup
Copy "TA_VeloCloud" folder to $SPLUNK_HOME/etc/apps and restart Splunk.

# Dependencies
-	Splunk Enterprise 8.0+
-	Python 3.x
-	VeloCloud Orchestrator enterprise username and API Token.
-	Enterprise user account must be “Superuser”, “Standard Admin”, or “Customer Support” role.
- Tested up to VCO V4.2

# In Progress
TBD - Automatic Token Refresh

# New VeloCloud Orchestrator Endpoint Configuration

Required values are:

Name – The name given to this Modular Input. It is recommended to give it the name of the VeloCloud Orchestrator and Enterprise.

VCO URL – The https URL of the VeloCloud Orchestrator

Username – The VeloCloud Orchestrator username for a VCO enterprise user.

API Token – The API Token generated against this username.

Optional values are:

More Settings – Exposes additional configuration options. 

Interval – Polling interval in seconds between requests to the VeloCloud Orchestrator for event log data. Default is 300 seconds. Minimum is 120 seconds.

Source type, Host, and Index options are Splunk environment specific. Your Splunk administrator will recommend appropriate setting to use. 

# Issues
03/21 - Currently there is no automatic refresh of the API Token. Add a calendar item as a reminder to refresh the token before it expires.

# Logging
Modular input event logging is to the splunkd.log file found at ../Splunk/var/log/splunk/splunkd.log. Filter on velocloud to find all events associated with this modular input.

# Sample Audit Log
../velocloud_events.py" Last Position read is: 1109532 for: VCO--12

../velocloud_events.py" Last Time Logged is: 2020-01-01T22:45:05.667827Z for: VCO--12

../velocloud_events.py" Request to VCO is: {'interval': {'end': '2020-01-01T23:33:35.169909Z', 'start': '2020-01-01T22:45:05.667827Z'}} for: VCO--12

../velocloud_events.py" 1 records returned from VCO Request for: VCO--12

../velocloud_events.py" Last Position out is: 1109553 for: VCO--12

../velocloud_events.py" Last Time out is: 2020-01-01T23:33:35.169909Z for: VCO--12

../velocloud_events.py" 1 VeloCloud events written to log for: VCO--12

../velocloud_events.py" Last Position read is: 71510885 for: VCO--47

../velocloud_events.py" Last Time Logged is: 2020-01-01T22:44:58.507862Z for: VCO--47

../velocloud_events.py" Request to VCO is: {'interval': {'start': '2020-01-01T22:44:58.507862Z', 'end': '2020-01-
01T23:33:36.454618Z'}} for: VCO--47

../velocloud_events.py" 0 records returned from VCO Request for: VCO--47
