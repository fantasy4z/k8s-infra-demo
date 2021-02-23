# charts

## Prerequisites

- helm v3.5.2+
- helmfile v0.138.4+
- helm-diff v3.1.3+

## Usage

- Adding a helm chart.
  - Create a directory under the current directory.
  - Get the chart tarball by `helm pull [chart URL]`.
  - Create `helmfile.yaml` under the newly-created directory.
    - Check [helmfile repo](https://github.com/roboll/helmfile) for how to
        write a `helmfile.yaml` file.
    - Chart version can be found in `Chart.yaml` in the tarball.
  - Prepare value files.
    - Common practices:
      - Copy `values.yaml` from the tarball.
      - Prepare `override.yaml`.
      - Prepare configs for different environments by leverage helmfile
          templates: `*.gotmpl`.
          See: <https://github.com/roboll/helmfile#templates>
  - Utilize [Helmfile hooks](https://github.com/roboll/helmfile#hooks) to
    mutate cluster state by listening to `presync`/`postsync` events. This is
    ideal to create a namespace or some resources.
  - Run `helmfile` to install the helm chart.

    ```bash
    helmfile --environment=<ENV> apply
    ```
