# Contributing to django-lead-capture

Thank you for your interest in contributing to django-lead-capture!

## Development Setup

### Install for Development

```bash
# Clone the repository
git clone https://github.com/heysamtexas/django-lead-capture.git
cd django-lead-capture

# Install in development mode with dev dependencies
pip install -e ".[dev]"
```

### Running Tests

```bash
# Basic import test
python -c "import django_lead_capture; print('Successfully imported django-lead-capture')"
```

### Code Quality

This project uses:
- **ruff** for linting and formatting
- **mypy** for type checking (configured for Django)

```bash
# Format code
ruff format .

# Lint code
ruff check .

# Type check
mypy src/django_lead_capture
```

## Release Process

This package uses GitHub Actions for automated publishing to PyPI using Trusted Publishing (OIDC).

### Prerequisites

- PyPI project must be configured with Trusted Publishing for this GitHub repository
- You must have write access to the repository
- You must be able to create releases

### Steps to Release a New Version

1. **Update the version** in `pyproject.toml`:
   ```toml
   [project]
   name = "django-lead-capture"
   version = "0.2.0"  # Update this
   ```

2. **Update CHANGELOG.md** with release notes:
   ```markdown
   ## [0.2.0] - 2025-XX-XX

   ### Added
   - New feature description

   ### Changed
   - Changes to existing functionality

   ### Fixed
   - Bug fixes
   ```

3. **Commit and push the changes**:
   ```bash
   git add pyproject.toml CHANGELOG.md
   git commit -m "Bump version to 0.2.0"
   git push origin master
   ```

4. **Create and push a git tag**:
   ```bash
   git tag v0.2.0
   git push origin v0.2.0
   ```

5. **Create a GitHub release**:
   ```bash
   gh release create v0.2.0 \
     --title "v0.2.0 - Release Title" \
     --notes "Release description here"
   ```

   Or create the release manually through the GitHub web interface at:
   https://github.com/heysamtexas/django-lead-capture/releases/new

### What Happens Automatically

Once you create a GitHub release:

1. **GitHub Actions workflow triggers** (`.github/workflows/publish.yml`)
2. **Version verification** - Ensures git tag matches pyproject.toml version
3. **Dependencies installed** - Sets up Python 3.12 and uv
4. **Tests run** - Basic import test to verify package integrity
5. **Package built** - Creates wheel (.whl) and source distribution (.tar.gz)
6. **Published to PyPI** - Using Trusted Publishing (no manual tokens needed)
7. **Digital attestations** - Automatic attestation generation for supply chain security

The entire process takes about 30 seconds.

### Verify Publication

After the workflow completes:

1. **Check GitHub Actions**: Ensure the workflow passed
   ```bash
   gh run list --limit 1
   ```

2. **Verify on PyPI**:
   ```bash
   pip index versions django-lead-capture
   ```

3. **Test installation**:
   ```bash
   pip install --upgrade django-lead-capture
   python -c "import django_lead_capture; print(f'Installed version: {django_lead_capture.__version__}')"
   ```

### Troubleshooting

**Version mismatch error**:
- Make sure the version in `pyproject.toml` exactly matches the git tag (without the 'v' prefix)
- Git tag: `v0.2.0` → pyproject.toml: `version = "0.2.0"`

**Workflow fails at publish step**:
- Check that PyPI Trusted Publishing is configured correctly
- Verify the GitHub repository is authorized in PyPI project settings

**Tests fail**:
- Run tests locally before creating the release
- Fix any import or dependency issues

## Code Standards

### Docstrings

Use Django-style docstrings:

```python
def my_function(param1, param2):
    """Short description of function.

    Longer description if needed, explaining behavior,
    edge cases, etc.

    Args:
        param1: Description of param1
        param2: Description of param2

    Returns:
        Description of return value
    """
```

### Type Hints

While not strictly enforced, type hints are appreciated:

```python
from typing import Optional

def process_campaign(campaign_id: int) -> Optional[str]:
    """Process a campaign and return result."""
    ...
```

### Django Best Practices

- Follow Django naming conventions
- Use Django's built-in validators where possible
- Leverage Django's ORM efficiently
- Write migrations for all model changes

## Package Structure

```
django-lead-capture/
├── .github/
│   └── workflows/
│       └── publish.yml          # PyPI publishing workflow
├── src/
│   └── django_lead_capture/
│       ├── __init__.py
│       ├── admin.py             # Django admin configuration
│       ├── apps.py              # App configuration
│       ├── checks.py            # Django system checks
│       ├── forms.py             # Django forms
│       ├── models.py            # Database models
│       ├── urls.py              # URL routing
│       ├── utils.py             # Utility functions
│       ├── views.py             # View functions
│       ├── emails.py            # Email handling
│       ├── migrations/          # Database migrations
│       └── templates/           # HTML templates
├── CHANGELOG.md                 # Version history
├── CONTRIBUTING.md              # This file
├── LICENSE                      # MIT License
├── README.md                    # Package documentation
└── pyproject.toml               # Package metadata and dependencies
```

## Questions?

Open an issue on GitHub: https://github.com/heysamtexas/django-lead-capture/issues
