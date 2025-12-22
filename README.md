# .github

Default community health files for [@sealad886](https://github.com/sealad886) repositories.

## What is this?

This is a special `.github` repository that provides default community health files and configurations for all public repositories in the [@sealad886](https://github.com/sealad886) organization. Files in this repository will be used as defaults for any public repository that doesn't have its own file of that type.

## Contents

### Community Health Files

- **[LICENSE](LICENSE)** - MIT License for all projects
- **[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)** - Contributor Covenant Code of Conduct (v2.1)
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Guidelines for contributing to projects
- **[SECURITY.md](SECURITY.md)** - Security policy and vulnerability reporting instructions

### GitHub Configuration

- **[.github/FUNDING.yml](.github/FUNDING.yml)** - Sponsorship and funding information
- **[.github/dependabot.yml](.github/dependabot.yml)** - Automated dependency updates configuration

### Issue and PR Templates

- **[.github/ISSUE_TEMPLATE/bug_report.md](.github/ISSUE_TEMPLATE/bug_report.md)** - Template for bug reports
- **[.github/ISSUE_TEMPLATE/feature_request.md](.github/ISSUE_TEMPLATE/feature_request.md)** - Template for feature requests
- **[.github/ISSUE_TEMPLATE/config.yml](.github/ISSUE_TEMPLATE/config.yml)** - Issue template configuration
- **[.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md)** - Template for pull requests

### GitHub Actions Workflows

- **[.github/workflows/ci.yml](.github/workflows/ci.yml)** - Continuous integration workflow for linting, testing, and building
- **[.github/workflows/codeql-analysis.yml](.github/workflows/codeql-analysis.yml)** - CodeQL security scanning workflow
- **[.github/workflows/stale.yml](.github/workflows/stale.yml)** - Automated stale issue and PR management

## How It Works

When a repository doesn't have its own community health file, GitHub will automatically use the files from this repository. This ensures consistent community guidelines and contribution processes across all repositories.

## Customization

Individual repositories can override these defaults by creating their own files with the same names. This allows for project-specific customization while maintaining sensible defaults.

## Learn More

- [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [About community profiles for public repositories](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/about-community-profiles-for-public-repositories)

## License

This repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.