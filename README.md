[![Action Run Using](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcssnr%2Fhomebrew-action%2Frefs%2Fheads%2Fmaster%2Faction.yml&query=%24.runs.using&logo=githubactions&logoColor=white&label=runs)](https://github.com/cssnr/homebrew-action/blob/master/action.yml)
[![Workflow Test](https://img.shields.io/github/actions/workflow/status/cssnr/homebrew-action/test.yaml?logo=cachet&label=test)](https://github.com/cssnr/homebrew-action/actions/workflows/test.yaml)
[![Workflow Lint](https://img.shields.io/github/actions/workflow/status/cssnr/homebrew-action/lint.yaml?logo=cachet&label=lint)](https://github.com/cssnr/homebrew-action/actions/workflows/lint.yaml)
[![GitHub Last Commit](https://img.shields.io/github/last-commit/cssnr/homebrew-action?logo=github&label=updated)](https://github.com/cssnr/homebrew-action/pulse)
[![GitHub Repo Size](https://img.shields.io/github/repo-size/cssnr/homebrew-action?logo=bookstack&logoColor=white&label=repo%20size)](https://github.com/cssnr/homebrew-action?tab=readme-ov-file#readme)
[![GitHub Contributors](https://img.shields.io/github/contributors-anon/cssnr/homebrew-action?logo=github)](https://github.com/cssnr/homebrew-action/graphs/contributors)
[![GitHub Discussions](https://img.shields.io/github/discussions/cssnr/homebrew-action?logo=github)](https://github.com/cssnr/homebrew-action/discussions)
[![GitHub Forks](https://img.shields.io/github/forks/cssnr/homebrew-action?style=flat&logo=github)](https://github.com/cssnr/homebrew-action/forks)
[![GitHub Repo Stars](https://img.shields.io/github/stars/cssnr/homebrew-action?style=flat&logo=github)](https://github.com/cssnr/homebrew-action/stargazers)
[![GitHub Org Stars](https://img.shields.io/github/stars/cssnr?style=flat&logo=github&label=org%20stars)](https://cssnr.github.io/)
[![Discord](https://img.shields.io/discord/899171661457293343?logo=discord&logoColor=white&label=discord&color=7289da)](https://discord.gg/wXy6m2X8wY)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-72a5f2?logo=kofi&label=support)](https://ko-fi.com/cssnr)

# Homebrew Action

<a title="Homebrew Action" href="https://actions.cssnr.com/" target="_blank">
<img alt="Homebrew Action" align="right" width="128" height="auto" src="https://raw.githubusercontent.com/cssnr/homebrew-action/refs/heads/master/.github/assets/logo.svg"></a>

- [Support](#Support)
- [Contributing](#Contributing)

🍺 Homebrew Action to Update Formula.

🛠️ This action is a work-in-progress and may have breaking changes.

```yaml
- name: 'Homebrew Action'
  uses: cssnr/homebrew-action@master
  with:
    url: https://cssnr.com/#app.zip # optional
    sha256: 784236d # optional
    version: ${{ github.ref_name }} # optional
    repo: cssnr/homebrew-tap
    formula: toml-run.rb # optional
    message: Bump toml-run # optional
    branch: master # optional
    token: ${{ secrets.HOMEBREW_PAT }}
```

✅ Auth with `token` or `app_id`/`app_private_key`.

| Input&nbsp;Name   |  Default&nbsp;Value   | Description&nbsp;of&nbsp;Input |
| :---------------- | :-------------------: | :----------------------------- |
| `url`             |           -           | URL to Update                  |
| `sha256`          |           -           | SHA256 to Update               |
| `version`         |           -           | Version to Update              |
| `repo`            |     ⚠️ _Required_     | Repository `{owner}/{name}`    |
| `formula`         |   `{repo-name}.rb`    | File relative to `Formula`     |
| `message`         | Bump `{.rb}` to `{v}` | Commit Message                 |
| `branch`          |   _Default Branch_    | Branch to Checkout/Commit      |
| `token`           |    `GITHUB_TOKEN`     | Access Token for `repo`        |
| `app_id`          |   _w/ private_key_    | App ID (and private key)       |
| `app_private_key` |      _w/ app_id_      | App Private Key (and id)       |

You must provide a `token` or an `app_id` + `app_private_key`.

You should also provide at least one of `url`, `sha256` or `version`.

To see how updates are applied, view: [src/update-formula.sh](src/update-formula.sh)

Example workflow with all inputs...

```yaml
- name: 'PyPi URL'
  id: url
  uses: cssnr/web-request-action@master
  with:
    method: 'GET'
    url: 'https://pypi.org/pypi/toml-run/${{ github.ref_name }}/json'
    path: '$.urls[?(@.packagetype=="sdist")]'

- name: 'Homebrew Action'
  uses: cssnr/homebrew-action@master
  with:
    url: ${{ fromJSON(steps.url.outputs.result).url }}
    sha256: ${{ fromJSON(steps.url.outputs.result).digests.sha256 }}
    version: ${{ github.ref_name }}
    repo: cssnr/homebrew-tap
    formula: toml-run.rb # .rb is optional
    message: Bump toml-run to ${{ github.ref_name }}
    branch: master
    app_id: 146360
    app_private_key: ${{ secrets.APP_PRIVATE_KEY }}
```

# Support

For general help or to request a feature, see:

- Q&A Discussion: https://github.com/cssnr/homebrew-action/discussions/categories/q-a
- Request a Feature: https://github.com/cssnr/homebrew-action/discussions/categories/feature-requests

If you are experiencing an issue/bug or getting unexpected results, you can:

- Report an Issue: https://github.com/cssnr/homebrew-action/issues
- Chat with us on Discord: https://discord.gg/wXy6m2X8wY
- Provide General Feedback: [https://cssnr.github.io/feedback/](https://cssnr.github.io/feedback/?app=Update%20Release%20Notes)

For more information, see the CSSNR [SUPPORT.md](https://github.com/cssnr/.github/blob/master/.github/SUPPORT.md#support).

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
- [Upload Release Action](https://github.com/cssnr/upload-release-action?tab=readme-ov-file#readme)
- [Check Build Action](https://github.com/cssnr/check-build-action?tab=readme-ov-file#readme)
- [Web Request Action](https://github.com/cssnr/web-request-action?tab=readme-ov-file#readme)
- [Get Commit Action](https://github.com/cssnr/get-commit-action?tab=readme-ov-file#readme)

<details><summary>❔ Unpublished Actions</summary>

These actions are not published on the Marketplace, but may be useful.

- [cssnr/create-files-action](https://github.com/cssnr/create-files-action?tab=readme-ov-file#readme) - Create various files from templates.
- [cssnr/draft-release-action](https://github.com/cssnr/draft-release-action?tab=readme-ov-file#readme) - Keep a draft release ready to publish.
- [cssnr/homebrew-action](https://github.com/cssnr/homebrew-action?tab=readme-ov-file#readme) - Homebrew formula update action.
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
