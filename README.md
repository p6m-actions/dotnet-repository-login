# Dotnet Repository Login

![Latest Release](https://img.shields.io/github/v/release/p6m-actions/dotnet-repository-login?style=flat-square&label=Latest%20Release&color=blue)

## Description

A GitHub Action that logs in to one or more .NET repositories for NuGet package publishing. This action configures NuGet sources and authentication credentials, making it easy to publish packages to private repositories or NuGet.org as part of your CI/CD pipeline.

## Usage

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository-urls: |
      private=https://nuget.mycompany.com/v3/index.json
      staging=https://nuget-staging.mycompany.com/v3/index.json
    credentials: |
      private=username:${{ secrets.PRIVATE_REPO_PASSWORD }}
      staging=${{ secrets.STAGING_API_KEY }}
      nuget=${{ secrets.NUGET_API_KEY }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `repository-urls` | Repository URL mappings in format `name=url`, one per line | No | `""` |
| `credentials` | Authentication credentials in format `name=username:password` or `name=api-key`, one per line | Yes | N/A |

### Credential Formats

- **API Key**: `repository-name=your-api-key`
- **Username/Password**: `repository-name=username:password`

## Outputs

| Output | Description |
|--------|-------------|
| `configured-repositories` | Comma-separated list of successfully configured repository names |

## Examples

### Basic NuGet.org Publishing

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    credentials: |
      nuget=${{ secrets.NUGET_API_KEY }}
```

### Multiple Private Repositories

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository-urls: |
      private=https://nuget.mycompany.com/v3/index.json
      staging=https://nuget-staging.mycompany.com/v3/index.json
    credentials: |
      private=service-account:${{ secrets.PRIVATE_REPO_PASSWORD }}
      staging=${{ secrets.STAGING_API_KEY }}
```

### Mixed Authentication Methods

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository-urls: |
      artifactory=https://mycompany.jfrog.io/artifactory/api/nuget/nuget-local
    credentials: |
      artifactory=admin:${{ secrets.ARTIFACTORY_PASSWORD }}
      nuget=${{ secrets.NUGET_API_KEY }}
```

## Security Recommendations

- Always use GitHub Secrets for storing credentials
- Never commit credentials directly in your workflow files
- Use least-privilege principles when creating API keys
- Consider using short-lived tokens when possible