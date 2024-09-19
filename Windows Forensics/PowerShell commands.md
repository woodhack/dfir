# PowerShell commands:

List all system info 

`Get-ComputerInfo`

Filter info my OS

`Get-ComputerInfo -Property "OS*"`

When user last logged in

`net user {username}|findstr "last"`

Users with admin privileges:

`Get-LocalGroupMember -Group "Administrators"`

Show scheduled tasks

`Get-ScheduledTask`

Info on a scheduled task

`*$task = Get-ScheduledTask | Where TaskName -EQ “{ task name }”*`