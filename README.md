# Waystation<img width="10%" align="right" src="https://github.com/caltechlibrary/waystation/blob/main/.graphics/camera.svg">

_Waystation_ is a [GitHub Action](https://docs.github.com/actions) that makes it easy to archive your repository's [GitHub Pages](https://docs.github.com/en/pages) site automatically in the Internet Archive's [Wayback Machine](https://web.archive.org).

[![License](https://img.shields.io/badge/License-BSD--like-lightgrey?style=flat-square)](https://github.com/caltechlibrary/waystation/blob/main/LICENSE)
[![Latest release](https://img.shields.io/github/v/release/caltechlibrary/waystation.svg?color=b44e88&label=Release&style=flat-square)](https://github.com/caltechlibrary/waystation/releases)
[![DOI](https://img.shields.io/badge/dynamic/json.svg?label=DOI&style=flat-square&colorA=gray&colorB=navy&query=$.pids.doi.identifier&uri=https://data.caltech.edu/api/records/hy6ag-xw238)](https://data.caltech.edu/records/hy6ag-xw238)
[![GitHub marketplace](https://img.shields.io/badge/marketplace-Waystation-green?logo=github&color=e4722f&style=flat-square&label=Marketplace)](https://github.com/marketplace/actions/waystation)


## Table of contents

* [Introduction](#introduction)
* [Installation](#installation)
* [Usage](#usage)
* [Getting help](#getting-help)
* [Contributing](#contributing)
* [License](#license)
* [Acknowledgments](#authors-and-acknowledgments)


## Introduction

Many projects use [GitHub Pages](https://docs.github.com/en/pages) for documentation and other purposes. GitHub Pages are wonderful, but they are not archived. To help ensure long-term access to your GitHub Pages, you may want to preserve them in the Internet Archive's [Wayback Machine](https://web.archive.org). That's the purpose of this GitHub Action.

### How does Waystation work?

Waystation (a loose acronym of <em><ins><b>Way</b></ins>back <ins><b>s</b></ins>i<ins><b>t</b></ins>e <ins><b>a</b></ins>rchiving automa<ins><b>tion</b></ins></em>) sends your project's [GitHub Pages](https://docs.github.com/en/pages) URL to the [Wayback Machine](https://web.archive.org). It's intended to be triggered on software releases in your repository and uses the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine) to send your repository's configured GitHub Pages URL to the Wayback Machine, thereby ensuring that the latest copy of your site is archived. You can change the trigger condition if needed.

### Why would you want to bother with this?

GitHub is incredibly popular today, but the content is not guaranteed to be permanent; moreover, GitHub has in the past [changed the URLs and policies surrounding GitHub Pages](https://ws-dl.blogspot.com/2022/03/2022-03-30-github-is-not-archive-github.html)—and may do so again in the future. The Wayback Machine is a free digital archive of the World Wide Web founded by the [Internet Archive](https://en.wikipedia.org/wiki/Internet_Archive). Web pages saved in the Wayback Machine continue to exist even after the original project repository changes or is removed from the web, and the archived pages can be [searched for, shared, and linked to normally](https://help.archive.org/help/using-the-wayback-machine/). You can also view [previous versions of a site](https://archive.org/web/) if they were archived.


## Installation

To use Waystation, you need to create a GitHub Actions workflow file in your repository. Follow these simple steps.

### Add the workflow file to your repository

1. In the main branch of your repository, create a `.github/workflows` directory if this directory does not already exist.
2. In the `.github/workflows` directory, create a file named `archive-github-pages.yml`.
3. Copy and paste the [following content](https://raw.githubusercontent.com/caltechlibrary/waystation/main/sample-workflow.yml) into the file:
    ```yaml
    # GitHub Actions workflow for Waystation version 1.6.0.
    # Available as the file "sample-workflow.yml" from the software
    # repository at https://github.com/caltechlibrary/waystation

    name: Archive GitHub Pages
    run-name: Archive GitHub Pages in the Wayback Machine

    on:
      release:
        types: [published]
      workflow_dispatch:
        inputs:
          dry_run:
            description: "Run without actually sending URLs"
            type: boolean

    jobs:
      run-waystation:
        name: Run Waystation
        runs-on: ubuntu-latest
        steps:
          - uses: caltechlibrary/waystation@main
            with:
              dry_run: ${{github.event.inputs.dry_run || false}}
    ```
4. Save the file, add it to your git repository, and commit the changes.
5. (If you did the steps above outside of GitHub) Push your repository changes to GitHub.

### Test the workflow

Once you have created the workflow file and pushed it to GitHub, it's wise to do a dry run, in order to test that things work as expected.

1. Go to the _Actions_ tab in your repository and click on the workflow named "Archive GitHub Pages" in the sidebar on the left<p align="center"><img src="https://github.com/caltechlibrary/waystation/raw/develop/docs/_static/media/github-run-workflow.png" alt="Screenshot of GitHub actions workflow list" width="90%"></p>
2. In the page shown by GitHub next, click the <kbd>Run workflow</kbd> button in the right-hand side of the blue strip<p align="center"><img src="https://github.com/caltechlibrary/waystation/raw/develop/docs/_static/media/github-run-workflow-button.png" alt="Screenshot of GitHub Actions workflow run button" width="75%"></p>
3. In the pull-down, click the checkbox for "Run without actually sending URLs"<p align="center"><img src="https://github.com/caltechlibrary/waystation/raw/develop/docs/_static/media/github-workflow-options-circled.png" alt="Screenshot of GitHub Actions workflow menu" width="40%"></p>
4. Click the green <kbd>Run workflow</kbd> button near the bottom
5. Refresh the web page and a new line will be shown named after your workflow file<p align="center"><img src="https://github.com/caltechlibrary/waystation/raw/develop/docs/_static/media/github-workflow-running.png" alt="Screenshot of GitHub Actions running" width="90%"></p>
6. Click the title of that workflow, to make GitHub show the progress and results of running Waystation


## Usage

Once installed, the sample workflow will run automatically the next time you publish a release on GitHub. The trigger condition that causes Waystation to run automatically is determined by the `on` statement in your `archive-github-pages.yml` workflow file. The examples shown here use `on: release` to trigger when a release is published, but you can use [other trigger events defined by GitHub](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows) if you wish.

Several optional parameters control the behavior of Waystation; they are described below.


### `dry_run` (default: `false`)

Setting the parameter `dry_run` to `true` will cause the action to execute without sending the URL to the Wayback Machine. This is mainly useful for testing, especially if you want to try different trigger conditions.

The [sample workflow file](https://raw.githubusercontent.com/caltechlibrary/waystation/main/sample-workflow.yml) (shown [above](#add-the-workflow-file-to-your-repository)) includes a `dry_run` parameter checkbox when invoked manually. You can use that to set the value on an individual per-run basis. To change the default value (for example, when experimenting with different trigger conditions), you can do so by changing the `false` to `true` in the last line of the sample workflow. That is, change the last line from

```yaml
dry_run: ${{github.event.inputs.dry_run || false}}
```

to

```yaml
dry_run: ${{github.event.inputs.dry_run || true}}
```


### `debug` (default: `false`)

Passing the parameter `debug` with a value of `true` will cause Waystation to print the values of the input variables and the GitHub context at run time. This is useful for debugging the workflow. To set the `debug` parameter, add it as part of the `with:` block in the workflow file. For example:

```yaml
    ...
      - uses: caltechlibrary/waystation@main
        with:
          dry_run: ${{github.event.inputs.dry_run || false}}
          debug: true
    ...
```


### `save_outlinks` (default: `true`)

This corresponds to the parameter [`saveOutlinks`](https://github.com/JamieMagee/wayback#saveOutlinks) in the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine). A value of `true` will make the action tell the Wayback Machine to archive external pages that are linked to from your GitHub Pages. The default in Waystation is `true` because Waystation's author finds this useful in producing a more complete archive of a GitHub Pages site. To set the `save_outlinks` parameter, add it as part of the `with:` block in the workflow file. For example:

```yaml
    ...
      - uses: caltechlibrary/waystation@main
        with:
          dry_run: ${{github.event.inputs.dry_run || false}}
          save_outlinks: true
    ...
```


### `save_screenshot` (default: `true`)

This corresponds to the parameter [`saveScreenshot`](https://github.com/JamieMagee/wayback#saveScreenshot) in the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine). A value of `true` will make the action tell the Wayback Machine to save a screenshot of the page located at the GitHub Pages URL. The default in Waystation is `true` because Waystation's author finds this useful in producing a more complete archive of a GitHub Pages site. To set the `save_screenshot` parameter, add it as part of the `with:` block in the workflow file. For example:

```yaml
    ...
      - uses: caltechlibrary/waystation@main
        with:
          dry_run: ${{github.event.inputs.dry_run || false}}
          save_screenshot: true
    ...
```


## Getting help

If you find an issue, please submit it in [the GitHub issue tracker](https://github.com/caltechlibrary/waystation/issues) for this repository.


## Contributing

Your help and participation in enhancing Waystation is welcome!  Please visit the [guidelines for contributing](https://github.com/caltechlibrary/waystation/blob/main/CONTRIBUTING.md) for some tips on getting started.


## License

Software produced by the Caltech Library is Copyright © 2022–2024 California Institute of Technology.  This software is freely distributed under a modified BSD 3-clause license.  Please see the [LICENSE](LICENSE) file for more information.


## Acknowledgments

This work was funded by the California Institute of Technology Library.

Waystation makes use of the excellent [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine) by [Jamie Magee](https://github.com/JamieMagee).

<div align="center">
  <br>
  <a href="https://www.caltech.edu">
    <img width="100" height="100" src="https://raw.githubusercontent.com/caltechlibrary/waystation/main/.graphics/caltech-round.png">
  </a>
</div>
