# Project Guidelines

## Purpose and Architecture

Build a platform for safely and consistently deploying and upgrading CMS websites, starting with WordPress and Drupal.

- Use GitHub repositories and GitHub Actions for version-controlled changes and deployment triggers. Use Argo CD to reconcile declarative deployment configuration to OpenShift or Kubernetes.
- Use HashiCorp Vault for secrets. Never commit secret values to Git, expose them in logs, or place them in plain-text catalog metadata or deployment values. Use the repository's established Vault integration.
- Use Backstage as the service catalog, software-template/scaffolder, backplane, and self-service portal.
- Keep one GitHub repository per website. Do not create a shared website-source monorepo. This repository is for platform/GitOps configuration; keep site-specific application source in that site's repository.
- Prefer small, reviewable pull requests and declarative changes. Do not bypass the established review and deployment workflows with manual production changes.

## Website Organization and Backstage

- Organize sites by department or college. Model organizational ownership (for example, Chemistry) separately from the CMS technology.
- Use Backstage catalog entities consistently: Domains for broad organizational groupings, Systems for related services or capabilities, Components for individual websites, and Resources for infrastructure and dependencies. Use the closest existing project convention when one has been established.
- Each website should have a `catalog-info.yaml` that describes its ownership, relationships, lifecycle, and CMS metadata. Make the CMS identifiable through metadata rather than relying on repository names.
- Keep deployment configuration and ownership explicit. Where the site-repository convention uses them, maintain `application.yaml`, `values.yaml`, and `ownership.yaml` as distinct, purpose-specific files.
- Backstage Scaffolder templates should create a complete, valid per-site repository with the required catalog metadata, deployment configuration, ownership, and CI workflows. Keep generated repositories consistent with the platform's current templates and conventions.

## CMS and Update Workflows

- For Drupal sites, commit `composer.json` and `composer.lock` together so dependency changes are reproducible. Treat `config/sync` as version-controlled Drupal configuration; do not store secrets or environment-specific secret values there.
- Backstage-triggered Drupal update workflows should propose changes through reviewable pull requests, including relevant Composer lockfile updates. Do not silently push unreviewed dependency or configuration changes to a deployment branch.
- Apply the same reviewability and reproducibility to WordPress and other CMS image or dependency updates.
- Pin or constrain container images and dependencies according to the existing project convention; avoid floating production versions that make deployments non-reproducible.

## Changes and Validation

- Read the affected chart, manifest, workflow, and documentation before changing them. Follow established naming, labels, ownership, and environment conventions.
- Keep changes scoped to the requested site or platform concern. Update directly related documentation and scaffolder templates when changing a generated repository contract.
- Validate YAML and Helm changes with the validation tools or CI workflows already configured in the affected repository. Do not claim a validation command passed unless it was run.
- This repository is evolving; inspect its current files and workflows for available build and test commands rather than assuming a command or infrastructure integration exists.
