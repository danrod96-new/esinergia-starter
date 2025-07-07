# Installation

Instructions on how to install and configure this Drupal project template for
Pantheon, CircleCI, and the local DDEV development.

## Installer method

### Create a GitHub repository for the project.

Install [GitHub CLI](https://cli.github.com/) if you don't have it. Please check out the site to install the CLI on many Operating Systems.

Install the [Repo Config GH CLI extension](https://github.com/twelvelabs/gh-repo-config) `gh extension install twelvelabs/gh-repo-config`

#### Create a GitHub team (Optional)

`gh api /orgs/<organization>/teams --method POST -f org=<organization> -f name=<team_name> -f privacy=closed`

* `organization` -  The GitHub organization name.
* `repo_name` - The name of your new repository.
* `team_name` - The name of the team created.


#### Create and clone your new repository

`cd ~/Projects` (Or where ever you keep your sites.)

`gh repo create <organization>/<repo_name> --template danrod96-new/esinergia-starter --private --team <team_name> --clone`

Example
`gh repo create danrod96-new/new_test_esinergia_site --template danrod96-new/esinergia-starter --public --clone`

`cd new_test_esinergia_site`

NOTE: Use `--public` instead of `--private` for a public repository.


#### Configure GitHub Repository Configuration

Edit the three files in `/.github/config/`

* `/branch-protection/main.json` - Configures branch protection rules on the `main` branch. [Branch Rules Reference](https://docs.github.com/en/rest/branches/branch-protection?apiVersion=2022-11-28#update-branch-protection)
* `repo.json` - Configures the repositories' settings. [Repository Update Reference](https://docs.github.com/en/rest/repos/repos?apiVersion=2022-11-28#update-a-repository)
* `topics.json` - Configures the repositories' topics/tags.

Run `gh repo-config apply` to apply the configuration to GitHub.

-----

### Create the site in Pantheon

Dont forget to run:

`terminus auth:login --email=yourname@youremail.ca`

Then run

`terminus site:create --org=<org_id> -- <site_name> <label> <upstream_id>`

Where

* `site_name` - Machine name of the project
* `label` - Friendly project name
* `upstream_id` - Currently *Drupal 11 Start State* - `e8efc734-962c-44ef-ae30-9c6b1330a135`

You can run `terminus upstream:list` to see all:

![Contents of terminus upstream:list](https://github.com/danrod96-new/esinergia-starter/blob/main/docs/assets/esinegia-starter1.png)

* `org_id` - The UUID of your Pantheon organization.

You can run `terminus org:list` to see all:

![Contents of terminus upstream:list](https://github.com/danrod96-new/esinergia-starter/blob/main/docs/assets/esinegia-starter1.png)

Example:

`terminus site:create --org=affb90c8-d5ec-4e20-555-e6d39892cff2 -- new-test-esinergia-site "New Test ESINERGIA Site" e8efc734-962c-44ef-ae30-9c6b1330a13`

You see will an output like this:

```
$ terminus site:create --org=affb90c8-d5ec-4e20-94ab-e6d39892cff2 -- new-test-esinergia-site "New Test ESINERGIA Site" e8efc734-962c-44ef-ae30-9c6b1330a135
 [notice] Creating a new site...
 [notice] Deploying CMS...
 [notice] Waiting for site availability...
 [notice] new-test-esinergia-site site has been created successfully and is available for use.
```

### Install Drupal using the minimal install profile

`terminus drush <site_name>.dev -- site-install minimal -y --site-name=<drupal_site_name> --account-name=<account_name> --account-mail=<account_mail> --site-mail=<site_mail>`

* `drupal_site_name` - Friendly name of the site.
* `account_name` - User 1's machine name.
* `account_mail` - User 1's email.
* `site_mail` - For Drupal system mailings.

Example:

`terminus drush 3393a6e8-c105-407a-a137-9b01c6ac38a6.dev -- site-install minimal -y --site-name="New Test ESINERGIA Site" --account-name=admin_esinergia --account-mail=danrod@esinergia.co`

You will an output like this:

```
$ terminus drush 3393a6e8-c105-407a-a137-9b01c6ac38a6.dev -- site-install minimal -y --site-name="New Test ESINERGIA Site" --account-name=admin_esinergia --account-mail=danrod@esinergia.co
 You are about to:
 * DROP all tables in your 'pantheon' database.

 // Do you want to continue?: yes.                                              

 [notice] Starting Drupal installation. This takes a while.
 [notice] Performed install task: install_select_language
 [notice] Performed install task: install_select_profile
 [notice] Performed install task: install_load_profile
 [notice] Performed install task: install_verify_requirements
 [notice] Performed install task: install_verify_database_ready
 [notice] Performed install task: install_base_system
 [notice] Performed install task: install_bootstrap_full
 [notice] Performed install task: install_profile_modules
 [notice] Performed install task: install_profile_themes
 [notice] Performed install task: install_install_profile
 [notice] Performed install task: install_configure_form
 [notice] Performed install task: install_finished
 [success] Installation complete.  User name: admin_esinergia  User password: D2pWbeqAxh
 [notice] Command: new-test-esinergia-site.dev -- drush site-install minimal [Exit: 0] (Attempt 1/1)
```

This will give you an username and a password to connect to the new pantheon instance

### Add Redis to the Pantheon site

`terminus redis:enable <site_id>`

Example:

```
$ terminus redis:enable 3393a6e8-c105-407a-a137-9b01c6ac38a6
 [notice] Enabled cacheserver for site
$
```

See [A note about Redis on Pantheon](#a-note-about-redis-on-pantheon) below.


### Configure CircleCI

@TODO See UI method below until this is documented.


### Site Build Drupal

@TODO See UI method below until this is documented.

-----

## UI Installation Method


### Create a new Drupal project.

![Create a new Drupal project](https://github.com/kanopi/drupal-starter/assets/7685811/a1926875-951d-473a-bf0f-146abf3ad1eb)


### Create a minimal site install

  ![Create a minimal site install](https://user-images.githubusercontent.com/1062456/130299368-effbdab3-87ec-435b-812a-cb5d50b1c430.png)


### Set the basic details for the site

  ![Set the basic details for the site](https://user-images.githubusercontent.com/1062456/130299369-e102b080-f94b-45ce-a706-08392e075c1a.png)


### Add Redis to the project

![Add redis to the project](https://user-images.githubusercontent.com/1062456/130299370-1e5564db-73dc-4ade-b086-5b7af27d7608.png)


### Configure Pantheon

* Go to the Pantheon dashboard for your project.
* Click on the Team tab.
* Click on Add organization
* Search for Kanopi Studios (Important: enter the full term (Kanopi Studios) to
find this - if you just enter Kanopi, you will end up with the wrong group and
things will not work).
* Select and add Kanopi Studios.


### Create a GitHub repository for the project.

* Go to [https://github.com/kanopi/drupal-starter](https://github.com/kanopi/drupal-starter)
* Click on "Use this template" button.
* Make the owner Kanopi and the repo private, then click "Create repository from
 template"
* In the new repo, click on Settings and then the Manage Access tab.
* Click on "Invite teams or people" button.
* Search for and add Kanopi Studios and grant them Read access.
* Click on "Add kanopicode to this repository"
* Still in Settings, click on the Branches tab.
* Click on Add Rule.
* Make Branch name pattern match your default branch (e.g., main).
* Select "Require pull request reviews before merging"
* Click Create button


### CircleCI project setup

* Go to
[CircleCI](https://app.CircleCI.com/projects/project-dashboard/github/kanopi/)
* Find your new project repo and click the "Set Up Project" button.
* Select the branch name option and select the main branch,
 and click on the "Lets go" button.
* Click on the gear for the project and click on the Advanced Settings tab.
* Enable "Only build pull request" and "Auto Cancel Builds" options.
[Update settings](https://user-images.githubusercontent.com/1062456/130299362-9c04c3e2-e59a-4e73-8dfa-816d8d5316f4.png)


-----

## Drupal setup

We have removed all opinions about which modules should be installed in Drupal.

Instead, we have created the [kanopi/saplings](https://www.github.com/kanopi/saplings)
Drupal recipe to require, intsall, and configure the modules and content types we 
use on most Drupal builds.  Please visit that repository to continue using that.


### A note about Redis on Pantheon.

* We enabled Redis on Pantheon in an earlier step.
* Before it can be configured, the Drupal Redis module needs to be enabled and
pushed to Pantheon.  It is a two commit process.
* Once the module has been enabled and verified on Pantheon:
  * Uncomment the Redis config in `/assets/pantheon_setting_defaults.inc`.
  * Git add, commit and push the change.
  * Submit a PR in the github repo.
  * Validate CircleCI job and deployment to multidev.
  * Merge the PR.
  * Validate CircleCI job deployment and Pantheon Dev site.


### Configuring Cron on CircleCI for use with Pantheon

Cron can be ran two different ways.

1. Accessing through the URL provided on the Status Report.
2. Using Drush through Terminus.

What can happen sometimes is that we don't configure cron to run which then makes it so
we manually need to run it. Within the `.circleci/config.yml` there is now a workflow
titled `run_cron` that will run a terminus command then drush then the core cron command.

Running the URL process on Pantheon can timeout and is sometimes not recommended for a
Cron Process that takes longer than 60 seconds.

Running Drush through Terminus is the next possible way. With this there are no time-out
restrictions. This is usually done by running the following command in the terminal.

```sh
terminus drush site-id.site-env -- core:cron
```

We have made it so that this can be automated and done through CircleCI.

To configure

* Go to the project in CircleCI.
* Click on Project Settings
* Click Triggers
* Click Add Trigger
* Select Schedule from the Trigger type
* Configure the Trigger
  * Trigger Name: (The name should be prefixed with the words "cron job", example "cron job test")
  * Trigger Description: (This is a description about what this trigger does)
  * Pipeline to run: (This can stay as is)
  * Repeats: Weekly
  * Repeats on these days: (Select all 7 days)
  * Repeats on these months: (Select all 12 months)
  * Start Time: (See Note 1)
  * Repeats Per Hour: (See Note 2)
  * Branch of Tag Name: (Set to whatever the name of the main branch is in the project)
  * Pipeline Parameters
    * Click Add Parameters
      * Name: cron_env
      * Type: string
      * Value: (Name of the environment on Pantheon to run cron on defaults to `live`)
      * Click Add Parameters
  * Attribution: Leave it as it is (Scheduling System)
  * Click Save Trigger

**NOTE 1** Configuring the Start time will depend on the need of the project. This is what hour the
cron should be ran. Usually in live it is recommended to run maybe once an hour so all the items would
be checked. But in other environments maybe it only needs to be ran in the morning so only specific times
would be selected. Gauge the need of the project.

**NOTE 2** Configuring the Repeats Per Hour will also dependo n the need of the project. If you aren't doing
something that relies heavily on cron running maybe it's only 1. There may be times where you need the cron
to run every 15 minutes and so setting to 4 is necessary. There are also times where you rely heavily on cron
and there for need it to run every 6 minutes so setting to 12 is required. 12 is the max number we can set this
to which means that we can only run this every 6 minutes.

**NOTE** While this is only configured to run with Pantheon the same sort of concept can
be adapted to run on any other type of job.

```yaml
workflows:
  workflow_name:
    when:
      and:
        - equal: [ scheduled_pipeline, << pipeline.trigger_source >> ]
        - matches: { "pattern": "^(example prefix).*", "value": << pipeline.schedule.name >> }
    jobs:
      ...
```
