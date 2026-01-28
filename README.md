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

This repository's `.gitignore` contains:

```
sftp-config.json
```

**Why is `sftp-config.json` ignored?**

`sftp-config.json` is a configuration file typically created by FTP/SFTP deployment tools (like Sublime SFTP plugin) that contains:
- Server connection details (hostname, port)
- Authentication credentials (username, password, SSH keys)
- Remote path mappings
- Upload/download preferences

**This file MUST be ignored** because:
- It contains sensitive connection credentials
- It's environment-specific (each developer may have different server access)
- Including it in version control would expose server credentials to anyone with repository access
- It's a security risk if the repository is public

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
- `sftp-config.json` - Must be configured separately for each deployment environment

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

### Common Files to Ignore for Squarespace Templates

Consider adding these to `.gitignore` if you use them:

```
# SFTP/FTP Configurations
sftp-config.json
.ftpconfig
.deployrc

# IDE/Editor files
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# OS files
.DS_Store
Thumbs.db

# Node modules (if using build tools)
node_modules/

# Logs
*.log
npm-debug.log*

# Environment files
.env
.env.local
```

## Additional Resources

- [Git Documentation - gitignore](https://git-scm.com/docs/gitignore)
- [GitHub's gitignore templates](https://github.com/github/gitignore)
- [Squarespace Developer Platform](https://developers.squarespace.com/)
