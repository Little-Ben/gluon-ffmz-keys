#gluon-ffmz-keys

##:unlock:

 # public __fastd__ Keys for Freifunk Mainz

 # please prepend every line in this file with a `#`-sign to stop __fastd__ from importing it as a key.

 # (leading spaces are possible to still use markdown)

 # [fastd-config-lex](http://git.universe-factory.net/fastd/tree/src/lex.c#n471)

##Git

 # Create an passwordless shh-key: `~/.ssh/github_vollhorst_rsa`

     # $ ssh-keygen -t rsa -b 4096

 # Add the public key to the __Vollhorst__ [User on GitHub](https://github.com/Vollhorst) [ssh keys](https://github.com/settings/ssh), named after your Gateway

 # __Vollhorst__ is in [the _AutoCRON_ Group](https://github.com/orgs/Freifunk-Mainz/teams/autocron), members [are allowed to push](https://github.com/Freifunk-Mainz/gluon-ffmz-keys/settings/collaboration) here.

 # `~/.ssh/config`

    #  Host github_vollhorst
    #    User git
    #    Hostname github.com
    #    PreferredAuthentications publickey
    #    IdentityFile ~/.ssh/github_vollhorst_rsa

 # test key-connection with github

    # $ ssh github_vollhorst
    # Hi Vollhorst! You've successfully authenticated, but GitHub does not provide shell access.
    # Connection to github.com closed.

 # clone keys repository

    # $ git clone ssh://github_vollhorst/Freifunk-Mainz/gluon-ffmz-keys /etc/fastd/mainzVPN/peers

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
    # FASTD_PEERS=/etc/fastd/mainz_meshVPN/peers
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

 # finally

    # $ chmod +x `~/bin/autoupdate_fastd_keys.sh`

 # crontab

    # */20 * * * * $HOME/bin/autoupdate_fastd_keys.sh >> /var/log/fastd/autoupdate_fastd_keys.cron 2>&1

##Usage

 # to __upload__ keys (and therefore sync to the other gateways) from `/etc/fastd/mainzVPN/peers/` just add them:

    # $ git add freifunk-000011112222

 # cron will come around to commit and push them

 # you may still commit and push manually

 # to __delete__ keys (and therefore delete via sync from the other gateways) you have to delete them from git:

    # $ git rm freifunk-000011112222

 # if you just remove them with `rm freifunk-000011112222` they will come back when cron comes around again
