# Waystation<img align="right" width="10%" src="_static/media/camera.png">

_Waystation_ is a [GitHub Action](https://docs.github.com/actions) that makes it easy to archive your repository's [GitHub Pages](https://docs.github.com/en/pages) site automatically in the Internet Archive's [Wayback Machine](https://web.archive.org).


## Introduction

Many projects use [GitHub Pages](https://docs.github.com/en/pages) for documentation and other purposes. GitHub Pages are wonderful, but they are not archived. To help ensure long-term access to your GitHub Pages, you may want to preserve them in the Internet Archive's [Wayback Machine](https://web.archive.org). That's the purpose of this GitHub Action.

### How does Waystation work?

Waystation (<ins><b>Way</b></ins>back <ins><b>s</b></ins>i<ins><b>t</b></ins>e <ins><b>a</b></ins>rchiving automa<ins><b>tion</b></ins>) automates the task of sending your project's [GitHub Pages](https://docs.github.com/en/pages) URL to the [Wayback Machine](https://web.archive.org). It's intended to be triggered on software releases in your repository and uses the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine) to send your repository's configured GitHub Pages URL to the Wayback Machine, thereby ensuring that the latest copy of your site is archived. You can change the trigger condition if needed.

### Why would you want to use it?

GitHub is incredibly popular today, but the content is not guaranteed to be permanent; moreover, GitHub has in the past [changed the URLs and policies surrounding GitHub Pages](https://ws-dl.blogspot.com/2022/03/2022-03-30-github-is-not-archive-github.html)—and may do so again in the future. The Wayback Machine is a free digital archive of the World Wide Web founded by the [Internet Archive](https://en.wikipedia.org/wiki/Internet_Archive). Web pages saved in the Wayback Machine continue to exist even after the original project repository changes or is removed from the web, and they can be [searched for, shared, and linked to normally](https://help.archive.org/help/using-the-wayback-machine/). You can also view [previous versions of a site](https://archive.org/web/) if they were archived.


## Installation

This action is available from the [GitHub Marketplace](https://github.com/marketplace?type=&verification=&query=waystation). Once you find the page in the GitHub Marketplace, do the following:

1. In the main branch of your repository, create a `.github/workflows` directory if this directory does not already exist.
2. In the `.github/workflows` directory, create a file named `archive-github-pages.yml`.
3. Copy and paste the following content into the file:
    ```yaml
    on:
      release:
        types: [published]
    jobs:
      Workflow:
        runs-on: ubuntu-latest
        steps:
          - uses: caltechlibrary/waystation@main
            with:
              GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    ```
4. Save the file, add it to your git repository, and commit the changes.
5. (If you did the steps above outside of GitHub) Push your repository changes to GitHub.

Refer to the next section for more information.


## Usage

The trigger condition that causes Waystation to run is determined by the `on` statement in your `archive-github-pages.yml` workflow file. The examples shown here use `on: release` to trigger when software is released, but you can use [other trigger events defined by GitHub](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows) if you wish.

Several parameters control the behavior of Waystation; they are described below.


### `dry_run` (default: `false`)

Setting the parameter `dry_run` to `true` will cause the action to execute without sending the URL to the Wayback Machine. This is useful during testing, especially if you want to try different trigger conditions.

Here is an example workflow definition using `dry_run`:

```yaml
# .github/workflows/archive-github-pages.yml
on:
  release:
    types: [published]
jobs:
  Workflow:
    runs-on: ubuntu-latest
    steps:
      - uses: caltechlibrary/waystation@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          dry_run: true
```


### `debug` (default: `false`)

Setting the parameter `debug` to `true` will cause the action to print the values of the input variables
and the GitHub context. This is useful for debugging the workflow.

Here is an example workflow definition using `debug`:

```yaml
on:
  release:
    types: [published]
jobs:
  Workflow:
    runs-on: ubuntu-latest
    steps:
      - uses: caltechlibrary/waystation@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          dry_run: true
          debug: true
```


### `save_errors` (default: `false`)

This corresponds to the parameter [`saveErrors`](https://github.com/JamieMagee/wayback#saveerrors) in the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine). A value of `true` will make the action tell the Wayback Machine to save web pages that return an HTTP status code in the range 4xx or 5xx. The default is `false`.


### `save_outlinks` (default: `true`)

This corresponds to the parameter [`saveOutlinks`](https://github.com/JamieMagee/wayback#saveOutlinks) in the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine). A value of `true` will make the action tell the Wayback Machine to archive external pages that are linked to from your GitHub Pages. The default in Waystation is `true` (unlike the default in the Wayback Machine GitHub Action) because the author finds this useful in producing a more complete archive of a GitHub Pages site.


### `save_screenshot` (default: `true`)

This corresponds to the parameter [`saveScreenshot`](https://github.com/JamieMagee/wayback#saveScreenshot) in the [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine). A value of `true` will make the action tell the Wayback Machine to save a screenshot of the page located at the GitHub Pages URL. The default in Waystation is `true` (unlike the default in the Wayback Machine GitHub Action) because the author finds this useful in producing a more complete archive of a GitHub Pages site.



## Getting help

If you find an issue, please submit it in [the GitHub issue tracker](https://github.com/caltechlibrary/waystation/issues) for this repository.


## Contributing

Your help and participation in enhancing Waystation is welcome!  Please visit the [guidelines for contributing](https://github.com/caltechlibrary/waystation/blob/main/CONTRIBUTING.md) for some tips on getting started.


## License

Software produced by the Caltech Library is Copyright © 2022 California Institute of Technology.  This software is freely distributed under a BSD-style license.  Please see the [LICENSE](LICENSE) file for more information.


## Acknowledgments

This work was funded by the California Institute of Technology Library.

Waystation makes use of the excellent [Wayback Machine GitHub Action](https://github.com/marketplace/actions/wayback-machine) by [Jaime Magee](https://github.com/JamieMagee).
