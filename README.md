# CM25 - Squarespace Template

This is a Squarespace template based on the Pacific theme.

## Understanding .gitignore

### What is .gitignore?

`.gitignore` is a configuration file used by Git to specify which files and directories should be **intentionally ignored** and not tracked by version control. When files are listed in `.gitignore`, they will not be:

- Staged for commits
- Tracked by Git
- Pushed to remote repositories (like GitHub)
- Visible in `git status` as untracked files

### Purpose of .gitignore

The `.gitignore` file helps keep your repository clean by excluding:

1. **Sensitive information** - API keys, passwords, credentials
2. **Environment-specific files** - Local configuration files
3. **Build artifacts** - Compiled files, minified assets
4. **Dependencies** - Libraries that can be re-downloaded (node_modules, vendor folders)
5. **IDE/Editor files** - Personal editor settings and caches
6. **Operating system files** - .DS_Store (macOS), Thumbs.db (Windows)
7. **Temporary files** - Logs, caches, temporary build files

### Current .gitignore Configuration

This repository's `.gitignore` has been configured with comprehensive patterns to exclude:

1. **SFTP/FTP Configuration files** - `sftp-config.json`, `.ftpconfig`, `.deployrc`
   - These contain sensitive server credentials and connection details
   - Must be kept private and configured per environment

2. **IDE/Editor files** - `.vscode/`, `.idea/`, `*.sublime-project`, etc.
   - Personal development environment preferences
   - Should not be shared across team members

3. **Operating System files** - `.DS_Store` (macOS), `Thumbs.db` (Windows)
   - OS-specific metadata files
   - Not relevant to the project

4. **Build artifacts** - `node_modules/`, `dist/`, `build/`
   - Generated files that can be recreated
   - Keeps repository size minimal

5. **Environment files** - `.env`, `.env.local`
   - Contains environment-specific configuration
   - May include sensitive data

6. **Logs and temporary files** - `*.log`, `*.tmp`, `.cache/`
   - Runtime generated files
   - Not needed in version control

**Key Security Protection:**

The most critical exclusion is `sftp-config.json` because it typically contains:
- Server connection details (hostname, port)
- Authentication credentials (username, password, SSH keys)
- Remote path mappings

Including this file in version control would expose deployment credentials to anyone with repository access.

## Impact on Deployment

### How .gitignore Affects Deployment

The `.gitignore` file has **direct and important impacts** on deployment:

#### 1. **Security Protection**
- Prevents accidental commits of credentials (like `sftp-config.json`)
- Protects API keys, passwords, and sensitive configuration
- Reduces security vulnerabilities in production

#### 2. **Repository Size**
- Keeps repository lightweight by excluding build artifacts
- Faster clone and pull operations
- Reduces storage costs

#### 3. **Deployment Process**
- Files in `.gitignore` are **not included** in the repository
- Deployment systems that pull from Git won't receive ignored files
- You may need to:
  - Recreate configuration files on the deployment server
  - Build/compile assets as part of the deployment process
  - Set environment variables separately

#### 4. **What Gets Deployed**

For this Squarespace template:

**✅ INCLUDED in version control and deployment:**
- Template files (`site.region`)
- Configuration (`template.conf`)
- Block templates (`blocks/*.block`)
- Collection templates (`collections/*`)
- Stylesheets (`styles/*.less`, `*.css`)
- JavaScript files (`scripts/*.js`)

**❌ EXCLUDED from version control (in .gitignore):**
- `sftp-config.json` and other SFTP/FTP config files - Must be configured separately for each deployment environment
- IDE/Editor files (`.vscode/`, `.idea/`, etc.) - Personal development environment settings
- OS files (`.DS_Store`, `Thumbs.db`) - Operating system metadata
- `node_modules/` - Dependencies (if using build tools)
- Environment files (`.env`) - Environment-specific configuration
- Build artifacts (`dist/`, `build/`) - Generated files
- Logs and temporary files - Runtime generated content

### Deployment Workflow for Squarespace Templates

1. **Developer Setup:**
   - Clone the repository
   - Create your own `sftp-config.json` with your Squarespace site credentials
   - The file stays local (not committed due to `.gitignore`)

2. **Code Changes:**
   - Make changes to template files, styles, scripts
   - Commit and push changes to Git
   - `.gitignore` ensures credentials stay private

3. **Deployment:**
   - Use SFTP tool to upload files to Squarespace
   - Or use Git-based deployment if configured
   - Only tracked files are deployed

### Best Practices

1. **Keep sensitive data out of Git** - Use `.gitignore` for all credentials
2. **Document required files** - If deployment needs files that are ignored, document how to create them
3. **Use environment variables** - For configuration that changes between environments
4. **Review .gitignore regularly** - Ensure it includes all necessary exclusions
5. **Never commit then ignore** - If a file is already tracked, `.gitignore` won't remove it

### What's Already in .gitignore

The `.gitignore` file in this repository already includes comprehensive patterns for:

- **SFTP/FTP Configurations** - `sftp-config.json`, `.ftpconfig`, `.deployrc`
- **IDE/Editor files** - `.vscode/`, `.idea/`, `*.sublime-project`, `*.sublime-workspace`, etc.
- **OS files** - `.DS_Store`, `Thumbs.db`, and other OS-specific metadata
- **Node modules** - `node_modules/` (if using build tools)
- **Logs** - `*.log`, `npm-debug.log*`, `yarn-debug.log*`
- **Environment files** - `.env`, `.env.local`, `.env.*.local`
- **Build artifacts** - `dist/`, `build/`
- **Temporary files** - `*.tmp`, `.cache/`

You can view the complete `.gitignore` file in the repository root to see all exclusion patterns.

## Additional Resources

- [Git Documentation - gitignore](https://git-scm.com/docs/gitignore)
- [GitHub's gitignore templates](https://github.com/github/gitignore)
- [Squarespace Developer Platform](https://developers.squarespace.com/)
