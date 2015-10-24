---
layout: default
group: extension-dev-guide
subgroup: 6_Module Development
title: Adding CLI commands
menu_title: Adding CLI commands
menu_order: 14
github_link: extension-dev-guide/code-generation.md

---

##{{page.menu_title}}


<!-- http://olgakopylova.espritica.com/naming-conventions-for-cli-commands-in-magento-2/
 -->

Magento 2 introduces a new command-line interface (CLI) that enables component developers to plug in commands provided by modules. 

As an extension developer, you can now create and distribute your own commands for Magento applications. But as for any implementation, it's also important to follow some general conventions to keep your commands consistent with commands from other developers. Being consistent in this way reduces the user's learning curve.

This topic discusses our recommended conventions.

A command name is a part of the command, which defines behavior of the tool on the very high level. In the command it goes right after the tool's name.
For example, in `bin/magento setup:upgrade`, `bin/magento` is the tool's name and `setup:upgrade` is the name of the command.

If you have a Magento installation handy, enter the following to display the current list of commands:

	php <your Magento install dir>/bin/magento --list

## Command format
Format: `group:[subject:]action`

### group
`group` represents a group of related commands. Commands in a group display in a list, which in turn makes it easier for the user to find the desired command. To find a group name for a command, imagine an subject area where it can be used. The subject area can be any of the following:

*	*Domain* area (for example, `module` for actions with modules, `info` for commands that provide some information)
*	*Workflow* area (for example, `admin` for commands that can be used by an administrator, `dev` for a developer)

### subject
`subject` is a subject for the action. The subject is optional, but it can be useful for defining sets of commands that work with the same object. If a subject is represented by a compound word, use a dash or hyphen character to separate the words.

### action
`action` is an action the command does.

### Examples
	// general commands: just a group and an action
	magento setup:install
	magento module:status

	// set of commands with a subject
	magento setup:config:set
	magento setup:config:delete
	magento setup:db-schema:upgrade
	magento setup:db-data:upgrade

<div class="bs-callout bs-callout-info" id="info">
  <p><code>db-schema</code> and <code>db-data</code> are examples of compound words.</p>
</div>

### Command options and arguments
Options and arguments go after the command name and allow to adjust the behavior of the command.

For example, in `bin/magento module:disable --force Magento_Catalog`, the `--force` *option* and the `Magento_Catalog` *argument* bypass the restrictions and specify a particular module to be disabled; in this case, regardless of dependencies on other modules.

Options and arguments create different user experiences. As a developer, you can choose which type of input is better for your particular case.

## Command arguments

Arguments are values passed by the user in a specified order. The argument name is not visible to the user.

Format: a single word or a compound word separated with a dash or hyphen character

Example:

	magento dev:theme:create frontend vendor themename

where:

`frontend` is a subject area argument

`vendor` is a vendor argument

`bar` is a theme name argument

Use arguments when you need required data from the user. We recommend as few arguments as possible (no more then three) so the user will not confuse their order.

To make it simpler for the user, we recommend the following:

*	Run the CLI multiple times for providing multiple similar values instead of running it once with 20 values
*	Use default values for required arguments where possible. 

	You can then use options instead of arguments to minimize the amount of required data the user must enter.

*	Replace arguments with options: options are named, so the user can provide them in any order. This requires additional data validation (by default, all options are optional).

## Command Options

Options are name-value pairs. The sequence of entered values doesn’t matter.
An option can have a value or no value. An option that does not require a value represents a flag (yes/no).
An option can also have a one-letter shortcut as an alternative to its full name. Enable shortcut for an option if it’s often-used option or it’s easy to determine what the shortcut means. Usually, it makes sense to enable shortcuts for options similar to the ones used in widely-used tools (for example, -f for --force, -v for --verbose, -h for --help).

Format: a single word or a compound word separated with a dash

For example,

magento dev:theme:create --parent=Magento/luma frontend Foo bar
magento dev:theme:create -p=Magento/luma frontend Foo bar
magento dev:theme:create --extend-from=Magento/luma frontend Foo bar
magento module:disable -f Magento_Cms
Where:

--parent is an option, which specifies a parent theme
-p is a shortcut for --parent option
-f is a shortcut for a non-value option --force
frontend, Foo and bar are arguments (see Command Arguments section)
Use options for:

optional data that the user may provide
required data that has default value
Example:

// correct
magento dev:theme:create --extend-from=Magento/luma frontend Foo bar
magento module:disable --force Magento_Catalog
magento module:disable -f Magento_Catalog

//incorrect
magento module:disable --force=1 Magento_Catalog
magento module:disable -f=yes Magento_Catalog
Naming Collisions

We’re still thinking about how to avoid naming collisions between commands from different extension developers and at the same time, how to keep command names simple. There are a few options:

Restricting command names to start with a unique name, such as a vendor name. The usability of the command depends on what you choose for a vendor name. For example, okopylova:dev:theme:create doesn’t look friendly for the end user.
Automatically adding a vendor name only in the case of collision. But it would produce multiple interfaces for the same command. For example, dev:theme:create and okopylova:dev:theme:create. This would require the developer to describe in the documentation two names of the same command. And it would confuse the users.
Allow only one command with the same name to be present in the system and automatically skip all others. It’s even more confusing for the user and it’s also unclear, if the command would be chosen randomly.
Right now I’m thinking about:

Include a vendor name in the command name. And it might not be only at the beginning of the name. In this case it’s possible at least to create commands for an existing group of commands by Symfony grouping. For example, dev:okopylova:theme:create.
Analyze extensions uploaded to Magento Connect (in the future) and display information about commands’ incompatibility with other extensions. You can also add a feature of disabling commands from specific modules by a user, so the user could choose which command to use.
Any other options?

Conclusion

So far we have a modular Magento CLI, so you can already try it and implement your custom commands.

The conventions are being created to define the rules and to make the command names consistent.

And there is still an open question about how to solve naming collisions for commands implemented by different extension developers?

Feel free to leave your feedback, if you have any thoughts about the conventions or the Magento CLI itself. Especially, if you try to implement some custom commands.