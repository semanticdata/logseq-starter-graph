# Logseq Starter Graph

<p>
<img src="https://img.shields.io/github/languages/code-size/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/repo-size/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/commit-activity/t/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/last-commit/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/website/https/semanticdata.github.io/logseq-starter-graph.svg" />
</p>

A Logseq Starter.

## 🔀 Workflows

### Validate ✅

The [validate workflow](https://github.com/semanticdata/logseq-starter-graph/blob/main/.github/workflows/logseq-validate.yml) runs tests on the graph to identify any errors using [logseq/graph-validator](https://github.com/logseq/graph-validator).

```yml
name: Validate Logseq Graph
steps:
  - name: Checkout code
    uses: actions/checkout@v4
  - name: Run graph-validator tests
    uses: logseq/graph-validator@main
```

### Publish 📢

The [publish](https://github.com/semanticdata/logseq-starter-graph/blob/main/.github/workflows/logseq-publish.yml) workflow builds and deploys the graph to GitHub Pages using [logseq/publish-spa](https://github.com/logseq/publish-spa).

```yml
name: Publish Logseq Graph
steps:
  - name: Checkout code
    uses: actions/checkout@v4
  - name: Build Logseq graph
    uses: logseq/publish-spa@main
    with:
      output-directory: build # must match path below
  - name: Configure for GitHub Pages
    uses: actions/configure-pages@v5
  - name: Upload artifact
    uses: actions/upload-pages-artifact@v3
    with:
      path: build # must match output-directory above
  - name: Deploy to GitHub Pages
    id: deployment
    uses: actions/deploy-pages@v4
```

### Validate and Publish 🥂

A workflow that both validates and deploys to GitHub Pages (only after validation passes) looks like this:

```yml
name: Publish Logseq Graph
steps:
  - name: Checkout code
    uses: actions/checkout@v4
  - name: Run graph-validator tests
    uses: logseq/graph-validator@main
  - name: Build Logseq graph
    uses: logseq/publish-spa@main
    with:
      output-directory: build # must match path below
  - name: Configure for GitHub Pages
    uses: actions/configure-pages@v5
  - name: Upload artifact
    uses: actions/upload-pages-artifact@v3
    with:
      path: build # must match output-directory above
  - name: Deploy to GitHub Pages
    id: deployment
    uses: actions/deploy-pages@v4
```

## © License

Source code in this repository is available under the [MIT License](LICENSE).
