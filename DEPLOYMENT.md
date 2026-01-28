# Deployment Guide for CM25 Squarespace Template

## Overview

This repository has been restored to its state from commit f7c2b74 (3 days ago from 2026-01-28). All files now reflect the original template structure.

## Files Restored

The following changes were made to restore the repository:
- ✅ Restored `.gitignore` to original state (contains only `sftp-config.json`)
- ✅ Removed `README.md` (not present in original state)
- ✅ Removed `cm25-f7c2b74cc57bd2f74638fb8b0827b4b9feafd665.zip` (not present in original state)
- ✅ All template files match the f7c2b74 commit state

## Deployment Package

A deployment package (`cm25-deployment-package.tar.gz`) has been created containing all template files. This package can be extracted and uploaded to your Squarespace site via SFTP.

## Deployment Instructions

### Method 1: SFTP Deployment (Recommended)

To deploy this Squarespace template, you need to:

1. **Create SFTP Configuration**
   
   Create a file named `sftp-config.json` in the root directory with your Squarespace site credentials:
   
   ```json
   {
     "type": "sftp",
     "host": "your-site.squarespace.com",
     "username": "your-username",
     "password": "your-password",
     "port": 22,
     "remote_path": "/template",
     "upload_on_save": true
   }
   ```

2. **Install SFTP Plugin**
   
   If using Sublime Text:
   - Install the SFTP package
   - Right-click on the project folder
   - Select "SFTP/FTP" > "Upload Folder"

   If using VS Code:
   - Install the "SFTP" extension by liximomo
   - Create a `.vscode/sftp.json` configuration file
   - Use Command Palette: "SFTP: Upload"

3. **Manual SFTP Upload**
   
   Using command line SFTP:
   ```bash
   sftp username@your-site.squarespace.com
   cd template
   put -r blocks
   put -r collections
   put -r scripts
   put -r styles
   put site.region
   put template.conf
   ```

### Method 2: Squarespace Developer Platform

1. Log in to your Squarespace account
2. Go to Settings > Advanced > Developer Mode
3. Enable Developer Mode
4. Use the provided SFTP credentials to upload files

### What to Deploy

The following files and directories should be deployed:
- `blocks/` - Template blocks
- `collections/` - Collection templates
- `scripts/` - JavaScript files
- `styles/` - LESS stylesheets
- `site.region` - Main site template
- `template.conf` - Template configuration

### What NOT to Deploy

The following are excluded by `.gitignore` and should NOT be deployed:
- `sftp-config.json` - Contains sensitive credentials (keep local only)
- `.git/` - Version control files
- `.gitignore` - Git configuration

## Verification

After deployment, verify that:
1. All template files are present on the Squarespace server
2. The template appears correctly in your Squarespace dashboard
3. The site renders properly with the restored template

## Security Notes

- Never commit `sftp-config.json` to version control
- Keep your SFTP credentials secure
- Use environment-specific configurations for different deployment targets
- Rotate credentials regularly

## Support

For issues with:
- Squarespace templates: Visit https://developers.squarespace.com/
- SFTP deployment: Contact your Squarespace support team
- Template bugs: Open an issue in this repository
