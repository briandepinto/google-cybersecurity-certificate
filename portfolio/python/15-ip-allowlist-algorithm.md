# Python Algorithm: IP Address Allowlist

**Purpose:** Automatically remove unauthorized IP addresses from an allowlist file
**Language:** Python 3
**Date:** [Date]
**Prepared By:** Security Analyst

---

## Overview

This algorithm reads a text file containing a list of approved IP addresses, compares each IP against a list of addresses to be removed, removes any matches, and writes the updated list back to the file. This automates the process of revoking network access for specific IP addresses.

---

## Complete Algorithm

```python
# Define the allowlist file and the IPs to remove
import_file = "allow_list.txt"
remove_list = ["192.168.97.226", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Step 1: Open the file for reading
with open(import_file, "r") as file:

    # Step 2: Read the file contents into a string
    ip_addresses = file.read()

# Step 3: Convert the string to a list using split()
ip_addresses = ip_addresses.split()

# Step 4: Iterate over the remove list and remove matching IPs
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

# Step 5: Convert the list back to a string using join()
ip_addresses = "\n".join(ip_addresses)

# Step 6: Open the file for writing and overwrite with updated list
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

---

## Step-by-Step Explanation

### Step 1: Open the file for reading

```python
with open(import_file, "r") as file:
```

The `open()` function opens the file specified by `import_file`. The `"r"` argument specifies read mode. The `with` statement ensures the file is properly closed after the block executes, even if an error occurs.

---

### Step 2: Read the file contents

```python
ip_addresses = file.read()
```

The `.read()` method reads the entire file contents into a single string. At this point, `ip_addresses` is a string with all IP addresses separated by whitespace (newlines or spaces).

---

### Step 3: Convert the string to a list

```python
ip_addresses = ip_addresses.split()
```

The `.split()` method splits the string on whitespace and returns a list. Each IP address becomes an individual element in the list, making it easy to iterate over and modify.

---

### Step 4: Remove unauthorized IPs

```python
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)
```

A `for` loop iterates over each IP in `remove_list`. The `if element in ip_addresses` check prevents a `ValueError` if the IP is not present in the list. The `.remove()` method removes the first matching element from the list.

---

### Step 5: Convert the list back to a string

```python
ip_addresses = "\n".join(ip_addresses)
```

The `.join()` method concatenates all elements in the list into a single string, with each IP separated by a newline character (`"\n"`). This prepares the data for writing back to the file.

---

### Step 6: Overwrite the file with the updated list

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

Opening the file in write mode (`"w"`) creates or overwrites the file. The `.write()` method writes the updated IP address string, replacing the previous file contents with the revised allowlist.

---

## Python Concepts Used

| Concept | Description |
|---|---|
| `open()` | Built-in function to open a file; mode `"r"` for read, `"w"` for write |
| `with` statement | Context manager — ensures the file is closed automatically |
| `.read()` | Reads entire file contents as a single string |
| `.split()` | Splits a string on whitespace into a list |
| `for` loop | Iterates over each element in a sequence |
| `in` operator | Checks if a value exists within a list |
| `.remove()` | Removes the first matching element from a list |
| `.join()` | Joins list elements into a string with a specified separator |
| `.write()` | Writes a string to an open file |
