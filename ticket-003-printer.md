# Ticket #003 — Printer Not Printing

**Category:** Hardware / Peripheral  
**Priority:** Medium  
**Status:** Resolved  

---

## User Report

> "The office printer stopped working. I send jobs to it but nothing prints. The printer shows online on my computer."

**User:** Office staff, Windows 11  
**Printer:** HP LaserJet network printer  

---

## Troubleshooting Steps

### Step 1 — Gather information
- Issue affects one user or everyone? → Everyone on the floor
- Any error messages on printer display? → No, shows "Ready"
- Any paper jams recently? → Yes, cleared it this morning
- Print queue status? → 47 jobs stuck in queue

**Conclusion:** Print spooler stuck with backlogged jobs after the paper jam.

### Step 2 — Clear the print queue
```
# Open Services
services.msc → Print Spooler → Stop

# Delete stuck jobs
cd C:\Windows\System32\spool\PRINTERS
del /Q /F /S *.*

# Restart spooler
services.msc → Print Spooler → Start
```

Or via PowerShell (run as Administrator):
```powershell
Stop-Service -Name Spooler
Remove-Item -Path "C:\Windows\System32\spool\PRINTERS\*" -Force -Recurse
Start-Service -Name Spooler
```

### Step 3 — Test print
- Sent a test page from one workstation → Printed successfully
- Notified all users queue was cleared

### Step 4 — Verify printer driver
- Checked driver version → Up to date
- No driver reinstall needed

---

## Resolution

Print spooler was stuck with 47 queued jobs following a paper jam. Stopped the Print Spooler service, cleared all pending jobs, restarted the service. Printer fully operational.

**Time to resolve:** 12 minutes  
**Escalation needed:** No  
**Users affected:** 12  

---

## Prevention

- After clearing paper jams, always check and clear the print queue
- Consider setting up print queue monitoring alerts
