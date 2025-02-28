# Helm push action

This action package helm chart and publish it to your chartmuseum.

## Usage

### `workflow.yml` Example

Place in a `.yml` file such as this one in your `.github/workflows` folder. [Refer to the documentation on workflow YAML syntax here.](https://help.github.com/en/articles/workflow-syntax-for-github-actions)

```yaml
name: Build & Push ecs-exporter chart
on: push

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Build and Push Charts
        uses: MarletteStandards/push-helm-chart-action@repo-add
        with:
          ChartFolder: "my-chart"
          ChartSourcePath: "helm"
          ChartmuseumRepoName: "chartmuseum"
          ChartmuseumUrl: ${{ env.ChartmuseumUrl }}
          ChartmuseumUsername: ${{ env.ChartmuseumUser }}
          ChartmuseumPassword: ${{ env.ChartmuseumPassword }}
          ChartVersion: ${{ env.SemVer }}
          ChartAppVersion: ${{ env.SemVer }}
```

### Older Configuration

These settings are old, but can still be used. The following settings may be passed as environment variables as shown in the example. Sensitive information, especially `CHARTMUSEUM_USER` and `CHARTMUSEUM_PASSWORD`, should be [set as encrypted secrets](https://help.github.com/en/articles/virtual-environments-for-github-actions#creating-and-using-secrets-encrypted-variables) — otherwise, they'll be public to anyone browsing your repository.

| Key | Value | Suggested Type | Required |
| ------------- | ------------- | ------------- | ------------- |
| `CHART_FOLDER` | Folder with charts in repo | `env` | **Yes** |
| `CHARTMUSEUM_URL` | Chartmuseum url | `env` | **Yes** |
| `CHARTMUSEUM_USER` | Username for chartmuseum  | `secret` | **Yes** |
| `CHARTMUSEUM_PASSWORD` | Password for chartmuseum | `secret` | **Yes** |
| `SOURCE_DIR` | The local directory you wish to upload. For example, `./charts`. Defaults to the root of your repository (`.`) if not provided. | `env` | No |
| `FORCE` | Force chart upload (in case version exist in chartmuseum, upload will fail without `FORCE`). Defaults is `False` if not provided. | `env` | No |

## Action versions

- v2: helm v2.17.0
- v3: helm3 v3.7.2

## License

This project is distributed under the [MIT license](LICENSE.md).
