# WordPress Perils and Countermeasures

WordPress is the most widely used Content Management System CMS on the today. It was never build with "security" or "privacy" as a required priority.
Using this application without taking "major" countermeasures to over its innate flaws would be ludicrous.

## Pressing Issue # 1: Insecure FTP (File Transfer Protocol)

The WordPress application manages udates and customization via FTP. This file tranfer protocol is 100% insecure! 

You have the typical catch 22: You need to update frequently because the software is full of holes. Then you use a risky protocol for those updates.

### Countermeasure: Do not use these applications and protocols based on them: FTP or ProFTP. 

![FTP](https://github.com/gitezri/Secure-WordPress/blob/master/Setting-up-an-FTP-Client.png  "FTP")

To mitigate this, use programs like SFTP or vsFTP (Secure-FTP or Very Secure FTP)

![SFTP Information](https://kb.iu.edu/d/akqg  "SFTP")

Alternatively, you can use SCP, WinSCP.

SFTP is a Linux secure file transfer utility.
It practically can't be setup with 2FA key-file for web file transfer.
You have to only rely on entropy passwords, which is good enough.
Note: SFTP is a subsystem of SSH or OpenSSH and constitutes your secure FTP server.

	service sshd start 
	
then you can connect with
	
	sftp userx@x.x.x.x (and provide you entropy password)
	
The best solution for FTP problem is to use the [WP CLI](https://developer.wordpress.org/cli/commands/)  (WordPress Command Line Interface). It focuses all transfers via the security of your hosts' operating system. You achieve "total security" via Operating System's SSH (Secure Shell).

### The WP Command Line Interface

See this site [WP CLI](https://kinsta.com/blog/wp-cli/#getting-wp-cli) 

Alternatively also here [More Examples](https://kinsta.com/knowledgebase/manually-update-wordpress-plugin/) 

	# Download WordPress core
	$ wp core download --locale=nl_NL
	Downloading WordPress 4.5.2 (nl_NL)...
	md5 hash verified: c5366d05b521831dd0b29dfc386e56a5
	Success: WordPress downloaded.
	
	# Install WordPress 
	$ wp core install --url=example.com --title=Example --admin_user=supervisor --admin_password=strongpassword --admin_email=info@example.com
	Success: WordPress installed successfully.
	
	# Display the WordPress version
	$ wp core version
	4.5.2

****Remember, all these commands are being ran via a super encrypted SSH tunnel.


## Pressing Issue # 2: WordPress

Using WordPress and all of its plugins and buggy themes.

Known Security Issues Counts (August 2020)

|Software  |Issues  |
|--|--|
|FTP  |1088  |
|ProFTP  |45  |
|WordPress  |1222  |
|SFTP  |35  |

### Installing and Upgrading WordPress

 [See this site: Wordpress.org](https://wordpress.org/support/article/upgrading-wordpress-extended-instructions/) 

To mitigate this issue you have to "security baseline" the app and don't deploy your app until all major flaws are patched or mitigated.

I wrote an article on web applications security baselining on github.com: [Web Application Security Baselining](https://github.com/gitezri/owasp-zap-base/blob/master/README.md)

## Pressing Issue #3: Configuration Hard-Coded Passwords

Your are responsible to remove any Hard-coded user IDs and passwords.

