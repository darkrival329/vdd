# VDD Dependency Manager

An Ansible role for managing Maven dependencies and generating changelogs.

## Description

This role provides functionality to:
- Update Maven dependencies in pom.xml files
- Update Maven build plugin versions
- Update Maven properties
- Generate and maintain changelogs in Keep a Changelog format

## Requirements

- Ansible 2.9 or higher
- community.general collection (>=3.0.0)
- Python 3.6 or higher
- Maven project with pom.xml

## Role Variables

### Required Variables

The following variables must be defined in your dependency configuration file:

```yaml
global:
  release_version: "1.0.0"  # Semantic version for the release
  release_date: "2024-03-21"  # Release date in YYYY-MM-DD format
  dependencies:  # List of dependencies to update
    - artifactId: "example-dependency"
      version: "1.0.0"
  properties:  # Maven properties to update
    maven.compiler.source: "17"
    maven.compiler.target: "17"
  build_plugins:  # Build plugins to update
    - artifactId: "maven-compiler-plugin"
      version: "3.11.0"
```

### Optional Variables

The following variables can be customized in your playbook:

```yaml
# Path to the pom.xml file
pom_file: "./pom.xml"

# Path to the changelog file
changelog_path: "CHANGELOG.md"

# Enable debug mode for verbose output
debug_mode: false

# CI Project URL for changelog links (defaults to CI_PROJECT_URL environment variable)
ci_project_url: "https://gitlab.example.com/group/project"
```

## Example Playbook

```yaml
- name: Update dependencies and generate changelog
  hosts: localhost
  gather_facts: false
  vars_files:
    - dependency_config.json
  roles:
    - role: vdd_dependency_manager
      vars:
        debug_mode: true
```

## Example dependency_config.json

```json
{
  "global": {
    "release_version": "1.2.7",
    "release_date": "2024-03-21",
    "dependencies": [
      {
        "artifactId": "database-interface",
        "version": "1.0.14-SNAPSHOT"
      }
    ],
    "properties": {
      "maven.compiler.source": "18",
      "maven.compiler.target": "18"
    },
    "build_plugins": [
      {
        "artifactId": "maven-compiler-plugin",
        "version": "3.12.0"
      }
    ]
  }
}
```

## License

MIT

## Author Information

VDD Team 