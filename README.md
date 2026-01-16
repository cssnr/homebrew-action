[![GitHub Tag Major](https://img.shields.io/github/v/tag/cssnr/homebrew-action?sort=semver&filter=!v*.*&logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/homebrew-action/tags)
[![GitHub Tag Minor](https://img.shields.io/github/v/tag/cssnr/homebrew-action?sort=semver&filter=!v*.*.*&logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/homebrew-action/releases)
[![GitHub Release Version](https://img.shields.io/github/v/release/cssnr/homebrew-action?logo=git&logoColor=white&labelColor=585858&label=%20)](https://github.com/cssnr/homebrew-action/releases/latest)
[![Action Run Using](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcssnr%2Fhomebrew-action%2Frefs%2Fheads%2Fmaster%2Faction.yml&query=%24.runs.using&logo=githubactions&logoColor=white&label=runs)](https://github.com/cssnr/homebrew-action/blob/master/action.yml)
[![Workflow Release](https://img.shields.io/github/actions/workflow/status/cssnr/homebrew-action/release.yaml?logo=checkmarx&logoColor=white&label=release)](https://github.com/cssnr/homebrew-action/actions/workflows/release.yaml)
[![Workflow Test](https://img.shields.io/github/actions/workflow/status/cssnr/homebrew-action/test.yaml?logo=checkmarx&logoColor=white&label=test)](https://github.com/cssnr/homebrew-action/actions/workflows/test.yaml)
[![Workflow Lint](https://img.shields.io/github/actions/workflow/status/cssnr/homebrew-action/lint.yaml?logo=checkmarx&logoColor=white&label=lint)](https://github.com/cssnr/homebrew-action/actions/workflows/lint.yaml)
[![GitHub Last Commit](https://img.shields.io/github/last-commit/cssnr/homebrew-action?logo=github&label=updated)](https://github.com/cssnr/homebrew-action)
[![Codeberg Last Commit](https://img.shields.io/gitea/last-commit/cssnr/homebrew-action/master?gitea_url=https%3A%2F%2Fcodeberg.org%2F&logo=codeberg&logoColor=white&label=updated)](https://codeberg.org/cssnr/homebrew-action)
[![GitHub Repo Size](https://img.shields.io/github/repo-size/cssnr/homebrew-action?logo=buffer&label=repo%20size)](https://github.com/cssnr/homebrew-action?tab=readme-ov-file#readme)
[![GitHub Contributors](https://img.shields.io/github/contributors-anon/cssnr/homebrew-action?logo=southwestairlines)](https://github.com/cssnr/homebrew-action/graphs/contributors)
[![GitHub Issues](https://img.shields.io/github/issues/cssnr/homebrew-action?logo=codeforces&logoColor=white)](https://github.com/cssnr/homebrew-action/issues)
[![GitHub Discussions](https://img.shields.io/github/discussions/cssnr/homebrew-action?logo=rocketdotchat&logoColor=white)](https://github.com/cssnr/homebrew-action/discussions)
[![GitHub Forks](https://img.shields.io/github/forks/cssnr/homebrew-action?style=flat&logo=forgejo&logoColor=white)](https://github.com/cssnr/homebrew-action/forks)
[![GitHub Repo Stars](https://img.shields.io/github/stars/cssnr/homebrew-action?style=flat&logo=gleam&logoColor=white)](https://github.com/cssnr/homebrew-action/stargazers)
[![GitHub Org Stars](https://img.shields.io/github/stars/cssnr?style=flat&logo=apachespark&logoColor=white&label=org%20stars)](https://cssnr.github.io/)
[![Discord](https://img.shields.io/discord/899171661457293343?logo=discord&logoColor=white&label=discord&color=7289da)](https://discord.gg/wXy6m2X8wY)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-72a5f2?logo=kofi&label=support)](https://ko-fi.com/cssnr)

# Homebrew Action

<a title="Homebrew Action" href="https://actions.cssnr.com/" target="_blank">
<img alt="Homebrew Action" align="right" width="128" height="auto" src="https://raw.githubusercontent.com/cssnr/homebrew-action/refs/heads/master/.github/assets/logo.svg"></a>

- [Features](#Features)
- [Inputs](#Inputs)
  - [Permissions](#Permissions)
- [Outputs](#Outputs)
- [Examples](#Examples)
- [Support](#Support)
- [Contributing](#Contributing)

🍺 Homebrew Action to Update Formula `url`, `version` and `sha256`.

✅ Auth with `token` or `app_id`/`app_private_key` for Verified commits.

[![Verified Commit](https://raw.githubusercontent.com/smashedr/repo-images/refs/heads/master/homebrew/commit.jpg)](https://github.com/cssnr/homebrew-tap/?tab=readme-ov-file#readme)

```yaml
- name: 'Homebrew Action'
  uses: cssnr/homebrew-action@master
  with:
    url: https://cssnr.com/#app.zip # optional
    sha256: a6c550e966e # calculated from url
    version: ${{ github.ref_name }} # optional
    calculate: true # true is default, optional
    repo: cssnr/homebrew-tap # set to your tap
    formula: toml-run.rb # optional
    message: Bump toml-run # optional
    branch: master # optional
    token: ${{ secrets.HOMEBREW_PAT }} # or app_id
    commit: true # true is default, optional
    pull: false # false is default, optional
```

For more workflow examples, see the [Examples](#examples) section.

For an example Tap, see: <https://github.com/cssnr/homebrew-tap>

To test your formula, see: [cssnr/homebrew-tap/.github/workflows/test.yaml](https://github.com/cssnr/homebrew-tap/blob/master/.github/workflows/test.yaml)

## Features

- Works on any Custom Tap
- Update `url`, `sha256`, or `version`
- Calculate `sha256` from the `url`
- Automatically find `formula` file
- Commit: Commit and Push to a `branch`
- Pull: Optionally create a `pull` Request
- Auth with Token or App ID and Key
- Create Verified commits to the `repo`
- Customize all options with [Inputs](#inputs)
- All data accessible via [Outputs](#outputs)

## Inputs

| Input&nbsp;Name   |   Default&nbsp;Value    | Description&nbsp;of&nbsp;Input |
| :---------------- | :---------------------: | :----------------------------- |
| `url`             |            -            | Formula URL to update          |
| `sha256`          | _calculated from `url`_ | Formula Hash to update         |
| `version`         |            -            | Formula Version to update      |
| `calculate`       |         `true`          | Calculate `sha256` from `url`  |
| `repo`            |       _Required_        | Repository `{owner}/{name}`    |
| `formula`         |    `{repo-name}.rb`     | File relative to `Formula`     |
| `message`         |  Bump `{.rb}` to `{v}`  | Commit Message                 |
| `branch`          |    _Default Branch_     | Branch to Checkout             |
| `token`           |     `GITHUB_TOKEN`      | Access Token for `repo`        |
| `app_id`          |    _w/ private_key_     | App ID (and private key)       |
| `app_private_key` |       _w/ app_id_       | App Private Key (and id)       |
| `commit`          |         `true`          | Commit and Push Changes        |
| `pull`            |         `false`         | Create a Pull Request          |

You should provide at least one of `url`, `sha256` or `version` to update.

The `sha256` is calculated from the `url` unless the `sha256` is provided or `calculate` is set to `false`.

To `commit` you must provide a `token` or an `app_id` + `app_private_key`. _See [Permissions](#permissions)._

To create a `pull` request your token/app must have `pull-requests: write`. _See [Permissions](#permissions)._

To see how updates are applied, view the: [src/update-formula.sh](src/update-formula.sh)

### Permissions

The default `GITHUB_TOKEN` will not work unless workflow is in the same `repo` as the tap.

Therefore, you need to create a Personal Access or Fine Grained Access Token.

Alternatively, you can create and use a GitHub App ID and Private Key.

**In all cases, you need `contents: write`.**

```yaml
permissions:
  contents: write
```

If you set `pull: true` you must grant `pull-requests: write` permissions.

```yaml
permissions:
  pull-requests: write
```

_Note: these are not workflow permissions, they are Token/App permissions._

## Outputs

| Output    | Description       |
| :-------- | :---------------- |
| `formula` | Formula File      |
| `message` | Commit Message    |
| `branch`  | Branch Used       |
| `sha256`  | Formula Hash      |
| `sha`     | Commit Hash       |
| `pull`    | Pull Request JSON |

The commit `sha` and `pull` json are only set if `commit` and/or `pull` is enabled.

Tip: you can parse the `pull` output with `fromJSON`.

```yaml
- run: echo html_url ${{ fromJSON(steps.pull.outputs.pull).html_url }}
```

## Examples

Minimal with Provided URL.

```yaml
- name: 'Homebrew Action'
  uses: cssnr/homebrew-action@master
  with:
    url: https://... # used to calculate the sha256
    repo: cssnr/homebrew-tap
    token: ${{ secrets.REPO_TOKEN }}
```

Update from a GitHub Release.

```yaml
- name: 'Upload Release'
  id: release
  uses: cssnr/upload-release-action@v1
  with:
    files: dist/asset.zip

- name: 'Homebrew Action'
  uses: cssnr/homebrew-action@master
  with:
    url: ${{ fromJSON(steps.release.outputs.assets)[1].browser_download_url }}
    sha256: ${{ fromJSON(steps.release.outputs.assets)[1].digest }}
    version: ${{ github.ref_name }} # only set if you use version
    repo: cssnr/homebrew-tap
    formula: get-contributors.rb # .rb is optional
    message: Bump get-contributors.rb to ${{ github.ref_name }}
    branch: master
    app_id: 146360
    app_private_key: ${{ secrets.APP_PRIVATE_KEY }}
```

Update from a PyPi Release.

```yaml
- name: 'PyPi Request'
  id: request
  uses: cssnr/web-request-action@v2
  with:
    method: 'GET'
    url: 'https://pypi.org/pypi/toml-run/${{ github.ref_name }}/json'
    path: '$.urls[?(@.packagetype=="sdist")]'

- name: 'Homebrew Action'
  id: homebrew
  uses: cssnr/homebrew-action@master
  with:
    url: ${{ fromJSON(steps.request.outputs.result).url }}
    sha256: ${{ fromJSON(steps.request.outputs.result).digests.sha256 }}
    version: ${{ github.ref_name }} # only set if you use version
    repo: cssnr/homebrew-tap
    formula: t/toml-run.rb # t/ and .rb are optional
    message: Bump toml-run to ${{ github.ref_name }}
    branch: master
    app_id: 12345678
    app_private_key: ${{ secrets.APP_PRIVATE_KEY }}
    pull: true

- name: 'Echo Outputs'
  continue-on-error: true
  run: |
    echo "formula: ${{ steps.homebrew.outputs.formula }}"
    echo "message: ${{ steps.homebrew.outputs.message }}"
    echo "branch: ${{ steps.homebrew.outputs.branch }}"
    echo "sha256: ${{ steps.homebrew.outputs.sha256 }}"
    echo "sha: ${{ steps.homebrew.outputs.sha }}"
    echo "pull: ${{ steps.homebrew.outputs.pull }}"
    echo "pull url: ${{ fromJSON(steps.pull.outputs.pull).html_url }}"
```

For more examples, check out other projects using this action:  
<https://github.com/cssnr/homebrew-action/network/dependents>

# Support

If you run into any issues or need help getting started, please do one of the following:

- [Report an Issue](https://github.com/cssnr/homebrew-action/issues)
- [Q&A Discussion](https://github.com/cssnr/homebrew-action/discussions/categories/q-a)
- [Request a Feature](https://github.com/cssnr/homebrew-action/issues/new?template=1-feature.yaml)
- [Chat with us on Discord](https://discord.gg/wXy6m2X8wY)

[![Features](https://img.shields.io/badge/features-brightgreen?style=for-the-badge&logo=rocket&logoColor=white)](https://github.com/cssnr/homebrew-action/issues/new?template=1-feature.yaml)
[![Issues](https://img.shields.io/badge/issues-red?style=for-the-badge&logo=southwestairlines&logoColor=white)](https://github.com/cssnr/homebrew-action/issues)
[![Discussions](https://img.shields.io/badge/discussions-blue?style=for-the-badge&logo=livechat&logoColor=white)](https://github.com/cssnr/homebrew-action/discussions)
[![Discord](https://img.shields.io/badge/discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/wXy6m2X8wY)

# Contributing

If you would like to submit a PR, please review the [CONTRIBUTING.md](#contributing-ov-file).

Please consider making a donation to support the development of this project
and [additional](https://cssnr.com/) open source projects.

[![Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cssnr)

[![Actions Tools](https://raw.githubusercontent.com/smashedr/repo-images/refs/heads/master/actions/actions-tools.png)](https://actions-tools.cssnr.com/)

Additionally, you can support other [GitHub Actions](https://actions.cssnr.com/) I have published:

- [Stack Deploy Action](https://github.com/cssnr/stack-deploy-action?tab=readme-ov-file#readme)
- [Portainer Stack Deploy Action](https://github.com/cssnr/portainer-stack-deploy-action?tab=readme-ov-file#readme)
- [Docker Context Action](https://github.com/cssnr/docker-context-action?tab=readme-ov-file#readme)
- [Actions Up Action](https://github.com/cssnr/actions-up-action?tab=readme-ov-file#readme)
- [Rhysd Actionlint Action](https://github.com/cssnr/actionlint-action?tab=readme-ov-file#readme)
- [Zensical Action](https://github.com/cssnr/zensical-action?tab=readme-ov-file#readme)
- [VirusTotal Action](https://github.com/cssnr/virustotal-action?tab=readme-ov-file#readme)
- [Homebrew Action](https://github.com/cssnr/homebrew-action?tab=readme-ov-file#readme)
- [Mirror Repository Action](https://github.com/cssnr/mirror-repository-action?tab=readme-ov-file#readme)
- [Update Version Tags Action](https://github.com/cssnr/update-version-tags-action?tab=readme-ov-file#readme)
- [Docker Tags Action](https://github.com/cssnr/docker-tags-action?tab=readme-ov-file#readme)
- [TOML Action](https://github.com/cssnr/toml-action?tab=readme-ov-file#readme)
- [Update JSON Value Action](https://github.com/cssnr/update-json-value-action?tab=readme-ov-file#readme)
- [JSON Key Value Check Action](https://github.com/cssnr/json-key-value-check-action?tab=readme-ov-file#readme)
- [Parse Issue Form Action](https://github.com/cssnr/parse-issue-form-action?tab=readme-ov-file#readme)
- [Cloudflare Purge Cache Action](https://github.com/cssnr/cloudflare-purge-cache-action?tab=readme-ov-file#readme)
- [Mozilla Addon Update Action](https://github.com/cssnr/mozilla-addon-update-action?tab=readme-ov-file#readme)
- [Package Changelog Action](https://github.com/cssnr/package-changelog-action?tab=readme-ov-file#readme)
- [NPM Outdated Check Action](https://github.com/cssnr/npm-outdated-action?tab=readme-ov-file#readme)
- [Label Creator Action](https://github.com/cssnr/label-creator-action?tab=readme-ov-file#readme)
- [Algolia Crawler Action](https://github.com/cssnr/algolia-crawler-action?tab=readme-ov-file#readme)
- [Create Pull Action](https://github.com/cssnr/create-pull-action?tab=readme-ov-file#readme)
- [Upload Release Action](https://github.com/cssnr/upload-release-action?tab=readme-ov-file#readme)
- [Check Build Action](https://github.com/cssnr/check-build-action?tab=readme-ov-file#readme)
- [Web Request Action](https://github.com/cssnr/web-request-action?tab=readme-ov-file#readme)
- [Get Commit Action](https://github.com/cssnr/get-commit-action?tab=readme-ov-file#readme)

<details><summary>❔ Unpublished Actions</summary>

These actions are not published on the Marketplace, but may be useful.

- [cssnr/create-files-action](https://github.com/cssnr/create-files-action?tab=readme-ov-file#readme) - Create various files from templates.
- [cssnr/draft-release-action](https://github.com/cssnr/draft-release-action?tab=readme-ov-file#readme) - Keep a draft release ready to publish.
- [cssnr/env-json-action](https://github.com/cssnr/env-json-action?tab=readme-ov-file#readme) - Convert env file to json or vice versa.
- [cssnr/push-artifacts-action](https://github.com/cssnr/push-artifacts-action?tab=readme-ov-file#readme) - Sync files to a remote host with rsync.
- [smashedr/update-release-notes-action](https://github.com/smashedr/update-release-notes-action?tab=readme-ov-file#readme) - Update release notes.
- [smashedr/combine-release-notes-action](https://github.com/smashedr/combine-release-notes-action?tab=readme-ov-file#readme) - Combine release notes.

---

</details>

<details><summary>📝 Template Actions</summary>

These are basic action templates that I use for creating new actions.

- [javascript-action](https://github.com/smashedr/javascript-action?tab=readme-ov-file#readme) - JavaScript
- [typescript-action](https://github.com/smashedr/typescript-action?tab=readme-ov-file#readme) - TypeScript
- [py-test-action](https://github.com/smashedr/py-test-action?tab=readme-ov-file#readme) - Dockerfile Python
- [test-action-uv](https://github.com/smashedr/test-action-uv?tab=readme-ov-file#readme) - Dockerfile Python UV
- [docker-test-action](https://github.com/smashedr/docker-test-action?tab=readme-ov-file#readme) - Docker Image Python

Note: The `docker-test-action` builds, runs and pushes images to [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry).

---

</details>

For a full list of current projects visit: [https://cssnr.github.io/](https://cssnr.github.io/)
