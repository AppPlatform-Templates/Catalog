# NOT OFFICIAL. DO NOT USE
# Contributing to DigitalOcean App Platform Templates

Thank you for your interest in contributing! This document provides guidelines for contributing to the App Platform Templates catalog.

## Ways to Contribute

### 1. Submit a New Template
See [SUBMISSION_GUIDE.md](./SUBMISSION_GUIDE.md) for detailed instructions on submitting templates.

### 2. Improve Existing Templates
- Fix bugs in official templates
- Update dependencies
- Improve documentation
- Add features

### 3. Improve Catalog Documentation
- Fix typos or unclear instructions
- Add examples
- Improve troubleshooting guides
- Update outdated information

### 4. Report Issues
- Template deployment problems
- Documentation errors
- Catalog website issues

---

## Getting Started

### For Template Contributions

1. **Read the guides:**
   - [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md) - How to create templates
   - [SUBMISSION_GUIDE.md](./SUBMISSION_GUIDE.md) - How to submit templates

2. **Check existing templates:**
   - Browse the [catalog](./README.md)
   - Avoid duplicating existing templates
   - Consider improving existing templates instead

3. **Follow requirements:**
   - Templates must deploy successfully
   - Documentation must be complete
   - Code must follow best practices

### For Documentation Contributions

1. **Fork this repository**
2. **Make your changes**
3. **Submit a pull request**

---

## Pull Request Process

### 1. Fork and Clone

```bash
# Fork the repository on GitHub
# Then clone your fork
git clone https://github.com/YOUR-USERNAME/Catalog.git
cd Catalog
```

### 2. Create a Branch

```bash
git checkout -b feature/your-contribution-name
```

**Branch naming:**
- `feature/add-react-template` - New features or templates
- `fix/readme-typo` - Bug fixes
- `docs/improve-submission-guide` - Documentation updates

### 3. Make Your Changes

**For Documentation:**
- Edit the relevant .md files
- Preview your changes locally
- Check for typos and clarity

**For Catalog Updates (adding community templates):**
- Add your template to the appropriate section in README.md
- Include all required information (name, description, link, deploy button)
- Follow the existing table format

### 4. Test Your Changes

**Documentation:**
- Read through your changes
- Check all links work
- Verify markdown renders correctly

**Community Template Submissions:**
- Deploy your template successfully
- Verify the Deploy button works
- Test all documented features

### 5. Commit Your Changes

```bash
git add .
git commit -m "Brief description of your changes"
```

**Commit message guidelines:**
- Use present tense ("Add feature" not "Added feature")
- Be descriptive but concise
- Reference issues if applicable

**Examples:**
```
Add Python FastAPI template to community section
Fix typo in DEVELOPER_GUIDE troubleshooting section
Update Node.js version requirements in documentation
```

### 6. Push and Create Pull Request

```bash
git push origin feature/your-contribution-name
```

Then create a pull request on GitHub with:

**Title:** Brief, descriptive title

**Description:**
```markdown
## Description
Brief explanation of your changes

## Type of Change
- [ ] New template submission
- [ ] Bug fix
- [ ] Documentation update
- [ ] Other (please describe)

## Checklist
- [ ] I have read the DEVELOPER_GUIDE.md
- [ ] My changes follow the project guidelines
- [ ] I have tested my changes
- [ ] Documentation is updated (if needed)

## Additional Notes
Any special considerations or context
```

### 7. Review Process

- A maintainer will review your PR
- You may be asked to make changes
- Once approved, your PR will be merged

---

## Code of Conduct

### Our Standards

**Be respectful:**
- Use welcoming and inclusive language
- Respect differing viewpoints
- Accept constructive criticism gracefully
- Focus on what's best for the community

**Be constructive:**
- Provide helpful feedback
- Suggest improvements
- Help others learn

**Be professional:**
- No harassment, trolling, or insulting comments
- No personal or political attacks
- No publishing others' private information

### Enforcement

Violations may result in:
1. Warning
2. Temporary ban from contributing
3. Permanent ban from the project

Report issues to: [maintainer email or contact method]

---

## Development Workflow

### For Template Developers

1. **Create template in your account** or request repo in AppPlatform-Templates org
2. **Develop following DEVELOPER_GUIDE.md**
3. **Test thoroughly**
4. **Submit via SUBMISSION_GUIDE.md process**
5. **Address review feedback**
6. **Template gets published**

### For Documentation Contributors

1. **Fork catalog repo**
2. **Make improvements**
3. **Submit PR**
4. **Address feedback**
5. **Get merged**

---

## Style Guidelines

### Documentation

**Markdown:**
- Use ATX-style headers (`#` not underlines)
- Include blank lines around headers and code blocks
- Use code fences with language identifiers
- Use tables for structured data

**Writing:**
- Use clear, concise language
- Explain acronyms on first use
- Include examples
- Use active voice
- Be specific, not vague

**Code Examples:**
```javascript
// Good: Specific, clear
const PORT = process.env.PORT || 8080;

// Bad: Vague, unclear
const port = somePort;
```

### Templates

**Code:**
- Follow framework/language conventions
- Use consistent indentation (2 or 4 spaces)
- Include comments for complex logic
- No commented-out code in final submission

**Configuration:**
- YAML files: 2-space indentation
- JSON files: 2-space indentation
- Consistent naming conventions

---

## Testing Requirements

### Before Submitting

**Templates:**
- [ ] Deploys successfully via Deploy button
- [ ] All features work post-deployment
- [ ] No errors in application logs
- [ ] Health checks pass (if applicable)
- [ ] Environment variables work correctly
- [ ] Costs match estimates

**Documentation:**
- [ ] All links work
- [ ] Code examples are correct
- [ ] Instructions are clear and complete
- [ ] Markdown renders correctly

---

## Questions?

**General Questions:**
- Open a [Discussion](https://github.com/AppPlatform-Templates/Catalog/discussions)

**Specific Issues:**
- Open an [Issue](https://github.com/AppPlatform-Templates/Catalog/issues)

**Template Help:**
- See [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md) Troubleshooting section
- Open an issue in the template's repository

---

## Recognition

Contributors will be:
- Listed in template README (for template authors)
- Credited in commit history
- Mentioned in release notes (for significant contributions)
- Featured in community highlights (occasionally)

---

## License

By contributing, you agree that your contributions will be licensed under the same license as the project (typically MIT for templates).

---

**Thank you for contributing!** Your efforts help the entire DigitalOcean and developer community. We appreciate your time and expertise.