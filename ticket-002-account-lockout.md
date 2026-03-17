# Ticket #002 — Account Lockout

**Category:** Account & Access  
**Priority:** High  
**Status:** Resolved  

---

## User Report

> "I can't log into my computer. It says my account is locked out. I need to get to a meeting in 10 minutes."

**User:** Manager, Windows 10 domain-joined PC  
**Location:** Conference room  

---

## Troubleshooting Steps

### Step 1 — Gather information
- Error message: "Your account has been locked out"
- Last successful login: Yesterday
- Any password changes recently? → No
- Mobile device or other device syncing old password? → Yes, work phone

**Conclusion:** Old password cached on mobile device causing repeated failed login attempts → triggering lockout policy.

### Step 2 — Unlock the account (Admin action)
Via Active Directory:
```
Active Directory Users and Computers →
Find user account →
Right-click → Properties →
Account tab →
Check "Unlock account" checkbox →
Apply → OK
```

Or via PowerShell:
```powershell
Unlock-ADAccount -Identity "username"
```

### Step 3 — Verify unlock
```powershell
Get-ADUser -Identity "username" -Properties LockedOut | Select LockedOut
# Should return: False
```

### Step 4 — Address root cause
- Asked user to update password on mobile device
- Updated Exchange ActiveSync profile on phone
- Confirmed no more repeated failed attempts in event log

### Step 5 — Verify
- User logged in successfully
- Made it to meeting on time

---

## Resolution

Account was locked due to old cached credentials on mobile device. Unlocked via Active Directory and updated credentials on mobile device to prevent recurrence.

**Time to resolve:** 8 minutes  
**Escalation needed:** No  

---

## Prevention

- Educate users to update passwords on all devices simultaneously
- Set up account lockout notification alerts for IT team
