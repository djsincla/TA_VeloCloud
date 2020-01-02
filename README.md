# TA_VeloCloud

Splunk VeloCloud Event Log - Extract VeloCloud Event Log to Splunk via REST API via Splunk Modular Input. 

The API call to VeloCloud Orchestrator (VCO) specifies an interval to minimize the performance impact to VCO of frequent API calls. It is recommended an interval of 120-600 seconds to poll VCO.

There is some overlap between API calls to VCO (interval x 2) to ensure no records are missed. We assume the record ID associated with each VCO event record is ascending and we save the last record ID written and only write records to Splunk which are greater than the saved record ID.

We mask and encrypt the VCO password and save to the Splunk Password DB. We encrypt the VCO session cookie and also save to the Splunk Password DB.

# Version
1.0.7

# Author
Dwayne Sinclair / VMware 

# Setup
Copy the TA_VeloCloud folder to $SPLUNK_HOME/etc/apps and restart Splunk

# With thanks to:
Ken Guo, Andrew Lohman, Kevin Fletcher

# Logging
Modular input event logging is to th splunkd.log found at ../Splunk/var/log/splunk/splunkd.log. Search on velocloud to find all events associated with this modular input.

# Endpoint Configuration
VCO URL - The https:// url of VCO without a trailing "/"

Username - An enterprise VCO Login without 2FA with log access.

Password - A password for the username. 

Cookie Refresh Time = 0 to 24 hours. After this time, a new login attempt will be made to VCO and a new cookie will be saved. 
Set to 0 to generate and save a new cookie.

Interval - How often (in seconds) do we poll VCO for event data. We dont want to poll too often so 120-600 seconds is ideal.

# Issues
0120-1 - Low - The API call to VeloCloud Orchestrator incorporates a start and end interval. Start interval does not update if an API call to VeloCloud Orchestrator returns no data. A fix will be to update the start interval if no data is returned.

# Sample Log

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
