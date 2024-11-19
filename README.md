# GitHub Actions Collection

A collection of reusable GitHub Actions for container build and Kubernetes deployment workflows.

## Available Actions

### 1. Build and Push Image (`build-and-push`)

This action builds a Docker image and pushes it to Amazon ECR.

```yaml
- uses: ./actions/build-and-push
  with:
    # Required
    tags: 'org/repo:latest'
    labels: |
      org.opencontainers.image.created=${{ steps.prep.outputs.created }}
      org.opencontainers.image.source=${{ github.repositoryUrl }}
    file: './Dockerfile'
    
    # Optional
    cache-from: 'type=local,src=path/to/cache'
    platforms: 'linux/amd64,linux/arm64'
    context: '.'
```

#### Inputs

| Name | Required | Description | Default |
|------|----------|-------------|---------|
| `tags` | Yes | List of tags for the Docker image | |
| `labels` | Yes | List of metadata labels for the image | |
| `file` | Yes | Path to the Dockerfile | |
| `cache-from` | No | List of external cache sources for buildx | |
| `platforms` | No | List of target platforms for build | |
| `context` | No | Build context path | |

### 2. Helm Deploy (`helm-deploy`)

This action deploys Helm charts to a Kubernetes cluster, with optional Helmfile support.

```yaml
- uses: ./actions/helm-deploy
  with:
    # Required
    cluster: 'my-cluster'
    release: 'my-release'
    
    # Optional
    helm_version: 'v3.13.1'
    helmfile: 'false'
    install-helm-plugins: 'yes'
```

#### Inputs

| Name | Required | Description | Default |
|------|----------|-------------|---------|
| `cluster` | Yes | Cluster name | |
| `release` | Yes | Release name | |
| `helm_version` | No | Helm version | `v3.13.1` |
| `helmfile` | No | Enable helmfile | `false` |
| `install-helm-plugins` | No | Install Helm plugins | `yes` |

## Contributing

When contributing to this repository, please follow the [Angular Conventional Commits](https://www.conventionalcommits.org/) specification for your commit messages.

### Commit Message Format
```
<type>(<scope>): <short summary>
```

Types:
- feat: A new feature
- fix: A bug fix
- docs: Documentation only changes
- style: Changes that do not affect the meaning of the code
- refactor: A code change that neither fixes a bug nor adds a feature
- perf: A code change that improves performance
- test: Adding missing tests or correcting existing tests
- build: Changes that affect the build system or external dependencies
- ci: Changes to our CI configuration files and scripts
- chore: Other changes that don't modify src or test files

## License

MIT License
