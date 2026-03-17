# Troubleshooting Guide — Slow Computer Performance

**Category:** Hardware / Software  
**Applies to:** Windows 10/11  

---

## Common Causes

| Cause | Likelihood |
|-------|------------|
| Too many startup programs | High |
| Low disk space | High |
| Malware / background processes | Medium |
| Insufficient RAM | Medium |
| Overheating | Low |
| Failing hard drive | Low |

---

## Step-by-Step Diagnosis

### Step 1 — Check Task Manager
```
Ctrl + Shift + Esc → Processes tab
```
- CPU above 90%? → Identify which process
- RAM above 90%? → Close unused applications
- Disk at 100%? → See Step 3

### Step 2 — Disable startup programs
```
Ctrl + Shift + Esc → Startup tab
```
- Disable all non-essential startup programs
- Reboot and check performance

### Step 3 — Check disk space
```
This PC → Check C: drive free space
```
- Less than 10% free? → Run Disk Cleanup
```
cleanmgr → Select drive → Clean up system files
```

### Step 4 — Run Disk Cleanup
```
Windows Search → "Disk Cleanup" → Run as Administrator
→ Check all boxes including "System files"
→ OK
```

### Step 5 — Check for malware
```
Windows Security → Virus & threat protection
→ Quick scan
```

### Step 6 — Check temperatures (if overheating suspected)
- Download HWMonitor or SpeedFan
- Check CPU temp — should be under 80°C under load
- Clean dust from vents if laptop

### Step 7 — Check hard drive health
```
# In Command Prompt (Admin):
wmic diskdrive get status
```
- Status should be "OK"
- If "Pred Fail" → back up data immediately and replace drive

---

## Quick Fixes Checklist

- [ ] Reboot the computer
- [ ] Close unused browser tabs
- [ ] Disable startup programs
- [ ] Run Disk Cleanup
- [ ] Check for Windows updates
- [ ] Run antivirus scan
- [ ] Check free disk space

---

## Escalate if:

- Hard drive showing "Pred Fail" status
- RAM test (MemTest86) shows errors
- Blue screen errors (BSOD) occurring
- Performance issues persist after all steps
