Init script for the open-source cuwo Cube World server
======================================================
A init script that apart from starting and stopping the server correctly also has some extra features for running a Cube World server.

Features
--------

 * Backup for worlds
 * Server complete backup
 * Exclude files and directories from full backup by adding them to "exclude.list"

Requirements
------------
screen, rsync, python

Access server console
=====================

	screen -x cuwo

Exit the console

	Ctrl+A D

Setup
=====

1. Symlink the cuwo file to `/etc/init.d/cuwo`, set the required premissions and update rc.d.

		sudo ln -s ~/cuwo-init/cuwo /etc/init.d/cuwo
		chmod 755  ~/cuwo-init/cuwo
		sudo update-rc.d cuwo defaults

2. Edit the variables in `config.example` to your needs and rename it to `config` (leaving it in the same folder as the original minecraft script)

3. Move your worlds to the folder specified by `WORLDSTORAGE`

4. Edit crontab

	As the server user:

		crontab -e

	Add these lines:

		#m 	h 	dom	mon	dow	command
		02 	05 	*	*	*	/etc/init.d/cuwo backup
		55 	04 	*	*	*	/etc/init.d/cuwo log-roll
		*/30 	* 	*	*	*	/etc/init.d/cuwo to-disk


For more help with the script, run

	/etc/init.d/cuwo help
