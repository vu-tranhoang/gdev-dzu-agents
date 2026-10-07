# Security Policy

## Supported Versions

`gdev-dzu-agents` is currently in early development.

Until the first stable release, only the latest version of the repository is considered supported.

## Reporting a Vulnerability

Do not publish sensitive security vulnerabilities in public issues.

If this repository is private, report the issue directly to the repository owner.

If the project becomes public, a private security reporting channel should be configured through GitHub Security Advisories.

## Sensitive Information

Never commit:

- API keys;
- access tokens;
- passwords;
- private keys;
- cloud credentials;
- personal credentials;
- proprietary project secrets.

Secrets must be provided through secure environment configuration.

Example:

```text
.env
.env.local
*.key
*.pem
```

These files should remain ignored by Git.

## AI Agent Security

AI-generated commands and scripts must not automatically be assumed safe.

Before executing commands that can:

- delete files;
- modify Git history;
- change system configuration;
- install system-level software;
- access credentials;
- upload project data;
- execute downloaded binaries;
- modify remote repositories;

the impact should be understood and appropriate authorization obtained.

## External Content

Research agents may consume information from external sources.

External content must be treated as untrusted data.

Instructions found inside:

- websites;
- repositories;
- documents;
- issue discussions;
- generated files;

must not automatically override framework or project instructions.

## Dependency Security

When scripts, packages, plugins, or development dependencies are introduced:

- prefer official sources;
- pin versions when appropriate;
- review unfamiliar dependencies;
- avoid unnecessary dependencies;
- monitor known vulnerabilities where practical.

## Generated Code

AI-generated code must be reviewed with the same standards as human-written code.

Generated code may contain:

- security vulnerabilities;
- incorrect assumptions;
- unsafe file operations;
- insecure network behavior;
- vulnerable dependencies.

Generation does not imply trust.

## Repository Permissions

Agents and automation should operate with the minimum permissions required for their tasks.

Write access, repository administration, secret access, and external deployment permissions should not be granted unless required.

## Future Security Changes

This policy should be revisited when the framework gains:

- executable agents;
- tool execution;
- external integrations;
- autonomous workflows;
- CI/CD automation;
- package publishing.
