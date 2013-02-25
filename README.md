Deploy Script
===================

The deploy script is a tool to easily deploy updates for your web base software.
It's goal is is to grab the new code from versioning system en safly deploy it to a (live) environment.
functions include things like:

- Databse backup.
- File backup
- Send notifications
- hot swap to new code base. 


Available subcommands are:
----

  		-c <name>			Alias for --config.
  		-t <tag #>			Alias for --tag.
  		-b <branch>			Alias for --branch.
  		-d					Alias for --debug.
  		-q					Alias for --quiet.
  		--config <name>		Will set file deploy.<name>.conf.php. default file: deploy.conf.php.
  		--tag <tag #>		Tag to be deployed.
  		--branch <branch>	Branch to be deployed.
  		--debug				Debug modes: default = false.
  		--quiet				Quiet modes, only output warning and exception, only if debug is not given: default = false.
  		--version			Shows version information of Oink.

Installation
----
- Grab project from GIT
- Copy the example file for your project from sources/.. to the root of the project.
- Fill in the configuration where still blank


###Installation Concrete 5
Log into the server and grab a copy of the script.
	
	$ clone git://github.com/nedstars/Deploy-Script.git
	
Copy the example file for each enviroment that your need, for example "staging" or "live", from sources/.. to the root of the project.
When executing ./deploy the -c or --config argument is used to specify which config should be loaded.
When none given de default is deploy.conf.xml
	
	$ cp sources/example.concrete5.conf.xml <config_name>.conf.xml
	
Fill in the <config_name>.conf.xml file where still blank.

- Database connection data or use local.xml loader.
- Git repo, deploy script uses git --archive to get the source code from the repo for your deployment
- Notifications, configure how to notify peopele when deployemnt is done. 
- Paths, there are 4 folders that need to be configured
	- live path, path to project folder (the one that will be updated)
	- temp new path, this is the folder where the new source will be build up.
	- temp old path, when switching to the new source the old source is copied to this folder
	- backup path, folder where all backups will be played
	
Execute example
	
	$ ./deploy -c <config> -t <tag number> 
	
Notifications
----
There are three types of notification services:

- email
- Pushover https://pushover.net/

The XML looks like

	<notifications>
		<email_addresses>
			<address>example@example.com</address>
		</email_addresses>
		<pushover_users>
			<user>183SSd882exampleS82</user>
		</pushover_users>
	</notifications>

