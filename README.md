# Pre-Commit Hook Script

## Overview:
This pre-commit hook script scans the staged files in the `src/` directory for secrets (e.g., API keys). If secrets are detected, the commit will be aborted, ensuring sensitive information isn't committed.

## How It Works:
1. Runs from `.git/hooks` directory.
2. Scans the `src/` folder using `2ms.exe`.
3. Removes ANSI escape codes from the scan results.
4. Aborts the commit if secrets are found.

## Setup:
1. Place the script in `.git/hooks/pre-commit`.
2. Ensure `2ms.exe` is installed and configured.
3. Make the script executable:
    ```bash
    chmod +x .git/hooks/pre-commit
    ```

## Configuration:
- Update `SCAN_PATH` as needed to point to the correct directory.
- Ensure the correct path to `2ms.exe` is set in the script, or set it using an environment variable.

## Running:
The script will automatically run when a commit is attempted. If secrets are detected, the commit will be stopped, and the detected secrets will be shown in the output.
