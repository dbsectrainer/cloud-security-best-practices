# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based documentation project focused on cloud security best practices, frameworks, and implementation guides. The project serves as a comprehensive resource for multi-cloud security strategies across AWS, Azure, and Google Cloud Platform.

## Development Commands

### Jekyll Site Management
```bash
# Install dependencies
bundle install

# Serve the site locally for development
bundle exec jekyll serve

# Build the site for production
bundle exec jekyll build

# Clean build artifacts
bundle exec jekyll clean
```

### Working with SVG Diagrams
The project includes Graphviz DOT files that generate SVG diagrams:
```bash
# Generate SVG from DOT files (if Graphviz is installed)
dot -Tsvg security_framework.dot -o security_framework.svg
dot -Tsvg risk_management.dot -o risk_management.svg
dot -Tsvg disaster_recovery.dot -o disaster_recovery.svg
dot -Tsvg incident_response.dot -o incident_response.svg
```

## Repository Architecture

### Documentation Structure
- **Core Frameworks**: `SECURITY_FRAMEWORK.md`, `COMPLIANCE.md`, `RISK_MANAGEMENT.md`
- **Implementation**: `IMPLEMENTATION_GUIDE.md` contains technical deployment instructions
- **Operational**: `INCIDENT_RESPONSE_PLAN.md`, `DISASTER_RECOVERY.md`, `TESTING_GUIDE.md`
- **Specialized**: `VENDOR_SECURITY_ASSESSMENT.md`, `SECURITY_TRAINING_GUIDE.md`, `INNOVATION.md`

### Jekyll Configuration
- Site configured in `_config.yml` with GitHub Pages compatibility
- Custom layout in `_layouts/default.html`
- Styling in `assets/css/style.css`
- All markdown files are automatically included and converted to HTML

### Visual Elements
- SVG diagrams generated from DOT files for security frameworks, risk management, disaster recovery, and incident response
- Mermaid diagrams embedded in markdown for quick start guides
- Comprehensive badge system in README.md for project status

## Content Guidelines

### Security Focus
This is a defensive security documentation project. Content should focus on:
- Cloud security best practices and frameworks
- Compliance and governance strategies
- Risk management and threat mitigation
- Incident response and disaster recovery
- Security architecture and implementation guides

### Documentation Standards
- Each major topic has its own dedicated markdown file
- Technical implementation examples use Infrastructure as Code (Terraform, CloudFormation)
- Multi-cloud approach covering AWS, Azure, and GCP
- Emphasis on Zero Trust architecture and automated security controls

### Key Themes
- Zero Trust security model implementation
- Infrastructure as Code with embedded security
- Continuous compliance monitoring
- Automated threat detection and response
- Multi-cloud security strategy