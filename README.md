# DevX Tooling Docs Site

## Requirements

- Hugo Extended. See [Docsy Getting Started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) for more information.

> For Windows users, chocolatey hosts a [Hugo Extended package](https://chocolatey.org/packages/hugo-extended)

> For macOS users, when installing via `brew`, you will get the extended version by default.

- NodeJS with PostCSS installed.  This is available via `npm install`. See [Docsy Getting Started](https://www.docsy.dev/docs/getting-started/#install-postcss) for more information.

## Cloning
To install/update the Docsy theme use

`git submodule update --init --recursive --depth 50`

## Add Hugo Modules
Run the following command to download the pdkgo and prm modules and their dependencies:

`hugo mod get`

To update these hugo modules repeat the above commands.
## Run the Hugo server
Execute the following command to locally host the Hugo site with draft markdown files **enabled**:

`hugo server -D`

## Known problems and fixes
When using the `get` command, if the `cannot find module providing package` message appears for each dependency the problem can be fixed by running the command stated below, then re-running the `hugo mod get {repo_url}` commands stated in the "Add Hugo Modules" section:

`hugo mod clean --all`

## Updating the live site

The site will be deployed when commits are merged into the main branch of the repo.

Alternatively, the site can be deployed by running the [`github_pages` workflow action](https://github.com/puppetlabs/devx/actions/workflows/gh-pages.yml).
