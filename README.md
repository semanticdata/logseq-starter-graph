# Logseq Starter Graph

<p>
<img src="https://img.shields.io/github/languages/code-size/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/repo-size/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/commit-activity/t/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/github/last-commit/semanticdata/logseq-starter-graph" />
<img src="https://img.shields.io/website/https/semanticdata.github.io/logseq-starter-graph.svg" />
</p>

A Logseq Starter.

## 📢 Publish to GitHub Pages

We recommend using the [publish workflow](https://github.com/semanticdata/logseq-starter-graph/blob/main/.github/workflows/logseq-publish.yml) to publish your graph to GitHub Pages. To do so, follow the steps below.

> 📝 The first time the workflow is run takes significantly longer than subsequent cycles. Please be patient.

### 1. Open the Repository Settings

At the top of the repository, click **Settings**.

![repository settings](assets/repository-settings.png)

### 2. Navigate to the Pages Section

On the left sidebar, click **Pages** under *Code and automation*.

![source branch](assets/source-branch.png)

### 3. Configure GitHub Pages Source to GitHub Actions

Under the *Build and deployment* section, under **Source**, change it from **Deploy from a branch** to **GitHub Actions**.

![source actions](assets/source-actions.png)

### 4. Navigate to the Actions Section

At the top of the repository, click **Actions**.

![repository actions](assets/repository-actions.png)

### 5. Run the Workflow for the First Time

On the left sidebar, click the workflow name (**Validate and Publish Logseq Graph to GitHub Pages**).

![action summary](assets/action-summary.png)

On the right, click **Run workflow**, then click on the new **Run workflow** (blue) button.

![action runs](assets/action-runs.png)

> 📝 The first time the workflow is run takes significantly longer than subsequent cycles. Please be patient.

### 6. Be Patient

The first time you run the workflow, it will take a few minutes to complete. Subsequent runs will be faster.

Take a look at the first run for *this* repository:

![action duration](assets/action-duration.png)

Over 11 minutes!

## 🔀 Workflows

A breakdown of the workflows used in this project.

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

### Validate and Publish 🚀

A workflow that both validates and deploys to GitHub Pages (only after validation passes) is used for this project and looks like this:

```yml
name: Validate then Publish Logseq Graph
steps:
  - name: Checkout
    uses: actions/checkout@v4
  - name: Run graph-validator tests
    uses: logseq/graph-validator@main
  - name: Build Logseq graph
    uses: logseq/publish-spa@main
    with:
      output-directory: build # must match path below
      accent-color: indigo
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
