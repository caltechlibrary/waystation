# Change log for Waystation

## Version 1.6 (2024-01-02)

Changes in this release:

* Fixed bug in issue #3. The default value of `dry_run` is now `false`, as it was supposed to be.
* Removed the `save_errors` parameter; it doesn't seem useful for Waystation and just adds complexity.
* Revised and improved the sample workflow.
* Added a file (`sample-workflow.yml`) for the sample workflow, to make copying easier.
* Updated file headers to be more streamlined and include a missing copyright statement.
* Updated the year in the `LICENSE` file.


## Version 1.5 (2022-11-22)

This release updates the version of the [Wayback](https://github.com/marketplace/actions/wayback-machine) action used by Waystation to the latest version (thanks to PR #1 from [Jamie Magee](https://github.com/JamieMagee)), and corrects the misspelling of the author's name (thanks to PR #2 from [Jamie Magee](https://github.com/JamieMagee)).


## Version 1.4 (2022-11-21)

This release adds a GitHub Pages documentation site for docs, which not only seems fitting considering the purpose of this GitHub Action, but also helps with testing. It also polishes up the GitHub Action a little bit.


## Version 1.3

This version fixes a gaff in the step for getting the repository path.


## Version 1.2

This version fixes a failure to pass GITHUB_TOKEN to the composite workflow.


## Version 1.1

This version fixes a bug (missing `shell` parameters) in `action.yml`


## Version 1.0

First release.
