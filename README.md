# Dotnet Repository Login

![Latest Release](https://img.shields.io/github/v/release/p6m-actions/dotnet-repository-login?style=flat-square&label=Latest%20Release&color=blue)

## Description

A GitHub Action that logs in to a .NET repository for NuGet package publishing. This action configures NuGet sources and authentication credentials, making it easy to publish packages to private repositories as part of your CI/CD pipeline.

## Usage

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository: ${{ github.repository_owner }}-nuget
    repository-url: https://mycompany.jfrog.io/artifactory/api/nuget/${{ github.repository_owner }}-nuget
    username: ${{ secrets.ARTIFACTORY_USERNAME }}
    password: ${{ secrets.ARTIFACTORY_IDENTITY_TOKEN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `repository` | Repository name to configure | Yes | N/A |
| `repository-url` | Full repository URL (e.g., https://api.nuget.org/v3/index.json, https://mycompany.jfrog.io/artifactory/api/nuget/repo-name) | Yes | N/A |
| `username` | Username for repository authentication | Yes | N/A |
| `password` | Password/token for repository authentication | Yes | N/A |

## Outputs

| Output | Description |
|--------|-------------|
| `configured-repository` | Name of successfully configured repository |

## Examples

### Artifactory Repository

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository: ${{ github.repository_owner }}-nuget
    repository-url: https://mycompany.jfrog.io/artifactory/api/nuget/${{ github.repository_owner }}-nuget
    username: ${{ secrets.ARTIFACTORY_USERNAME }}
    password: ${{ secrets.ARTIFACTORY_IDENTITY_TOKEN }}
```

### NuGet.org

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository: nuget-org
    repository-url: https://api.nuget.org/v3/index.json
    username: apikey
    password: ${{ secrets.NUGET_API_KEY }}
```

### Private NuGet Server

```yaml
- uses: p6m-actions/dotnet-repository-login@v1
  with:
    repository: private-nuget
    repository-url: https://nuget.mycompany.com/v3/index.json
    username: ${{ secrets.PRIVATE_REPO_USERNAME }}
    password: ${{ secrets.PRIVATE_REPO_PASSWORD }}
```

## Security Recommendations

- Always use GitHub Secrets for storing credentials
- Never commit credentials directly in your workflow files
- Use least-privilege principles when creating API keys
- Consider using short-lived tokens when possible