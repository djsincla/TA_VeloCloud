# TA_VeloCloud
Splunk VeloCloud Event Log - Extract VeloCloud Event Log to Splunk via REST API via Splunk Modular Input

# Version
1.0.7

# Author
Dwayne Sinclair / VMware 

# Setup
Copy the TA_VeloCloud folder to $SPLUNK_HOME/etc/apps and restart Splunk

# With thanks to:
Ken Guo
Andrew Lohman
Kevin Fletcher

# Logging
Modular input event logging is to th splunkd.log found at ../Splunk/var/log/splunk/splunkd.log. Search on velocloud to find all events associated with this modular input.

# Endpoint Configuration
VCO URL - The https:// url of VCO without a trailing "/"

Username - An enterprise VCO Login without 2FA with log access.

Password - A password for the username. 

Cookie Refresh Time = 0 to 24 hours. After this time, a new login attempt will be made to VCO and a new cookie will be saved. 
Set to 0 to generate and save a new cookie.

Interval - How often (in seconds) do we poll VCO for event data. We dont want to poll too often so 120-600 seconds is ideal.

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
