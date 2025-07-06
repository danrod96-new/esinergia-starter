# Developer Instructions.

## Step #1: DDEV environment setup

If you don't have DDEV set up, complete this step.

**This is a one time setup.**

Follow [DDEV install instructions](https://ddev.readthedocs.io/en/stable/)

## Step #2: Project setup

1. Clone this repo into your Projects directory.
1. Change directory to the cloned folder.
1. Don't forget to add your Pantheon Terminus token globally, you can that by running `ddev config global --web-environment-add="TERMINUS_MACHINE_TOKEN=abcdeyourtoken"`
1. Restart the project by running `ddev restart` and you can start developing after that point.

## Installing Modules

Modules are installed using composer.
The process for installing a module would be the following:

```
ddev composer require [organization]/[package]
```

The standard composer command is used but with the DDEV specific command 
`ddev` prepended to the beginning.
