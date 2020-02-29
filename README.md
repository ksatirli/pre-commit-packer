# `pre-commit-packer`

> Packer-specific hooks for use with [pre-commit](https://pre-commit.com).

## Table of Contents

- [Requirements](#requirements)
- [Dependencies](#dependencies)
- [Usage](#usage)
  - [List of Hooks](#list-of-hooks)
  - [Configuring Hooks](#configuring-hooks)
  - [Using Docker](#using-docker)
- [Notes](#notes)
- [Author Information](#author-information)
- [License](#license)

## Requirements

- `pre-commit` version `1.15.0` or newer

## Dependencies

- `packer` for hooks that are prefixed with `packer-`
- `docker` for hooks that are prefixed with `docker-`

## Usage

The hooks in this repository can be used by adding the following stub to your `.pre-commit-config.yaml` file:

```yaml
---
  -
    repo: https://github.com/operatehappy/pre-commit-packer
    rev: 1.0.0
    hooks:
      - id: packer-validate
        files: packer*.json

      - id: packer-fix
        files: packer*.json

      - id: packer-validate-and-fix
        files: packer*.json
```

### List of Hooks

- `packer-validate` wraps the `validate` [command](https://packer.io/docs/commands/validate.html) to parse Packer template(s) and check template configuration against any used builders, provisioners, and processors.

- `packer-fix` wraps the `fix` [command](https://packer.io/docs/commands/fix.html) and attempts to fix (known) backwards incompatibilities in Packer template(s).

- `packer-validate-and-fix` wraps the `fix` [command](https://packer.io/docs/commands/fix.html) and additionally validates the fixed Packer template(s).

### Configuring Hooks

All hooks accept the following configuration options:

- `files` accepts a string (wildcards are supported) to define which file(s) the hook should target
- `args` accepts an array with one or more valid command-specific CLI arguments

The `files` configuration option defaults to `packer.json`

The `args` configuration option is most useful with the `packer-validate` action as it allows for passing additional arguments such as a path to a variables file (`-var-file=packer.vars.json`). The upstream documentation for the `validate` command provides an overview of all [available options](https://packer.io/docs/commands/validate.html#options).

### Using Docker

The hooks provided by `pre-commit-packer` support invocation through a containerized version of the Packer [Docker Image](https://hub.docker.com/r/hashicorp/packer).

This invocation defaults to the `light` [tag](https://hub.docker.com/r/hashicorp/packer/tags?page=1&name=light), but is otherwise functionally identical to a direct invocation via the `packer` binary.

The Docker-specific hooks are prefixed with `docker-`:

- `packer-validate` becomes `docker-packer-validate`
- `packer-fix` becomes `docker-packer-fix`
- `packer-validate-and-fix`  becomes `docker-packer-validate-and-fix`

## Notes

- In the [code example](#usage), the `1.0.0` version of `pre-commit-packer` has been selected. The [Releases](https://github.com/operatehappy/pre-commit-packer/releases) tab provides an overview of all available versions.

## Author Information

This repository is maintained by the contributors listed on [GitHub](https://github.com/operatehappy/pre-commit-packer/graphs/contributors)

Development of this module was sponsored by [Operate Happy](https://github.com/operatehappy).

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.
