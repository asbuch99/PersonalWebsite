# Vulnerability Scanner

## Overview
The Vulnerability Scanner is a tool designed to detect common security vulnerabilities in web applications. It utilizes regular expressions to search for patterns indicative of vulnerabilities across files within a specified directory.

## Scope
The scope of this project encompasses:
- Implementing detection mechanisms for OWASP Top 10 vulnerabilities.
- Enabling scanning of files within a given directory for vulnerability patterns.
- Displaying detailed information about the identified vulnerabilities, including file paths and matching patterns.

## Code Explanation

### `main.py`
This script initiates the scanning process by calling the `scan_directory` function and printing the results.

```python
import os
import re

# Define the OWASP Top 10 vulnerabilities patterns
OWASP_TOP_10 = {
    # Patterns for OWASP Top 10 vulnerabilities
}

def scan_directory(directory):
    # Function to scan files in a directory for vulnerabilities
    pass

# Example usage
directory_to_scan = "E:/Repos/VulnerabilityScanner"
vulnerabilities_found = scan_directory(directory_to_scan)

if vulnerabilities_found:
    # Display vulnerabilities found
else:
    print("No vulnerabilities found.")
```

### `scan_directory` Function
This function scans files within a specified directory for OWASP Top 10 vulnerability patterns using regular expressions.

```python
def scan_directory(directory):
    vulnerabilities = []

    for root, dirs, files in os.walk(directory):
        for file in files:
            file_path = os.path.join(root, file)
            with open(file_path, "r", encoding="latin-1") as f:
                content = f.read()
            for vulnerability, patterns in OWASP_TOP_10.items():
                for pattern in patterns:
                    matches = re.findall(pattern, content)
                    if matches:
                        vulnerabilities.append((file_path, vulnerability, matches))

    return vulnerabilities
```

### OWASP Top 10 Patterns
The `OWASP_TOP_10` dictionary contains regular expressions representing patterns for various OWASP Top 10 vulnerabilities.

### Example Usage
An example usage of the scanner is demonstrated, where the directory `"E:/Repos/VulnerabilityScanner"` is scanned for vulnerabilities, and the results are printed.

## Usage
To use the Vulnerability Scanner:
1. Clone the repository to your local machine.
2. Navigate to the project directory.
3. Modify the `OWASP_TOP_10` dictionary in `main.py` to add or modify vulnerability patterns as needed.
4. Specify the directory you want to scan in the `directory_to_scan` variable.
5. Run `main.py` to initiate the scanning process.
6. Review the output to identify any detected vulnerabilities.
