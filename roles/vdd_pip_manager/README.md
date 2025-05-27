# VDD Pip Manager Role

This Ansible role manages Python package dependencies in your project by updating requirements.txt and maintaining a changelog of package updates.

## Features

- Updates Python package versions in requirements.txt
- Maintains a changelog of package updates
- Supports custom requirements file location
- Handles Python version specification
- Creates requirements.txt if it doesn't exist

## Configuration

The role expects a configuration file (dependency_config.json) with the following structure:

```json
{
  "global": {
    "python_version": "3.9.0",
    "dependencies": [
      {
        "name": "requests",
        "version": "2.28.1"
      },
      {
        "name": "pandas",
        "version": "1.5.0"
      }
    ],
    "release_version": "1.0.0",
    "release_date": "2024-03-20"
  }
}
```

### Variables

- `requirements_file`: Path to requirements.txt (default: "requirements.txt")
- `changelog_path`: Path to CHANGELOG.md (default: "CHANGELOG.md")
- `debug_mode`: Enable debug output (default: false)

## Usage

1. Create a dependency_config.json file with your package configuration
2. Include the role in your playbook:

```yaml
- name: Update Python dependencies
  hosts: localhost
  roles:
    - vdd_pip_manager
```

## Example

```yaml
- name: Update Python dependencies
  hosts: localhost
  vars:
    requirements_file: "requirements/prod.txt"
    changelog_path: "docs/CHANGELOG.md"
    debug_mode: true
  roles:
    - vdd_pip_manager
``` 