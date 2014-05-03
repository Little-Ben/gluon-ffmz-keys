#gluon-ffmz-keys

##:unlock:

 # public __fastd__ Keys for Freifunk Mainz

 # please prepend every line in this file with a `#`-sign to stop __fastd__ from importing it as a key.
 
 # (leading spaces are possible to still use markdown)
 
 # [fastd-config-lex](http://git.universe-factory.net/fastd/tree/src/lex.c#n471)
 
##Git

 # Create an passwordless shh-key: `~/.ssh/github_gw_rsa`
 
     # $ ssh-keygen -t rsa -b 4096

 # Add the public key to the __Vollhorst__ [User on GitHub](https://github.com/Vollhorst).
 
 # __Vollhorst__ is in [the _AutoCRON_ Group](https://github.com/orgs/Freifunk-Mainz/teams/autocron), members [are allowed to push](https://github.com/Freifunk-Mainz/gluon-ffmz-keys/settings/collaboration) here.

 # `~/.ssh/config`

    #  Host github_gw
    #    User git
    #    Hostname github.com
    #    PreferredAuthentications publickey
	#    IdentityFile ~/.ssh/github_gw_rsa 
 
 # clone keys
 
    # $ git clone ssh://github_gw/Freifunk-Mainz/gluon-ffmz-keys /etc/fastd/mainzVPN/peers
    
 # crontab
 
    # */20 * * * * $HOME/bin/autoupdate_fastd_keys.sh
 
##Sync

 # `~/bin/autoupdate_fastd_keys.sh`
 
    # #!/bin/bash
    # # Simple script to update fastd peers from git upstream
    # # and only send HUP to fastd when changes happend.
    # 
    # # SET YOUR GATEWAY NAME HERE
    # GW_NAME="awesome gateway"
    # 
    # # CONFIGURE THIS TO YOUR PEER DIRECTORY
    # FASTD_PEERS=/etc/fastd/mainz/peers
    # 
    # function getCurrentVersion() {
    #  # Get hash from latest revision
    #  git log --format=format:%H -1
    # }
    # 
    # function getDate() {
    #  # Get timestamp
    #  date "+%s"
    # }
    # 
    # cd $FASTD_PEERS
    # 
    # # Get current version hash
    # GIT_REVISION=$(getCurrentVersion)
    # 
    # # Automagically commit local changes
    # # This preserves local changes
    # git commit -m "CRON $GW_NAME: auto commit $(getDate)"
    # 
    # # Pull latest changes from upstream
    # git fetch
    # git merge origin/master -m "CRON $GW_NAME: auto merge $(getDate)"
    # 
    # # Get new version hash
    # GIT_NEW_REVISION=$(getCurrentVersion)
    # 
    # if [ $GIT_REVISION != $GIT_NEW_REVISION ]
    # then
    #  # Version has changed we need to update
    #  echo "Reload fastd peers"
    #  kill -HUP $(pidof fastd)
    #  git push -u origin master
    # fi

 # 

    # $ chmod +x `~/bin/autoupdate_fastd_keys.sh`
