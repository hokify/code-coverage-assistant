> 🛑 Archived, not used anymore, see https://github.com/hokify/hokify/pull/11221

# Code Coverage Assistant

[![CI](https://github.com/peter-evans/create-pull-request/workflows/CI/badge.svg)](https://github.com/ScaCap/code-coverage-assistant/actions?query=workflow%3ACI)

> [GitHub Action](https://help.github.com/en/actions) to assist the pull request with code coverage stats

-   ✅ &nbsp;Code coverage comment for monorepo
-   ✅ &nbsp;Code coverage comment for single repo
-   ✅ &nbsp;Code coverage diff from base branch

The report is based on the lcov coverage report generated by your test runner.

## Usage

Just add this action to one of your [workflow files](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow):

```yml
- name: Add coverage comment
  uses: ScaCap/code-coverage-assistant@v1
```

### Action inputs

The possible inputs for this action are:

| Parameter                           | Description                                                                                                                                                                      | Default                |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `github-token` (**Required**)       | Github token used for posting the comment. To use the key provided by the GitHub action runner, use `${{ secrets.GITHUB_TOKEN }}`.                                               |                        |
| `monorepo-base-path` (**Optional**) | The location of your monrepo `packages` path                                                                                                                                     |                        |
| `lcov-file` (**Optional**)          | The location of the lcov file to read the coverage report. `Needed only for single repos`                                                                                        | `./coverage/lcov.info` |
| `lcov-base` (**Optional**)          | The location of the lcov file resulting from running the tests in the base branch. When this is set a diff of the coverage percentages is shown. `Needed only for single repos`. |                        |

## Examples

### Code coverage comment for monorepo

```yml
uses: ScaCap/code-coverage-assistant@v1
with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    monorepo-base-path: "./packages"
```

![](/assets/example_monorepo.png)

### Code coverage comment for single repo

```yml
uses: ScaCap/code-coverage-assistant@v1
with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    lcov-file: "./app/coverage/lcov.info"
```

![](/assets/example_single_repo.png)

### Code coverage comment with diff

⚠️ &nbsp;Note: This config expects a `lcov-base.info` coverage file for base branch in your `.coverage` dir

```yml
uses: ScaCap/code-coverage-assistant@v1
with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    monorepo-base-path: "./packages"
```

![](/assets/example_diff.png)

## Development

### Contributing

Contributions are encouraged! Fork this repo and open a pull request.

### Commands

| command  | description                                                                                               |
| -------- | --------------------------------------------------------------------------------------------------------- |
| `test`   | Run the unit tests                                                                                        |
| `eslint` | Run eslint on all applicable files                                                                        |
| `format` | Run prettier on all applicable files                                                                      |
| `build`  | build the dist file. You are required to run this locally in order to build the dist before opening a PR. |

### Releasing

This action follows [semantic versioning](https://semver.org/).

#### Creating a release

-   Ensure master is up to date with all the changes for the next release
-   In the [GitHub releases page](https://github.com/ScaCap/code-coverage-assistant/releases), click "draft a new release"
    -   Choose a tag matching this pattern: `vX.X.X`
    -   Choose `master` as the target
    -   Use the exact tag as the release title
    -   Write a description containing all the changes since the last release, and detailing any breaking changes
    -   Choose "Publish Release"
-   Github will create the release and add the appropriate tag

## Acknowledgements

The initial code is based on [romeovs/lcov-reporter-action](https://github.com/romeovs/lcov-reporter-action).

Thanks to:

-   [ziishaned/jest-reporter-action](https://github.com/ziishaned/jest-reporter-action)
-   [slavcodev/coverage-monitor-action](https://github.com/slavcodev/coverage-monitor-action)
-   [ScaCap/code-coverage-assistant](https://github.com/ScaCap/code-coverage-assistant)

## License

[MIT](LICENSE)
