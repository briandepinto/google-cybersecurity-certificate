# Linux File Permissions: Security Audit and Remediation

**Environment:** Linux — `/home/researcher2/projects`
**Date:** [Date]
**Prepared By:** Security Analyst

---

## Overview

This document describes the process of auditing and correcting file permissions in the `/home/researcher2/projects` directory to align with the organization's least-privilege security policy. Using Linux command-line tools, permissions were reviewed and three violations were identified and corrected.

---

## Step 1: Audit Current Permissions

The `ls -la` command lists all files in a directory, including hidden files (those beginning with `.`), along with their full permission strings.

```bash
ls -la /home/researcher2/projects
```

**Sample output:**

```
drwxr-xr-x  3 researcher2 researcher2 4096 Jan 10 10:00 .
drwxr-xr-x 10 researcher2 researcher2 4096 Jan 10 09:50 ..
drwx------  2 researcher2 researcher2 4096 Jan 10 10:00 drafts
-rw-rw-rw-  1 researcher2 researcher2  312 Jan 10 09:55 project_k.txt
-r--r-----  1 researcher2 researcher2  204 Jan 10 09:52 project_m.txt
-rw-rw-r--  1 researcher2 researcher2  418 Jan 10 09:53 project_r.txt
-rw-rw-rw-  1 researcher2 researcher2  511 Jan 10 09:54 .project_x.txt
```

### Reading Permission Strings

Each permission string is 10 characters:

```
-rw-rw-rw-
^  ^  ^  ^
|  |  |  other permissions (r/w/x or -)
|  |  group permissions
|  user (owner) permissions
file type (- = file, d = directory)
```

- `r` = read, `w` = write, `x` = execute, `-` = permission not granted

---

## Step 2: Identify and Fix Violations

### Violation 1: `project_k.txt` — Other Write Permission

**Problem:** The file has permissions `-rw-rw-rw-`. The "other" category (all users not in the owner group) has write access. No user outside the project team should be able to modify this file.

**Fix:**
```bash
chmod o-w /home/researcher2/projects/project_k.txt
```

**Explanation:** `o-w` removes (`-`) write (`w`) permission from other (`o`). The resulting permissions are `-rw-rw-r--`.

---

### Violation 2: `.project_x.txt` — Hidden File with Incorrect Permissions

**Problem:** The hidden file `.project_x.txt` has permissions `-rw-rw-rw-`. This file should be read-only for both the owner and the group, and no permissions for others.

**Fix:**
```bash
chmod u=r,g=r,o-rwx /home/researcher2/projects/.project_x.txt
```

**Explanation:**
- `u=r` sets user (owner) permissions to read-only.
- `g=r` sets group permissions to read-only.
- `o-rwx` removes all permissions from other.

Resulting permissions: `-r--r-----`

---

### Violation 3: `drafts` Directory — Group and Other Access

**Problem:** The `drafts` directory is a working directory for the researcher only. No other users or groups should have access.

**Fix:**
```bash
chmod u=rwx,g=,o= /home/researcher2/projects/drafts
```

**Explanation:**
- `u=rwx` grants the owner full access (read, write, execute — execute is required to enter a directory).
- `g=` removes all group permissions.
- `o=` removes all other permissions.

Resulting permissions: `drwx------`

---

## Summary of Changes

| File / Directory | Before | After | Action |
|---|---|---|---|
| `project_k.txt` | `-rw-rw-rw-` | `-rw-rw-r--` | Removed other write |
| `.project_x.txt` | `-rw-rw-rw-` | `-r--r-----` | Set read-only for user/group, removed other |
| `drafts/` | `drwxr-xr-x` | `drwx------` | Restricted to owner only |
