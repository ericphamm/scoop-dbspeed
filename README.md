# DBSpeed for Scoop

A Scoop bucket for [DBSpeed](https://github.com/ericphamm/dbflux), a fork of DBFlux, on
Windows.

## Install

```powershell
scoop bucket add dbspeed https://github.com/ericphamm/scoop-dbspeed
scoop install dbspeed/dbspeed
```

DBSpeed appears in the Start menu under Scoop Apps. It can also be started with
`dbspeed` from a terminal.

## Update

```powershell
scoop update
scoop update dbspeed
```

To update automatically, schedule the update once a day in Task Scheduler:

```powershell
$action = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-NoProfile -WindowStyle Hidden -Command scoop update; scoop update dbspeed"
$trigger = New-ScheduledTaskTrigger -Daily -At 9am
Register-ScheduledTask -TaskName "Update DBSpeed" -Action $action -Trigger $trigger
```

Close DBSpeed before an update runs. Scoop cannot replace a running program.

## How the manifest is kept current

Every DBSpeed release updates `bucket/dbspeed.json` with the new version and checksum.
Release candidates are included, so the manifest always points to the newest build.
