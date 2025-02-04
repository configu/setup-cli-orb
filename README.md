# configu/setup-cli-orb

[![CircleCI Build Status](https://circleci.com/gh/configu/setup-cli-orb.svg?style=shield "CircleCI Build Status")](https://circleci.com/gh/configu/setup-cli-orb) [![CircleCI Orb Version](https://badges.circleci.com/orbs/configu/setup-cli-orb.svg)](https://circleci.com/orbs/registry/orb/configu/setup-cli-orb) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

The configu/setup-cli-orb orb contains a bash command that sets up Configu CLI in your CircleCI workflow by downloading a specific version of Configu CLI and adding it to the `PATH`.

After you've used the orb's setup command, subsequent steps in the same job can run arbitrary Configu CLI commands. All of Configu commands work exactly like they do on your local command line.

## Usage

The default configuration installs the latest version of Configu CLI

```yaml
version: 2.1
orbs:
  configu: configu/setup-cli-orb@X.Y.Z

jobs:
  use-configu:
    docker:
      - image: cimg/base:stable
    steps:
      - configu/setup

workflows:
  deploy:
    jobs:
      - use-configu
```

A specific version of Configu CLI can be installed.

```yaml
steps:
  - configu/setup:
      version: 0.4.4
  - run: configu --version
```

Credentials for `Configu store` ([app.configu.com](https://app.configu.com/)) can be configured.

```yaml
jobs:
  use-configu:
    steps:
      - configu/setup
      - run: configu store --name "configu" --uri "configu://-"
      - run: configu export --set "production" --schema "path/to/schema.cfgu.json"

workflows:
  deploy:
    jobs:
      - use-configu:
        # defines $CONFIGU_ORG and $CONFIGU_TOKEN
        context: configu-credentials-context
```

## Parameters

The orb supports the [following parameters](https://github.com/configu/setup-cli-orb/blob/main/src/commands/setup.yml#L4).

## License

This orb is licensed under [Apache License 2.0](https://github.com/configu/setup-cli-orb/blob/main/LICENSE).

## References
- [Configu SaaS platform (app.configu.com)](https://app.configu.com/)
- [Configu Documentation](https://configu.com/docs)
- [CircleCI Orb Registry Page](https://circleci.com/orbs/registry/orb/configu/setup-cli-orb) - The official registry page of this orb for all versions, executors, commands, and jobs described.
- [CircleCI Orb Docs](https://circleci.com/docs/2.0/orb-intro/#section=configuration) - Docs for using, creating, and publishing CircleCI Orbs.
