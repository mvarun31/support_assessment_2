# Python Package with GitHub Actions Workflows

This repository contains a basic Python package structure along with three GitHub Actions workflows for automating the build, release, and promotion of packages to Cloudsmith.

## Project Structure

```
.github/
├── workflows/
│   ├── build_package.yml
│   ├── promote_package.yml
│   ├── release_package.yml
src/
├── example_package/
│   ├── __init__.py
│   ├── example.py
README.md
pyproject.toml
```

## Workflows

### 1. Build Package Workflow (`build_package.yml`)
This workflow is triggered on `push` and `pull_request` events to the `main` branch. It:
- Checks out the code
- Sets up Python
- Installs dependencies
- Builds the package
- Uploads the package artifact

### 2. Release Package Workflow (`release_package.yml`)
Triggered upon successful completion of the build workflow, it:
- Downloads the built package
- Installs Cloudsmith CLI
- Uploads the package to the Cloudsmith staging repository

### 3. Promote Package Workflow (`promote_package.yml`)
Manually triggered via `workflow_dispatch`, it:
- Tags a package as "ready-for-production"
- Lists packages tagged as "ready-for-production"
- Promotes them from staging to production in Cloudsmith

## Cloudsmith Environment Variables
This repository uses GitHub Actions environment variables to manage Cloudsmith uploads:
- `CLOUDSMITH_NAMESPACE`: The Cloudsmith namespace
- `CLOUDSMITH_REPOSITORY`: Target repository (e.g., `staging`)
- `CLOUDSMITH_SERVICE_SLUG`: Cloudsmith service slug

## Running Workflows
- The build workflow runs automatically on `push` and `pull_request`
- The release workflow runs after a successful build
- The promote workflow must be triggered manually

## License
This project is licensed under the MIT License.
