---
layout: page
title: Trivy Security Scanning
---

# Trivy Security Scanning

This project uses Trivy, a comprehensive vulnerability scanner, integrated into our GitHub Actions workflow to ensure the security of our codebase and dependencies.

## Overview

Trivy is configured to scan our project files and dependencies for known vulnerabilities. This scan is automatically triggered on every push to the main branch and for all pull requests targeting the main branch.

## Workflow Details

The security scanning workflow is defined in `.github/workflows/trivy-scan.yml`. Here's a breakdown of what it does:

1. **Trigger**: The workflow runs on pushes to the `main` branch and pull requests targeting the `main` branch.

2. **Environment**: The scan runs on the latest Ubuntu runner provided by GitHub Actions.

3. **Steps**:
   - Checkout the repository code
   - Run Trivy vulnerability scanner
   - List files in the current directory (for debugging)
   - Display SARIF file content (for debugging)
   - Upload scan results to GitHub Security tab

## Trivy Configuration

Our Trivy scan is configured with the following settings:

- **Scan Type**: File system (`fs`)
- **Scan Target**: The entire repository (`.`)
- **Output Format**: SARIF (for GitHub Security tab integration)
- **Severity Levels**: CRITICAL, HIGH

## Viewing Results

Scan results are automatically uploaded to the GitHub Security tab of our repository. To view the results:

1. Go to our GitHub repository
2. Click on the "Security" tab
3. Select "Code scanning" from the left sidebar
4. You'll see a list of any vulnerabilities detected by Trivy

## Addressing Vulnerabilities

If Trivy detects any vulnerabilities:

1. Review the details provided in the GitHub Security tab
2. Prioritize addressing critical and high severity issues
3. Update the affected dependencies or code as necessary
4. Commit your changes and push them to trigger a new scan

## Customizing the Scan

To modify the Trivy scan configuration:

1. Open `.github/workflows/trivy-scan.yml`
2. Locate the "Run Trivy vulnerability scanner" step
3. Adjust the parameters as needed (e.g., changing severity levels, ignoring certain vulnerabilities)
4. Commit and push your changes

## Troubleshooting

If you encounter issues with the Trivy scan:

1. Check the GitHub Actions logs for detailed output
2. Ensure the SARIF file is being generated correctly
3. Verify that the workflow has the necessary permissions

For persistent issues, please open an issue in our repository for assistance.

## Further Reading

- [Trivy Documentation](https://aquasecurity.github.io/trivy/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [SARIF Specification](https://sarifweb.azurewebsites.net/)