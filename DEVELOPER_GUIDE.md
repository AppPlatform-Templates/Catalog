# NOT OFFICIAL. DO NOT USE
# Developer Guide: Creating DigitalOcean App Platform Templates

This comprehensive guide walks you through creating, testing, and maintaining templates for the DigitalOcean App Platform.

## Table of Contents

- [Overview](#overview)
- [Template Structure](#template-structure)
- [Creating a New Template](#creating-a-new-template)
- [Deploy Configuration](#deploy-configuration)
- [Testing Your Template](#testing-your-template)
- [Documentation Requirements](#documentation-requirements)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

## Overview

Each template is a **standalone repository** containing a complete, deployable application. Templates demonstrate specific stacks, frameworks, or use cases with production-ready configurations.

### What Makes a Good Template?

-  **Complete**: Includes all code, configuration, and documentation needed to deploy
-  **Production-Ready**: Uses secure defaults and follows best practices
-  **Well-Documented**: Clear README with prerequisites, costs, and usage instructions
-  **Tested**: Successfully deploys to DigitalOcean App Platform
-  **Maintained**: Uses current, stable versions of dependencies
-  **Self-Contained**: Lives in its own repository with `.do/deploy.template.yaml` at root

## Template Structure

Each template repository must follow this structure:

```
YourTemplate-Repository/
 README.md                      # Required: Template documentation + Deploy button
 .do/
    deploy.template.yaml      # Required: At repository root!
 [application files]            # Your app code (index.js, app.py, etc.)
 .gitignore                    # Recommended: Ignore build artifacts, secrets
 .env.example                  # Optional: Example environment variables
 [other config files]          # package.json, requirements.txt, Dockerfile, etc.
```

**Critical**: `.do/deploy.template.yaml` **MUST** be at the repository root for the Deploy button to work.

### Naming Conventions

**Repository Names:**
- Use PascalCase with Template suffix: `HelloWorld-Template`, `ReactBlog-Template`
- Clear and descriptive: `WordPress-MySQL-Template` not `WP-DB`
- Include primary technology: `PythonFlask-API-Template`

**Examples:**
- `HelloWorld-Template` (Node.js)
- `ReactStaticSite-Template`
- `DjangoPostgres-Template`
- `GoAPI-Template`

## Creating a New Template

### Step 1: Create Your Repository

```bash
# Create a new repository in the AppPlatform-Templates org (or your account for community templates)
# Repository name: YourApp-Template
```

### Step 2: Create Directory Structure

```bash
cd YourApp-Template
mkdir .do
touch README.md .do/deploy.template.yaml .env.example .gitignore
```

### Step 3: Develop Your Application

Create your application code following best practices for your stack:

**Node.js:**
```bash
npm init -y
npm install express
# Create index.js, configure package.json
```

**Python:**
```bash
pip install -r requirements.txt
# Create app.py, requirements.txt
```

**Go:**
```bash
go mod init your-app
# Create main.go, go.mod
```

**Important Application Requirements:**
-  Listen on port from `PORT` environment variable (App Platform sets this)
-  Handle graceful shutdowns (SIGTERM, SIGINT)
-  Include health check endpoints (`/health` recommended)
-  Use environment variables for all configuration
-  Never hardcode secrets or API keys

**Example (Node.js):**
```javascript
const PORT = process.env.PORT || 8080;
app.listen(PORT, '0.0.0.0', () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Step 4: Create Deployment Configuration

Create `.do/deploy.template.yaml`:

```yaml
spec:
  name: your-app-name
  services:
    - name: web
      environment_slug: node-js  # Options: node-js, python, go, php, ruby, docker, static
      git:
        branch: main
        repo_clone_url: https://github.com/AppPlatform-Templates/YourTemplate-Repository.git
      http_port: 8080
      instance_count: 1
      instance_size_slug: basic-xxs
      routes:
        - path: /
      run_command: npm start  # Adjust for your stack: python app.py, go run main.go, etc.
      envs:
        - key: NODE_ENV
          scope: RUN_TIME
          value: "production"
        # Add required environment variables with placeholder values
        - key: API_KEY
          scope: RUN_TIME
          value: "your-api-key-here"  # Users will be prompted to fill this
```

**Key Fields Explained:**

| Field | Description | Required |
|-------|-------------|----------|
| `spec` | Root wrapper (MUST be present) | Yes |
| `name` | App name (lowercase, hyphens) | Yes |
| `environment_slug` | Runtime environment | Yes |
| `git.branch` | Git branch to deploy from | Yes |
| `git.repo_clone_url` | Full repository URL | Yes |
| `http_port` | Port your app listens on | Yes (for web services) |
| `instance_size_slug` | Resource tier (basic-xxs, basic-xs, etc.) | Yes |
| `run_command` | Command to start your app | Yes |
| `envs` | Environment variables | Optional |

**Important Notes:**
- � Use `git:` field, **NOT** `github:` (common mistake!)
- � Do NOT use `source_dir` for standalone repos (only needed for monorepos)
- � Do NOT include `deploy_on_push` in deploy templates

### Step 5: Create Template Documentation

Your `README.md` should include:

```markdown
# Your Template Name

Brief description of what this template does.

[![Deploy to DO](https://www.deploytodo.com/do-btn-blue.svg)](https://cloud.digitalocean.com/apps/new?repo=https://github.com/AppPlatform-Templates/YourTemplate-Repository/tree/main)

## What This Template Includes

- Feature 1
- Feature 2
- Feature 3

## Tech Stack

- **Runtime**: Node.js 20.x (or your stack)
- **Framework**: Express 4.x
- **Database**: PostgreSQL 15 (if applicable)

## Prerequisites

- DigitalOcean account
- [Any other requirements]

## Estimated Cost

- **Compute**: Basic XXS - $5/month
- **Database**: Dev tier - $7/month (if applicable)
- **Total**: ~$12/month

## Deployment Instructions

1. Click the "Deploy to DigitalOcean" button above
2. Authorize DigitalOcean to access the repository
3. Configure environment variables:
   - `VAR_NAME`: Description of what it does
4. Click "Deploy"
5. Wait 2-5 minutes for deployment

## Post-Deployment

Your app will be available at: `https://your-app-name-xxxxx.ondigitalocean.app`

[Any post-deployment configuration steps]

## Local Development

\`\`\`bash
git clone https://github.com/AppPlatform-Templates/YourTemplate-Repository.git
cd YourTemplate-Repository
npm install
cp .env.example .env
# Edit .env with your values
npm start
\`\`\`

## Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| VAR_NAME | What it does | Yes | N/A |

## Features

- List key features
- Of your application

## License

MIT License
```

### Step 6: Add .gitignore

Create appropriate `.gitignore`:

**Node.js:**
```gitignore
node_modules/
npm-debug.log
.env
.env.local
dist/
build/
```

**Python:**
```gitignore
__pycache__/
*.py[cod]
venv/
.env
*.sqlite
```

**Go:**
```gitignore
*.exe
*.test
vendor/
.env
```

## Deploy Configuration

### Environment Slugs

Choose the correct environment for your stack:

- `node-js` - Node.js applications
- `python` - Python applications
- `go` - Go applications
- `php` - PHP applications
- `ruby` - Ruby applications
- `docker` - Custom Dockerfile
- `static` - Static sites (HTML, React build, etc.)

### Instance Sizing

| Slug | RAM | vCPU | Cost | Use Case |
|------|-----|------|------|----------|
| `basic-xxs` | 512MB | 1 | $5/mo | Simple apps, APIs |
| `basic-xs` | 1GB | 1 | $12/mo | Medium apps |
| `basic-s` | 2GB | 2 | $24/mo | Larger apps |
| `professional-xs` | 1GB | 1 | $12/mo | High availability |

Start with `basic-xxs` for most templates.

### Environment Variables

**For Required Variables:**
```yaml
envs:
  - key: DATABASE_URL
    scope: RUN_TIME
    value: "${db.DATABASE_URL}"  # Auto-populated if using App Platform database
  - key: API_KEY
    scope: RUN_TIME
    value: "your-api-key-here"  # User will be prompted
```

**For Optional Variables with Defaults:**
```yaml
envs:
  - key: NODE_ENV
    scope: RUN_TIME
    value: "production"
  - key: LOG_LEVEL
    scope: RUN_TIME
    value: "info"
```

## Testing Your Template

### Pre-Deployment Testing

1. **Test Locally:**
   ```bash
   # Test your app runs correctly
   npm start  # or python app.py, go run main.go, etc.

   # Test it responds on PORT env var
   PORT=3000 npm start
   ```

2. **Validate YAML:**
   ```bash
   # Check YAML syntax
   python -c "import yaml; yaml.safe_load(open('.do/deploy.template.yaml'))"
   ```

3. **Check Critical Requirements:**
   - [ ] `.do/deploy.template.yaml` at repository root
   - [ ] `spec:` wrapper present in YAML
   - [ ] `git:` field used (not `github:`)
   - [ ] App listens on `PORT` environment variable
   - [ ] README includes Deploy button
   - [ ] All secrets use environment variables

### Deployment Testing

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Add template"
   git push origin main
   ```

2. **Test Deploy Button:**
   - Click your own Deploy button
   - Verify configuration loads correctly
   - Complete deployment
   - Test all features work
   - Check logs for errors

3. **Verify Functionality:**
   - All endpoints respond correctly
   - Environment variables work
   - Database connections succeed (if applicable)
   - Health checks pass

4. **Clean Up:**
   - Delete test deployment from App Platform dashboard
   - Verify no lingering resources (databases, etc.)

## Documentation Requirements

### Required Files

1. **README.md** - Template documentation:
   - Deploy button at top
   - Clear description
   - Tech stack and versions
   - Cost estimates
   - Deployment instructions
   - Environment variables table
   - Local development guide

2. **.do/deploy.template.yaml** - Deployment configuration:
   - Must be at repository root
   - Valid YAML syntax
   - Correct `git:` field usage
   - All required fields present

3. **.gitignore** - Ignore patterns:
   - Dependencies (node_modules, venv, vendor)
   - Build artifacts
   - Environment files (.env)
   - IDE files

### Recommended Files

- `.env.example` - Example environment variables
- `LICENSE` - License information (MIT recommended)
- `CHANGELOG.md` - Version history (for maintained templates)

## Troubleshooting

This section contains solutions to common issues discovered during template development and deployment.

### Deploy Button Issues

#### Issue: "Your Git template URL must match one of the following"

**Symptoms:**
- Deploy button shows validation error
- Branch name is shown in error message

**Cause:**
- Branch names with forward slashes (e.g., `feature/xyz`, `claude/test`) break DigitalOcean's URL validation
- This is a known limitation of the Deploy button

**Solution:**
```bash
# Use simple branch names without slashes
git checkout -b main  #  Good
git checkout -b my-feature  #  Good
git checkout -b feature/xyz  # L Breaks Deploy button
```

**Workarounds Tested (None worked):**
- L URL encoding (`%2F`) - Rejected by validation
- L Escaped slashes in YAML (`claude\/branch`) - Doesn't help
- L Quoted branch names in YAML - No effect

**Best Practice:** Always use `main` or simple branch names for deployable branches.

---

#### Issue: Deploy button doesn't find template

**Symptoms:**
- Clicking Deploy button shows error
- "Could not find .do/deploy.template.yaml"

**Cause:**
- `.do/deploy.template.yaml` not at repository root
- File in subdirectory (e.g., `templates/app/.do/deploy.template.yaml`)

**Solution:**
```bash
# Ensure file is at root
ls -la .do/deploy.template.yaml  # Must be at root, not in subdirectory
```

**For Monorepos:**
If you must use subdirectories, add `source_dir`:
```yaml
spec:
  services:
    - name: web
      source_dir: /templates/your-app  # Points to subdirectory
```

**Best Practice:** Use one repository per template for simplest deployment.

---

### Configuration Issues

#### Issue: "Invalid configuration" or "Failed to parse app spec"

**Symptoms:**
- Deploy fails immediately
- Error mentions YAML parsing or invalid spec

**Cause 1: Using `github:` instead of `git:`**

**Wrong:**
```yaml
services:
  - name: web
    github:  # L Wrong!
      branch: main
      repo_clone_url: https://github.com/...
```

**Correct:**
```yaml
services:
  - name: web
    git:  #  Correct!
      branch: main
      repo_clone_url: https://github.com/...
```

**Cause 2: Missing `spec:` wrapper**

**Wrong:**
```yaml
name: my-app  # L Missing spec: wrapper
services:
  - name: web
```

**Correct:**
```yaml
spec:  #  Must have spec: wrapper
  name: my-app
  services:
    - name: web
```

**Cause 3: Invalid YAML syntax**

```bash
# Validate your YAML
python -c "import yaml; print(yaml.safe_load(open('.do/deploy.template.yaml')))"
```

---

### Build and Runtime Issues

#### Issue: Build fails - "Command not found"

**Symptoms:**
- Build logs show command not found
- Deployment fails during build phase

**Cause:**
- Incorrect `run_command` for your stack
- Missing dependencies in build

**Solution:**

**Check your run_command matches your package manager:**
```yaml
# Node.js
run_command: npm start  # Must match package.json scripts.start

# Python
run_command: python app.py  # Or gunicorn app:app

# Go
run_command: ./main  # After build: go build -o main

# Static site
# No run_command needed for static sites
```

---

#### Issue: App crashes on startup

**Symptoms:**
- App builds successfully but crashes immediately
- Logs show "Address already in use" or "Cannot bind to port"

**Cause:**
- App not listening on `PORT` environment variable
- Hardcoded port number

**Wrong:**
```javascript
app.listen(3000);  // L Hardcoded port
```

**Correct:**
```javascript
const PORT = process.env.PORT || 8080;
app.listen(PORT, '0.0.0.0');  //  Uses environment PORT
```

**Python:**
```python
import os
port = int(os.environ.get('PORT', 8080))
app.run(host='0.0.0.0', port=port)
```

**Go:**
```go
port := os.Getenv("PORT")
if port == "" {
    port = "8080"
}
http.ListenAndServe(":"+port, nil)
```

---

#### Issue: Environment variables not working

**Symptoms:**
- App can't read environment variables
- Features requiring config don't work

**Cause:**
- Variables not defined in deploy.template.yaml
- Incorrect scope

**Solution:**
```yaml
envs:
  - key: DATABASE_URL
    scope: RUN_TIME  # Available at runtime
    value: "${db.DATABASE_URL}"

  - key: API_KEY
    scope: RUN_TIME
    value: "placeholder"  # User will be prompted

  - key: BUILD_FLAG
    scope: BUILD_TIME  # Only available during build
    value: "production"
```

**Scopes:**
- `RUN_TIME` - Available when app runs (most common)
- `BUILD_TIME` - Available during build only
- `RUN_AND_BUILD_TIME` - Available in both

---

### Testing and Debugging

#### Issue: Can't test Deploy button locally

**Reality:**
- Deploy button requires GitHub repository
- No local testing possible

**Solution:**
```bash
# Must push to GitHub first
git push origin main

# Then test the button from GitHub
# Or use direct URL:
https://cloud.digitalocean.com/apps/new?repo=https://github.com/YOUR_ORG/YOUR_REPO/tree/main
```

---

#### Issue: Need to test changes without creating new app

**Solution 1: Update existing app**
- Deploy once
- Make changes and push to GitHub
- App Platform auto-redeploys (if deploy_on_push enabled)

**Solution 2: Use App Platform UI**
- Create app without Deploy button
- Manually configure from UI
- Test deployment
- Export to YAML for deploy.template.yaml

---

### Common Mistakes Checklist

Before asking for help, verify:

- [ ] `.do/deploy.template.yaml` is at repository root (not in subdirectory)
- [ ] File starts with `spec:` wrapper
- [ ] Using `git:` field (not `github:`)
- [ ] `repo_clone_url` is correct and accessible
- [ ] Branch name has no forward slashes
- [ ] App listens on `process.env.PORT` (or equivalent)
- [ ] All required environment variables defined
- [ ] YAML syntax is valid
- [ ] `run_command` matches your start script
- [ ] Dependencies are properly declared
- [ ] No secrets hardcoded in code

---

## Best Practices

### Security

-  Never commit secrets, API keys, or passwords
-  Use environment variables for all sensitive data
-  Include comprehensive `.gitignore`
-  Use latest stable versions of dependencies
-  Enable HTTPS (automatic with App Platform)
-  Implement rate limiting for APIs
-  Validate all user input
-  Use security headers

### Performance

-  Optimize Docker images (use multi-stage builds)
-  Minimize dependencies
-  Enable caching where appropriate
-  Use CDN for static assets (automatic)
-  Implement health checks
-  Set appropriate resource limits

### Maintainability

-  Pin dependency versions
-  Document breaking changes
-  Use semantic versioning for releases
-  Follow framework conventions
-  Include linting/formatting configs
-  Write clear, concise code comments

### Cost Optimization

-  Start with smallest instance size that works
-  Use static sites for frontends when possible
-  Implement auto-scaling only if needed
-  Document actual resource requirements
-  Provide accurate cost estimates

---

## Need Help?

- **Catalog Issues**: [Open an issue](https://github.com/AppPlatform-Templates/Catalog/issues)
- **Template Issues**: Open issue in specific template repository
- **App Platform Docs**: https://docs.digitalocean.com/products/app-platform/
- **Community**: https://www.digitalocean.com/community

---

**Ready to create a template?** Follow this guide step-by-step, and don't forget to check the [Troubleshooting](#troubleshooting) section if you encounter issues!