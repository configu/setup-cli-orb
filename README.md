# configu/setup-cli-orb

[![CircleCI Build Status](https://circleci.com/gh/configu/setup-cli-orb.svg?style=shield "CircleCI Build Status")](https://circleci.com/gh/configu/setup-cli-orb) [![CircleCI Orb Version](https://badges.circleci.com/orbs/configu/setup-cli-orb.svg)](https://circleci.com/orbs/registry/orb/configu/setup-cli-orb) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

The configu/setup-cli-orb orb contains a bash command that sets up Configu CLI in your CircleCI workflow by downloading a specific version of Configu CLI and adding it to the `PATH`.

After you've used the orb's setup command, subsequent steps in the same job can run arbitrary Configu CLI commands. All of Configu commands work exactly like they do on your local command line.

## Usage

The default configuration installs the latest version of Configu CLI.

```yaml
version: 2.1
orbs:
  configu: configu/setup-cli-orb@1.0.0

jobs:
  deploy:
    docker:
      - image: cimg/base:stable
    steps:
      - configu/setup

workflows:
  deploy:
    jobs:
      - deploy
```

<!-- A specific version of Configu CLI can be installed.

```yaml
steps:
  - configu/setup:
      version: 0.0.105
  - run: configu --version
``` -->

Credentials for Configu SaaS platform ([app.configu.io](https://app.configu.io/)) can be configured.

without login (uses "CONFIGU_" environment variables):
```yaml
jobs:
  deploy:
    context: configu-credentials-context
    steps:
      - configu/setup
```

with login:
```yaml
steps:
  - configu/setup:
      org: $CONFIGU_ORG
      token: $CONFIGU_TOKEN
```

## Parameters

The orb supports the [following parameters](https://github.com/configu/setup-cli-orb/blob/main/src/commands/setup.yml#L4).

## License

This orb is licensed under [Apache License 2.0](https://github.com/configu/setup-cli-orb/blob/main/LICENSE).

## References
- [Configu SaaS platform (app.configu.io)](https://app.configu.io/)
- [Configu Documentation](https://configu.io/docs)
- [CircleCI Orb Registry Page](https://circleci.com/orbs/registry/orb/configu/setup-cli-orb) - The official registry page of this orb for all versions, executors, commands, and jobs described.
- [CircleCI Orb Docs](https://circleci.com/docs/2.0/orb-intro/#section=configuration) - Docs for using, creating, and publishing CircleCI Orbs.