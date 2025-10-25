# NOT OFFICIAL. DO NOT USE

# Template Submission Guide

Thank you for your interest in contributing to the DigitalOcean App Platform Templates catalog! This guide explains how to submit templates to the catalog.

## Two Ways to Contribute

### 1. Official Templates (Hosted in AppPlatform-Templates org)

Official templates are maintained by DigitalOcean and trusted contributors. They undergo thorough review and become part of the officially supported collection.

**Best for:**
- Core templates (common frameworks, databases)
- Templates you want DigitalOcean to maintain long-term
- Reference implementations

**Process:** See [Official Template Submission](#official-template-submission) below

### 2. Community Templates (Hosted in your account)

Community templates remain in your GitHub account. You maintain ownership and are responsible for updates. The catalog links to your repository.

**Best for:**
- Specialized use cases
- Your company's stack
- Experimental or niche templates
- When you want to keep ownership

**Process:** See [Community Template Submission](#community-template-submission) below

---

## Official Template Submission

### Prerequisites

Before submitting:

- [ ] Read the [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md) completely
- [ ] Your template follows all requirements
- [ ] You've successfully tested deployment multiple times
- [ ] Documentation is complete and accurate
- [ ] You're willing to transfer repository ownership to AppPlatform-Templates org

### Quality Requirements

Official templates must meet these standards:

**Code Quality:**
-  Production-ready code
-  Follows framework best practices
-  Includes error handling
-  No hardcoded secrets or credentials
-  Comprehensive comments where needed

**Security:**
-  Uses latest stable versions of dependencies
-  No known security vulnerabilities
-  Proper input validation
-  Security headers configured
-  Environment variables for all secrets

**Documentation:**
-  Comprehensive README with Deploy button
-  Clear deployment instructions
-  Accurate cost estimates
-  Environment variables documented
-  Local development guide
-  Troubleshooting section

**Testing:**
-  Successfully deploys via Deploy button
-  All features work post-deployment
-  No errors in application logs
-  Health checks pass
-  Resource usage is appropriate

### Submission Process

#### Step 1: Prepare Your Template

1. Create repository following [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md)
2. Test deployment thoroughly
3. Ensure all documentation is complete
4. Add LICENSE file (MIT recommended)

#### Step 2: Submit for Review

1. **Open an issue** in the [Catalog repository](https://github.com/AppPlatform-Templates/Catalog/issues/new):

```markdown
Title: [Official Template Submission] Your-Template-Name

**Template Repository:** https://github.com/yourusername/your-template-repo

**Description:** Brief description of what your template does

**Stack:** Node.js 20, Express 4.x, PostgreSQL 15 (list your stack)

**Checklist:**
- [ ] Follows DEVELOPER_GUIDE.md requirements
- [ ] Successfully tested deployment
- [ ] Documentation complete
- [ ] No security vulnerabilities
- [ ] Willing to transfer ownership to AppPlatform-Templates org

**Additional Notes:** Any special considerations or features
```

#### Step 3: Review Process

Our team will:

1. **Initial Review** (1-2 business days)
   - Check repository structure
   - Review documentation
   - Verify Deploy button works

2. **Technical Review** (3-5 business days)
   - Code quality assessment
   - Security audit
   - Test deployment
   - Performance evaluation

3. **Feedback**
   - We'll comment on your issue with feedback
   - You'll have opportunity to address any concerns
   - May require revisions

4. **Acceptance**
   - Once approved, you'll transfer repository to AppPlatform-Templates org
   - We'll add it to the Official Templates list
   - Template becomes officially maintained

#### Step 4: Transfer Repository

Once approved:

1. Go to your repository Settings � Transfer ownership
2. Transfer to `AppPlatform-Templates` organization
3. We'll rename if needed to follow naming conventions
4. You'll be added as a collaborator

### After Acceptance

- Your template is added to the catalog
- You're listed as the original author
- You can contribute updates via PRs
- Template may be featured in DigitalOcean blog posts or documentation

---

## Community Template Submission

### Prerequisites

- [ ] Read the [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md)
- [ ] Template follows minimum requirements
- [ ] Successfully tested deployment
- [ ] Documentation is complete

### Minimum Requirements

Community templates must meet these baseline standards:

**Required:**
-  `.do/deploy.template.yaml` at repository root
-  Valid YAML configuration with `git:` field
-  README with Deploy button and basic documentation
-  Cost estimate included
-  No obvious security issues
-  Successfully deploys to App Platform

**Recommended:**
-  .gitignore file
-  .env.example for required variables
-  LICENSE file
-  Local development instructions

### Submission Process

#### Step 1: Create Your Template

Follow [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md) to create your template in your own GitHub account.

#### Step 2: Submit Pull Request

1. **Fork** the [Catalog repository](https://github.com/AppPlatform-Templates/Catalog)

2. **Edit** `README.md` and add your template to the "Community Templates" table:

```markdown
| [YourTemplate-Name](https://github.com/yourusername/YourTemplate-Repo) | Brief description | @yourusername | [![Deploy to DO](https://www.deploytodo.com/do-btn-blue.svg)](https://cloud.digitalocean.com/apps/new?repo=https://github.com/yourusername/YourTemplate-Repo/tree/main) |
```

3. **Create Pull Request** with title: `[Community Template] Your-Template-Name`

**PR Description Template:**
```markdown
## Template Information

**Repository:** https://github.com/yourusername/YourTemplate-Repo
**Stack:** (e.g., Python 3.11, FastAPI, PostgreSQL)
**Description:** One-sentence description
**Estimated Cost:** $X/month

## Checklist

- [ ] Successfully deployed and tested
- [ ] README includes Deploy button
- [ ] `.do/deploy.template.yaml` at repository root
- [ ] No hardcoded secrets
- [ ] Cost estimate provided
- [ ] I will maintain this template

## Testing

I've tested this template by:
- Deploying successfully on (date)
- All features work as expected
- [Any special notes]
```

#### Step 3: Review

We'll review your submission for:

-  Template deploys successfully
-  Minimum requirements met
-  No obvious security issues
-  Documentation is adequate
-  Deploy button works

**Timeline:** 3-5 business days

#### Step 4: Acceptance

Once approved:
- Your PR is merged
- Template appears in Community Templates section
- You're listed as the maintainer
- **You keep ownership** and maintain the template

### After Acceptance

**Your Responsibilities:**
- Maintain your template repository
- Keep dependencies updated
- Respond to issues in your repository
- Update documentation as needed

**Optional:**
- Submit updates to improve your template
- Help others using your template
- Consider promoting to Official template later

---

## Submission Quality Tips

### Make It Easy to Review

**DO:**
-  Provide clear, complete documentation
-  Include screenshots or demo video
-  List all dependencies and versions
-  Explain any unusual configurations
-  Test thoroughly before submitting

**DON'T:**
- L Submit untested templates
- L Leave placeholder documentation
- L Include TODO comments in code
- L Submit with known bugs or issues
- L Use vague descriptions

### Documentation Checklist

Your README should answer:

- What does this template do?
- What stack/technologies does it use?
- How much will it cost to run?
- What environment variables are required?
- How do I deploy it?
- How do I develop locally?
- What are common issues and solutions?

### Common Rejection Reasons

We may request changes if:

- Deploy button doesn't work
- Obvious security vulnerabilities
- Incomplete or unclear documentation
- Template fails to deploy
- Cost estimate missing or inaccurate
- No error handling
- Hardcoded credentials
- Excessive resource usage without justification

---

## Review Timeline

| Submission Type | Initial Response | Full Review | Typical Total Time |
|-----------------|------------------|-------------|-------------------|
| Official | 1-2 days | 3-5 days | 1-2 weeks |
| Community | 2-3 days | 2-3 days | 3-7 days |

*Timelines are estimates and may vary based on submission complexity and volume.*

---

## After Your Template is Listed

### For Official Templates:

- Receive updates via GitHub notifications
- Contribute improvements via PRs
- Coordinate major changes with maintainers
- Template may be featured in official content

### For Community Templates:

- You receive issues/PRs in your repository
- Update your template as needed
- Can submit updates to catalog listing
- May be promoted to Official if actively maintained

---

## Questions?

- **General Questions**: [Open a Discussion](https://github.com/AppPlatform-Templates/Catalog/discussions)
- **Submission Questions**: [Open an Issue](https://github.com/AppPlatform-Templates/Catalog/issues)
- **Technical Help**: See [DEVELOPER_GUIDE.md](./DEVELOPER_GUIDE.md) Troubleshooting section

---

## Template Ideas We're Looking For

### High Priority:
- Popular frameworks (Next.js, Django, Laravel, etc.)
- Full-stack applications (MEAN, MERN, etc.)
- Databases with sample data
- API templates (REST, GraphQL)
- Microservices examples

### Would Be Great:
- CMS platforms
- E-commerce solutions
- Data processing pipelines
- Real-time applications
- AI/ML deployments

### Specialized:
- Industry-specific solutions
- Integration examples (Stripe, SendGrid, etc.)
- Monitoring and observability
- Multi-region setups

---

**Ready to submit?** Follow the appropriate process above based on whether you want to contribute an Official or Community template. Thank you for contributing to the community!