# DBSpeed for Scoop

A Scoop bucket for [DBSpeed](https://github.com/ericphamm/dbflux), a fork of DBFlux, on
Windows.

## First install

### 1. Install Scoop

Skip this step if `scoop --version` already prints a version in PowerShell.

Open **PowerShell** from the Start menu as your normal user. Do not choose "Run as
administrator": Scoop installs into your user folder and refuses to run as an administrator.

Allow PowerShell to run the Scoop scripts for your account:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Answer `Y` if it asks. Then install Scoop:

```powershell
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

Scoop needs Git to add a bucket:

```powershell
scoop install git
```

### 2. Install DBSpeed

Add this bucket:

```powershell
scoop bucket add dbspeed https://github.com/ericphamm/scoop-dbspeed
```

Install DBSpeed:

```powershell
scoop install dbspeed/dbspeed
```

Start it from the Start menu, under **Scoop Apps**, or with `dbspeed` in a terminal.

## Update

Close DBSpeed first. Scoop cannot replace a running program.

```powershell
scoop update
```

```powershell
scoop update dbspeed
```

To update automatically, schedule the update once a day in Task Scheduler:

```powershell
$action = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-NoProfile -WindowStyle Hidden -Command scoop update; scoop update dbspeed"
$trigger = New-ScheduledTaskTrigger -Daily -At 9am
Register-ScheduledTask -TaskName "Update DBSpeed" -Action $action -Trigger $trigger
```

## Without Scoop

1. Open the [releases page](https://github.com/ericphamm/dbflux/releases) and, under the
   newest release, download `dbflux-windows-amd64-setup.exe`.
2. Run it. If Windows shows "Windows protected your PC", click **More info** and then
   **Run anyway**. The installer is not signed, which is why Windows asks.
3. Follow the installer and start DBSpeed from the Start menu.

An install made this way does not update itself. DBSpeed shows a notice when a newer
release exists, and you download the new installer the same way.

## How the manifest is kept current

Every DBSpeed release updates `bucket/dbspeed.json` with the new version and checksum.
Release candidates are included, so the manifest always points to the newest build.
