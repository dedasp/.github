# GitHub Configuration

This repository contains GitHub workflows and configurations for automated versioning and releases.

## GitHub Workflows

This repository includes two GitHub workflows for maintaining consistent commit standards and automatic versioning:

1. **PR Title Convention Check** - Validates pull request titles follow conventional commit format
2. **Automatic Version Bump** - Creates version tags based on conventional commits when merging into `master`

### PR Title Convention Check

This workflow automatically validates that pull request titles follow the conventional commit format. It runs on every PR (opened, edited, or synchronized) and will fail the check if the title doesn't match the expected format.

**Features:**
- ✅ Validates PR titles against conventional commit patterns
- ✅ Provides helpful error messages with examples
- ✅ Comments on PRs with validation results
- ✅ Fails the check for unconventional titles
- ✅ Supports all conventional commit types and breaking changes

### Automatic Version Bump Workflow

This workflow automatically creates version tags based on conventional commits when merging into the `master` branch.

### How it works

The workflow analyzes commits since the last tag and determines the appropriate version bump:

- **Major version bump** (`v1.0.0` → `v2.0.0`): Breaking changes
  - Commits with `!` after the type: `feat!:`, `fix!:`, etc.
  - Commits with `BREAKING CHANGE:` in the body

- **Minor version bump** (`v1.0.0` → `v1.1.0`): New features
  - Commits with `feat:` type

- **Patch version bump** (`v1.0.0` → `v1.0.1`): Bug fixes and improvements
  - Commits with `fix:`, `perf:`, `refactor:`, `docs:`, `style:`, `test:`, `chore:`, `ci:`, `build:` types

### Conventional Commit Format

Use the following format for your commit messages:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

#### Types:
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools
- `ci`: Changes to CI configuration files and scripts
- `build`: Changes that affect the build system or external dependencies

#### Breaking Changes:
- Add `!` after the type: `feat!:`, `fix!:`
- Or include `BREAKING CHANGE:` in the commit body

### Examples

```bash
# Patch version bump
git commit -m "fix: resolve memory leak in data processing"

# Minor version bump  
git commit -m "feat: add user authentication system"

# Major version bump
git commit -m "feat!: redesign API with new response format"
# or
git commit -m "feat: add new API endpoint

BREAKING CHANGE: The old API endpoint has been removed"
```

### Workflow Features

- ✅ Automatically triggered on pushes to `master`
- ✅ Ignores documentation-only changes (`.md` files)
- ✅ Skips version bump if no conventional commits are found
- ✅ Creates GitHub releases with changelog
- ✅ Supports skipping with `[skip ci]` or `[ci skip]` in commit message

## How Both Workflows Work Together

1. **PR Creation**: When you create a PR, the title check workflow validates the PR title format
2. **PR Review**: The check must pass before the PR can be merged
3. **Merge to Master**: When merged, the version bump workflow analyzes the commits and creates appropriate version tags

This ensures that:
- All PRs have properly formatted titles
- Only conventional commits trigger version bumps
- The versioning system remains consistent and automated

### Setup

1. Ensure your repository has both workflow files:
   - `.github/workflows/pr-title-check.yml` - Validates PR titles
   - `.github/workflows/version-bump.yml` - Creates version tags
2. Make sure your default branch is `master` (or update the workflows to use your default branch)
3. Start using conventional commits in your development workflow
4. Use conventional commit format for PR titles

### Customization

You can customize both workflows by modifying their respective files:

**PR Title Check** (`.github/workflows/pr-title-check.yml`):
- Modify the conventional commit pattern regex
- Change validation rules
- Customize error messages and examples

**Version Bump** (`.github/workflows/version-bump.yml`):
- Change the trigger branch from `master` to your preferred branch
- Modify the conventional commit patterns
- Adjust the version bump logic
- Customize the release notes format
