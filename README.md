# [Drupal Starter](https://example.com/)

This is the Drupal Project Starter for the [ESINERGIA](https://esinergia.co) projects.

Features:

- Configured for Pantheon hosting
- Modern Drupal Installation with basic features
- Composer Installation
- DDEV Local Development Configuration
- CircleCI Deployment and Testing configuration

## ESINERGIA specific notes

- We use DDEV for local development


## Important links

Important links for the Drupal Starter:

* [Local URL]()
* [Project URL]()
* [GitHub Repo]()
* [GitHub Team]()
* [Pantheon Dev]()
* [Pantheon Dashboard]()
* [CircleCI]()
* [Teamwork]()


## Additional Documentation

- [Installation](docs/INSTALLATION.md) - for step by step instructions on
setting this repository up for the first time.
- [Developer Setup Instructions](docs/DEVELOP.md) - Developers start here to get
 setup.
- [About](docs/ABOUT.md) - for details on how this repository is set up and the
reasoning behind it.
- [Testing](docs/TESTING.md) - Details about all the testing available in this
project.
- [Creating Default Content](docs/DEFAULT_CONTENT.md) - Instructions on how to
use the Default Content module to create default content for a recipe.


## Theme Commands and Setup Documentation
- [Saplings Child](docs/SAPLINGS_THEME.md) - Current theme based on
ui_suite_bootstrap
- [Emulsify](docs/EMULSIFY.md) - Basic theme was built from
Emulsify. 

## Local Development with DDEV

### Installing DDEV

If you don't have DDEV installed:

1. [Install DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/)
2. Ensure you have a compatible Docker provider such as Docker Desktop,
   OrbStack, or Lima:
   [Docker Installation](https://ddev.readthedocs.io/en/stable/users/install/docker-installation/)

### Configure Pantheon Access

Install [Terminus](https://docs.pantheon.io/terminus), you'll use it to send commands to the Pantheon environment.

Generate a [Pantheon Machine Token](https://pantheon.io/docs/machine-tokens/)
and add it to your global DDEV config at `~/.ddev/global_config.yaml`:

```yaml
web_environment:
  - TERMINUS_MACHINE_TOKEN=your_token
```

## DDEV Commands

The following commands are available with DDEV and should be prefixed with
the command `ddev`.

| Command Name             | Container | Short Description                                     | Usage Syntax                        |
|--------------------------|-----------|-------------------------------------------------------|-------------------------------------|
| `cypress`                | host      | Run Cypress commands with optional environment target | `ddev cypress [command]`            |
| `cypress-users`          | host      | Create default admin user for Cypress testing         | `ddev cypress-users`                |
| `init`                   | host      | Initialize local development environment              | `ddev init`                         |
| `install-cypress`        | host      | Install node packages for Cypress on local machine    | `ddev install-cypress`              |
| `open`                   | host      | Open the project URL in the default browser           | `ddev open`                         |
| `phpmyadmin`             | host      | Launch PhpMyAdmin                                     | `ddev phpmyadmin`                   |
| `rebuild`                | host      | Run composer install and refresh database             | `ddev rebuild`                      |
| `refresh`                | host      | Pull database from hosting environment (Pantheon)     | `ddev refresh`                      |
| `testenv`                | host      | Initialize stack and testing environment              | `ddev testenv [env_name] [profile]` |
| `install-critical-tools` | web       | Install tools needed for Critical CSS generation      | `ddev install-critical-tools`       |
| `install-theme-tools`    | web       | Install and set up theme development tools            | `ddev install-theme-tools`          |
| `migrate-prep-db`        | web       | Create and configure a migration database             | `ddev migrate-prep-db`              |
| `npm`                    | web       | Run npm commands inside the theme directory           | `ddev npm`                          |
| `npx`                    | web       | Run npx commands inside the theme directory           | `ddev npx`                          |
| `recipe-apply`           | web       | Apply a Drupal recipe                                 | `ddev recipe-apply <recipe-path>`   |
| `recipe-unpack`          | web       | Unpack a Drupal recipe into composer.json             | `ddev recipe-unpack [package-name]` |
| `tickle`                 | web       | Continuously wake a Pantheon environment              | `ddev tickle`                       |
| `uuid-rm`                | web       | Remove UUIDs and \_core metadata from config files    | `ddev uuid-rm [path/to/folder]`     |

### Still to do for DDEV

- [ ] Add support for Pantheon Solr
- [ ] Add command: `migrate-prep-db`
- [ ] Add command: `config-capture`
- [ ] Add command: `critical`
- [ ] Add command: `release`

## Composer Commands

The following commands are available with Composer and should be prefixed with
the command `fin composer`.

| Command               | Description                                                        |
|-----------------------|--------------------------------------------------------------------|
| `lint-php`            | Analyzes custom modules for programmatic and stylistic errors.     |
| `code-sniff-modules`  | Runs PHPcs on the custom modules folder.                           |
| `code-sniff-themes`   | Runs PHPcs on the custom themes folder.                            |
| `code-sniff`          | Runs `code-sniff-modules` and `code-sniff-themes`.                 |
| `code-fix-modules`    | Runs PHPcbf on the custom modules folder.                          |
| `code-fix-themes`     | Runs PHPcbf on the custom themes folder.                           |
| `code-fix`            | Runs `code-fix-modules` `code-fix-themes` `rector-fix` `lint-php`. |
| `phpstan`             | PHPStan finds errors in custom modules and themes.                 |
| `rector-modules`      | Dry run of finding deprecations in custom modules.                 |
| `rector-themes`       | Dry run of finding deprecations in custom themes.                  |
| `rector-fix-modules`  | Refactors deprecations on the custom modules folder.               |
| `rector-fix-themes`   | Refactors deprecations on the custom themes folder.                |
| `rector-fix`          | Runs `rector-fix-modules` and `rector-fix-themes`.                 |
| `twig-lint-modules`   | Runs Twig-CS-Fixer on the custom modules folder.                   |
| `twig-lint-themes`    | Runs Twig-CS-Fixer on the custom themes folder.                    |
| `twig-lint`           | Runs `twig-lint-modules` and `twig-lint-themes`.                   |
| `twig-fix-modules`    | Runs Twig-CS-Fixer with the fix option on custom modules.          |
| `twig-fix-themes`     | Runs Twig-CS-Fixer with the fix option on custom themes.           |
| `twig-fix`            | Runs `twig-fix-modules` and `twig-fix-themes`.                     |
| `code-check`          | Runs `phpstan` `rector-modules` `rector-themes` `code-sniff`.      |
| `prepare-for-pantheon`| Used by CircleCI for Pantheon.                                     |
| `build-assets`        | Used by CircleCI for Pantheon.                                     |
| `post-autoload-dump`  | Used by CircleCI for Pantheon.                                     |


## Deployments

### GitHub to Pantheon
Deployments to the dev Pantheon environment are managed through CircleCI.

Pull requests will build a MultiDev environment then update the PR with a
comment. We also have Lighthouse testing and other audits enabled.

Merges to `main` will merge and deploy the GitHub code to the Pantheon dev
environment.

### Pantheon dev to prod deployments
1. Go to the project dashboard on Pantheon.
1. Backup databases for Test and Dev.
    1. To accomplish this you can go to the backups tab and backup everything
    or go to Database/Files and under Export 'export the database'.
1. Go to the environment you want to deploy to and make note of the tickets
that are ready to deploy, document these in the deploy log message.
1. Once content has been deployed clone the Test database down to Dev.
1. Pull the database locally, make sure there are no config changes
that need to be committed to code.
If there are changes, commit those and deploy.
1. Tell the appropriate Slack channel that a deployment has taken place
and include which tickets were deployed.
