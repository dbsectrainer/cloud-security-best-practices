# Copilot Instructions for AI Coding Agents

## Project Overview

This repository is a Jekyll-based documentation site for cloud security best practices, focusing on multi-cloud (AWS, Azure, GCP) security frameworks, compliance, and operational guides. The site is designed for GitHub Pages deployment.

## Architecture & Key Files

- **Documentation Structure**:
  - Core frameworks: `SECURITY_FRAMEWORK.md`, `COMPLIANCE.md`, `RISK_MANAGEMENT.md`
  - Implementation: `IMPLEMENTATION_GUIDE.md` (deployment, automation, best practices)
  - Operations: `INCIDENT_RESPONSE_PLAN.md`, `DISASTER_RECOVERY.md`, `TESTING_GUIDE.md`
  - Specialized: `VENDOR_SECURITY_ASSESSMENT.md`, `SECURITY_TRAINING_GUIDE.md`, `INNOVATION.md`
- **Jekyll Config**: `_config.yml` (site settings, GitHub Pages compatibility)
- **Layout & Styling**: `_layouts/default.html`, `assets/css/style.css`
- **Visuals**: SVG diagrams generated from DOT files (Graphviz), embedded Mermaid diagrams in markdown

## Developer Workflows

- **Local Development**:
  - Install dependencies: `bundle install`
  - Serve site: `bundle exec jekyll serve`
  - Build site: `bundle exec jekyll build`
  - Clean artifacts: `bundle exec jekyll clean`
- **Diagram Generation**:
  - Generate SVGs from DOT files (requires Graphviz):
    ```
    dot -Tsvg security_framework.dot -o security_framework.svg
    dot -Tsvg risk_management.dot -o risk_management.svg
    dot -Tsvg disaster_recovery.dot -o disaster_recovery.svg
    dot -Tsvg incident_response.dot -o incident_response.svg
    ```
- **Markdown Conversion**: All `.md` files are auto-converted to HTML by Jekyll.

## Project-Specific Patterns

- **Zero Trust Architecture**: Central theme in `SECURITY_FRAMEWORK.md`
- **Automation**: Emphasized in `IMPLEMENTATION_GUIDE.md` (95% coverage)
- **Compliance**: Real-time monitoring, automated validation (`COMPLIANCE.md`)
- **Visual Documentation**: Use DOT files for SVGs, Mermaid for quick diagrams
- **Badges**: Status badges in `README.md` reflect project health and focus areas

## Integration Points

- **External Dependencies**: Ruby (Jekyll), Bundler, Graphviz (for diagrams)
- **No custom build scripts**; all workflows use standard Jekyll and Graphviz commands

## Conventions

- All documentation is markdown-first, auto-published via Jekyll
- Diagrams are versioned as both DOT and SVG; regenerate SVG files with Graphviz when editing DOT sources
- Maintain factual vendor currency: Microsoft Entra ID (not Azure AD), Prisma Cloud Compute (not Twistlock), Google Security Operations / Google SecOps (not Chronicle), Lacework FortiCNAPP, OpenTofu and IBM HashiCorp
- Maintain regulatory currency: PCI-DSS v4.0.1 (in full force), NIST FIPS 203/204/205 post-quantum cryptography standards, OWASP Top 10:2025, and EU AI Act phased compliance milestones
- Ensure multi-document consistency across `README.md`, `SECURITY_FRAMEWORK.md`, `COMPLIANCE.md`, and `IMPLEMENTATION_GUIDE.md` when updating framework lists

## Examples

- To update a diagram, edit the `.dot` file and regenerate the `.svg` using `dot -Tsvg <name>.dot -o <name>.svg`
- To add a new guide, create a markdown file and link it in `README.md`, `_config.yml` (include list), and relevant navigation structures
