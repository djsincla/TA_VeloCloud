# TA_VeloCloud

Splunk VeloCloud Event Log - Extract VeloCloud Event Log to Splunk via the VCO REST API and a Splunk Modular Input.

The API call to VeloCloud Orchestrator (VCO) specifies an interval to minimize the performance impact to VCO of frequent API calls. It is recommended an interval of 120-600 seconds to poll VCO.

There is some overlap between API calls to VCO (interval x 2) to ensure no records are missed. We assume the record ID associated with each VCO event record is ascending and we save the last record ID written and only write records to Splunk which are greater than the saved record ID.

We mask and encrypt the VCO password and save to the Splunk Password DB. We encrypt the VCO session cookie and also save to the Splunk Password DB.

# Author
Dwayne Sinclair / VMware 

# Change Log
- Updated to Support Python3
- 7/16/21 Tested ok with VCO Version 4.2.1
- 7/16/21 Tested ok with Splunk Enterprise 8.2.1
- 7/16/21 Updated to latest version of splunklib and deleted external python libraries from ~/bin

# Version
1.0.10

# With thanks to:
Ken Guo, Andrew Lohman, Kevin Fletcher

# Installation / Setup
When you download this folder from github, it may be suffixed by the github branch name. Rename the folder to "TA-VeloCloud" and copy "TA_VeloCloud" folder to $SPLUNK_HOME/etc/apps and restart Splunk.

# Dependencies
-	Splunk Enterprise 8.0+
-	Python 3.x
-	VeloCloud Orchestrator enterprise username and password credentials
-	Enterprise user account must be “Superuser”, “Standard Admin”, or “Customer Support” role.

# New VeloCloud Orchestrator Endpoint Configuration

Required values are:

Name – The name given to this Modular Input. It is recommended to give it the name of the VeloCloud Orchestrator and Enterprise.

VCO URL – The https URL of the VeloCloud Orchestrator

Username – The VeloCloud Orchestrator username for a VCO enterprise user.

Password – Matching password for the VeloCloud Orchestrator enterprise user.

Optional values are:

Cookie Refresh Time – Successful authentication to VeloCloud Orchestrator (VCO) using a userid and password returns a session cookie which is used for subsequent API calls. Setting this value between 0 and 24 hours is a maximum interval between VCO reauthenticating for a new session cookie. Setting this value to 0 forces the Modular Input to request a session cookie every time the event log is read. If something was to happen to VCO (DR activity etc), modifying the modular input to set this value to 0 then back to a high value is a simple way to regenerate and save a new session cookie. Default is 8 hours.

More Settings – Exposes additional configuration options. 

Interval – Polling interval in seconds between requests to the VeloCloud Orchestrator for event log data. Default is 300 seconds. Minimum is 120 seconds.

Source type, Host, and Index options are Splunk environment specific. Your Splunk administrator will recommend appropriate setting to use. 

# Issues
0120-1 - Low - The API call to VeloCloud Orchestrator incorporates a start and end interval. Start interval does not update if an API call to VeloCloud Orchestrator returns no data. A fix will be to update the start interval if no data is returned.

# Logging
Modular input event logging is to the splunkd.log file found at ../Splunk/var/log/splunk/splunkd.log. Filter on velocloud to find all events associated with this modular input.

# Sample Audit Log
../velocloud_events.py" Cookie time read: 2020-01-01 22:44:52.337208 VCO--12

../velocloud_events.py" Cookie read from Password DB for: VCO--12 

../velocloud_events.py" No Cookie required for: VCO--12

../velocloud_events.py" Last Position read is: 1109532 for: VCO--12

../velocloud_events.py" Last Time Logged is: 2020-01-01T22:45:05.667827Z for: VCO--12

../velocloud_events.py" Request to VCO is: {'interval': {'end': '2020-01-01T23:33:35.169909Z', 'start': '2020-01-01T22:45:05.667827Z'}} for: VCO--12

../velocloud_events.py" 1 records returned from VCO Request for: VCO--12

../velocloud_events.py" Last Position out is: 1109553 for: VCO--12

../velocloud_events.py" Last Time out is: 2020-01-01T23:33:35.169909Z for: VCO--12

../velocloud_events.py" 1 VeloCloud events written to log for: VCO--12

../velocloud_events.py" Cookie time read: 2020-01-01 22:43:42.559030 VCO--47

../velocloud_events.py" Cookie read from Password DB for: VCO--47 

../velocloud_events.py" No Cookie required for: VCO--47

../velocloud_events.py" Last Position read is: 71510885 for: VCO--47

../velocloud_events.py" Last Time Logged is: 2020-01-01T22:44:58.507862Z for: VCO--47

../velocloud_events.py" Request to VCO is: {'interval': {'start': '2020-01-01T22:44:58.507862Z', 'end': '2020-01-
01T23:33:36.454618Z'}} for: VCO--47

../velocloud_events.py" 0 records returned from VCO Request for: VCO--47
