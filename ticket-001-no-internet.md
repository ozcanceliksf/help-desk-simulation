# Ticket #001 — No Internet Connection

**Category:** Network Connectivity  
**Priority:** High  
**Status:** Resolved  

---

## User Report

> "My computer has no internet access. I can't load any websites. Everything was working fine yesterday."

**User:** Staff member, Windows 10  
**Location:** Office workstation  

---

## Troubleshooting Steps

### Step 1 — Gather information
- When did the issue start? → This morning
- Any recent changes? → Windows update ran overnight
- Other devices affected? → No, only this workstation
- Can ping local network? → Yes (`ping 192.168.1.1` succeeds)
- Can ping external IP? → No (`ping 8.8.8.8` fails)

**Conclusion:** Local network is fine. Issue is with DNS or external routing.

### Step 2 — Check DNS settings
```
ipconfig /all
```
DNS server was set to an invalid address after the Windows update.

### Step 3 — Fix DNS settings
```
netsh interface ip set dns "Ethernet" static 8.8.8.8
netsh interface ip add dns "Ethernet" 8.8.8.8 index=2
```
Or via GUI:
- Control Panel → Network and Sharing Center → Change adapter settings
- Right-click Ethernet → Properties → IPv4 → Use the following DNS server
- Primary: `8.8.8.8` | Secondary: `8.8.4.4`

### Step 4 — Flush DNS cache
```
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

### Step 5 — Verify
- Tested `ping google.com` → Success
- Opened browser → Websites loading correctly

---

## Resolution

DNS settings were corrupted by the overnight Windows update. Reset DNS to Google's public DNS servers and flushed the cache. Internet access restored.

**Time to resolve:** 15 minutes  
**Escalation needed:** No  

---

## Prevention

- Monitor Windows updates for network configuration changes
- Document default DNS settings for all workstations
