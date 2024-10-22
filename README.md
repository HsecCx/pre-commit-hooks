
# Pre-Commit Hook Script

A Bash script to prevent committing secrets (e.g., API keys) to the repository by scanning the `src/` (or another target) directory using `2ms.exe`. If secrets are detected exceeding a defined threshold, the commit is aborted.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Disabling the Hook](#disabling-the-hook)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [References](#references)

## Features

- Scans the `src/` directory for secrets using `2ms.exe`.
- Removes ANSI escape codes for clean output.
- Compares detected secrets against a configurable threshold.
- Aborts commit if secrets exceed the threshold.
- Easily enabled or disabled via configuration.
- Configurable paths and thresholds via environment variables.

## Prerequisites

- **Git**: Ensure Git is installed on your system.
- **2ms**: Download and install `2ms.exe` from [Checkmarx/2ms](https://github.com/Checkmarx/2ms).
- **Bash**: The script is written for Bash. Windows users can use Git Bash or WSL.

## Installation

1. **Download `2ms.exe`**

   - Download from the [Checkmarx official repository](https://github.com/Checkmarx/2ms).
   - Place `2ms.exe` in a directory included in your system's `PATH`, or note its location for configuration.

2. **Ensure the Pre-Commit Script is in Place**

   The pre-commit script should be located at `.git/hooks/pre-commit` in your repository. If it's not there, add it accordingly.

3. **Make the Script Executable**

   ```  
   chmod +x .git/hooks/pre-commit

## Configuration
The script can be customized via environment variables:

SCAN_PATH: Directory to scan. Default is `../../src` relative to the script.
`export SCAN_PATH="/path/to/your/src"`

TWO_MS_PATH: Path to 2ms.exe. Default is C:/Tools/windows-amd64/2ms.exe.
`export TWO_MS_PATH="/path/to/2ms.exe"`

THRESHOLD: Maximum allowed secrets before aborting commit. Default is 0.
`export THRESHOLD=1`


ENABLED: Enable or disable the pre-commit scan. Default is true.
`export ENABLED=false`

## Usage
With the pre-commit hook installed and configured, simply commit your changes as usual:

If no secrets are detected over the threshold, the commit proceeds.
If secrets are detected exceeding the threshold, the commit is aborted, and details are displayed.

Disabling the Hook
To temporarily disable the pre-commit scan without removing the script:
`export ENABLED=false`

To re-enable:
` unset ENABLED  # Or set it to true`
## Troubleshooting
### 2ms.exe Not Found:

Ensure 2ms.exe exists at the path specified in TWO_MS_PATH and has execute permissions.

### Script Permissions:

Ensure the pre-commit script is executable:
`chmod +x .git/hooks/pre-commit`

### Invalid TOTAL_SECRETS Value:
If you receive an error about determining the total number of secrets, check the output format of 2ms.exe. The parsing in the script may need adjustment.

### Windows Path Issues:

Ensure paths are correctly formatted for your environment. Windows users may need to adjust paths or use Git Bash.


## License

This project is licensed under the MIT License.