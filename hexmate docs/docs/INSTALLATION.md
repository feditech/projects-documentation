# Installation Guide

This guide provides detailed instructions for installing and setting up HexMate on your local development environment.

## Table of Contents

- [System Requirements](#system-requirements)
- [Prerequisites](#prerequisites)
- [Installation Steps](#installation-steps)
- [Configuration](#configuration)
- [Verification](#verification)
- [Troubleshooting](#troubleshooting)

## System Requirements

### Hardware Requirements

**Minimum:**
- 4 GB RAM
- 2 GB free disk space
- Dual-core processor

**Recommended:**
- 8 GB RAM or more
- 5 GB free disk space
- Quad-core processor

### Operating System

HexMate can be installed on:
- Windows 10/11
- macOS 10.15 or later
- Linux (Ubuntu 18.04+, Debian 10+, CentOS 7+, or equivalent)

### Browser Requirements

For development and testing:
- Chrome 90+ (recommended)
- Firefox 88+
- Safari 14+
- Edge 90+

## Prerequisites

### 1. Node.js and npm

HexMate requires Node.js version 16 or higher and npm version 7 or higher.

#### Check Current Version

```bash
node --version
npm --version
```

#### Install Node.js

**Windows/macOS:**
1. Download installer from [nodejs.org](https://nodejs.org/)
2. Run the installer
3. Follow the installation wizard

**Linux (Ubuntu/Debian):**
```bash
# Install Node.js 18.x
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Linux (CentOS/RHEL):**
```bash
# Install Node.js 18.x
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs
```

**Verify Installation:**
```bash
node --version  # Should show v16.x.x or higher
npm --version   # Should show 7.x.x or higher
```

### 2. Git

Git is required to clone the repository.

#### Check Current Version

```bash
git --version
```

#### Install Git

**Windows:**
Download from [git-scm.com](https://git-scm.com/download/win)

**macOS:**
```bash
# Using Homebrew
brew install git

# Or install Xcode Command Line Tools
xcode-select --install
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt-get install git

# CentOS/RHEL
sudo yum install git
```

## Installation Steps

### Step 1: Clone the Repository

```bash
# Using HTTPS
git clone https://github.com/feditech/hexmate.git

# Or using SSH (if you have SSH keys set up)
git clone git@github.com:feditech/hexmate.git

# Navigate to the project directory
cd hexmate
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install all required dependencies listed in `package.json`. The installation may take several minutes depending on your internet connection.

**Note:** You may see some warnings about deprecated packages or vulnerabilities. These are generally from transitive dependencies and are being addressed in future updates.

### Step 3: Create Environment Configuration

Create a `.env` file in the root directory of the project:

```bash
# Create .env file
touch .env
```

Add the following content to `.env`:

```env
# API Configuration
REACT_APP_BASE_API=https://your-api-endpoint.com/api/

# Optional: Public URL for deployment
# PUBLIC_URL=/hexmate
```

**Important:** Replace `https://your-api-endpoint.com/api/` with your actual backend API endpoint.

### Step 4: Configure Modules

The module configuration is located in `public/config.json`. The default configuration includes all three modules:

```json
{
  "modules": [
    {
      "id": 1,
      "name": "DMS",
      "link": "/dms/documents"
    },
    {
      "id": 2,
      "name": "CTS",
      "link": "/cts/dashboard"
    },
    {
      "id": 3,
      "name": "VMS",
      "link": "/vms/dashboard"
    }
  ],
  "signatureScale": 0.5
}
```

You can modify this file to:
- Enable/disable specific modules
- Change default landing pages
- Adjust signature scaling

### Step 5: Verify Installation

Run the development server to verify the installation:

```bash
npm start
```

The application should start and automatically open in your default browser at:
```
http://localhost:3000
```

You should see the HexMate login page.

## Configuration

### Environment Variables

HexMate supports the following environment variables in `.env`:

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `REACT_APP_BASE_API` | Backend API base URL | Yes | - |
| `PUBLIC_URL` | Public URL path for deployment | No | `/` |

### Module Configuration

Edit `public/config.json` to configure available modules:

```json
{
  "modules": [
    // Enable only DMS module
    {
      "id": 1,
      "name": "DMS",
      "link": "/dms/documents"
    }
  ]
}
```

### Development vs Production

#### Development Mode

```bash
npm start
```

- Hot module reloading enabled
- Source maps enabled
- Unminified code for debugging
- Development server on port 3000

#### Production Build

```bash
npm run build
```

- Code minification
- Tree shaking
- Optimized bundle size
- Source maps (optional)

## Verification

### 1. Check Dependencies

Verify all dependencies are installed:

```bash
npm list --depth=0
```

### 2. Run Tests

```bash
npm test
```

Press `a` to run all tests. All tests should pass.

### 3. Build the Application

```bash
npm run build
```

Check that the build completes successfully and creates a `build` folder.

### 4. Verify API Connection

1. Start the development server: `npm start`
2. Open browser to `http://localhost:3000`
3. Open browser console (F12)
4. Check for any API connection errors

## Post-Installation

### Setting Up Your Backend

HexMate requires a backend API server. Ensure that:

1. Your backend server is running
2. The API endpoint in `.env` is correct
3. CORS is properly configured on the backend
4. API authentication is set up

### Initial Login

The default credentials depend on your backend setup. Contact your system administrator for:
- Initial admin username
- Initial admin password
- System configuration details

### User Setup

After logging in as admin:

1. Navigate to User Management
2. Create user accounts
3. Assign modules to users
4. Configure user groups and roles
5. Set up user permissions

## Troubleshooting

### Common Issues

#### 1. npm install fails

**Error:** `npm ERR! code EACCES`

**Solution:**
```bash
# Fix npm permissions
sudo chown -R $USER:$(id -gn $USER) ~/.npm
npm install
```

#### 2. Port 3000 already in use

**Solution:**
```bash
# Use a different port
PORT=3001 npm start
```

Or kill the process using port 3000:
```bash
# macOS/Linux
lsof -ti:3000 | xargs kill -9

# Windows
netstat -ano | findstr :3000
taskkill /PID [PID] /F
```

#### 3. Module not found errors

**Solution:**
```bash
# Clear npm cache and reinstall
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

#### 4. Can't connect to API

**Checklist:**
- Verify `.env` file exists and contains correct API URL
- Check that backend server is running
- Verify network connectivity
- Check browser console for specific error messages
- Ensure CORS is configured on backend

#### 5. Build fails with memory errors

**Solution:**
```bash
# Increase Node memory limit
NODE_OPTIONS="--max-old-space-size=4096" npm run build
```

### Getting Help

If you encounter issues not covered here:

1. Check [Troubleshooting Guide](TROUBLESHOOTING.md)
2. Search existing [GitHub Issues](https://github.com/feditech/hexmate/issues)
3. Create a new issue with:
   - Operating system and version
   - Node.js and npm versions
   - Complete error message
   - Steps to reproduce

## Next Steps

After successful installation:

1. Read the [Configuration Guide](CONFIGURATION.md)
2. Review [Development Guide](DEVELOPMENT.md)
3. Check module-specific documentation:
   - [DMS Documentation](DMS.md)
   - [CTS Documentation](CTS.md)
   - [VMS Documentation](VMS.md)
4. Review [Security Best Practices](SECURITY.md)

## Updating HexMate

To update to the latest version:

```bash
# Pull latest changes
git pull origin main

# Install any new dependencies
npm install

# Rebuild
npm run build
```

**Note:** Always backup your `.env` file and `public/config.json` before updating.
