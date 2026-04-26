# How to Release Helm Charts Using cr.sh

This document explains how to manually release Helm charts using the `cr.sh` script, without relying on GitHub Actions.

## Prerequisites
- You have a GitHub repository for your Helm charts.
- You have [chart-releaser](https://github.com/helm/chart-releaser) installed, or you let `cr.sh` handle the installation.
- You have a valid GitHub token with `repo` permissions, exported as the environment variable `CR_TOKEN`.
- Your local git remote is set to HTTPS (e.g., `https://github.com/yourname/yourrepo.git`).

## Steps

### 1. Set Up Your Environment
Export your GitHub token:

```bash
export CR_TOKEN=your_github_token
# Rename the cr.sh file
mv cr.sh.template cr.sh
```

### 2. Prepare Your Repository
Make sure your Helm charts are organized in a directory (e.g., `helm-chart/`).

### 3. Run cr.sh
Use the following command to release your Helm charts:

```bash
./cr.sh --owner <github-username-or-org> --repo <repo-name> --charts-dir <charts-directory>
```

**Example:**

```bash
./cr.sh --owner amyinfo --repo gh-pages --charts-dir ./helm-chart/
```

- `--owner`: Your GitHub username or organization name.
- `--repo`: The name of your GitHub repository.
- `--charts-dir`: The directory containing your Helm charts (default is `charts`).

### 4. What Happens Next
- The script will package all changed charts in the specified directory.
- It will create or update GitHub releases for the charts.
- It will update the `index.yaml` file in your repository's `gh-pages` branch.

### 5. Notes
- Make sure your git remote is set to HTTPS, not SSH. Example:
  ```bash
  git remote set-url origin https://github.com/amyinfo/gh-pages.git
  ```
- The script will automatically install the chart-releaser binary in a local directory if not present.
- You can pass additional options as needed (see `./cr.sh --help`).

## Troubleshooting
- If you see errors about remote URLs, ensure your git remote uses HTTPS.
- If you see authentication errors, check that `CR_TOKEN` is set and has the correct permissions.
- For more options, run:
  ```bash
  ./cr.sh --help
  ```

---
For more details, see the [chart-releaser documentation](https://github.com/helm/chart-releaser).
