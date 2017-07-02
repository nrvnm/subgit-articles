---
title: "1. Mirror - Gitlab"
category: chapter
booktype: subgit-articles
weight: 4
---
## SubGit Mirror to GitLab

1. Configure GitLab server:

    - Log in to GitLab web GUI and create a new project:

        ![Create new project](GitLab_New_project.png)

        Give a name to your project and click **Create project** button. 

        ![New project](GitLab_Created_Project.png)
    
    - Login to the GitLab server (over ssh or to the local console) and install JRE:

        - for CentOS 6/7:

                $ sudo yum install java

        - for Debian and Ubuntu:

                $ sudo apt-get install default-jre
              
        - for OpenSUSE:
        
                $ zypper in java-1_8_0-openjdk

    - install SubGit binary:
    
        - On CentOS and OpenSUSE Linux download universal **subgit-3.2.4.zip** binary:

            https://subgit.com/download/subgit-3.2.4.zip
                
            and unzip it:
            
              $ unzip subgit-3.2.4.zip
                
        - on Debian and Ubuntu download Debian package:

            https://subgit.com/download/subgit_3.2.4_all.deb

            fetch missing dependencies and install:

              $ sudo dpkg -i subgit_3.2.4_all.deb
              $ sudo apt-get install -f


2. Configure the repository:
    
    - Change identity to 'git' user:

            su git

    - Change directory to that one that contains the newly created project. GitLab usually stores its project in

            /var/opt/gitlab/git-data/repositories/<username>

        *username* here is actual GitLab user name that was used during the project creation on step 1.
        Step into that directory:

            $ cd /var/opt/gitlab/git-data/repositories/user

        New GitLab project we have created in step 1 is being stored here in the directory of the same name we named the project:

            $ ls -l
              total 0
              drwxrwx---. 6 git git 131 apr 25 02:06 project.git
              drwxrwx---. 6 git git 131 apr 25 02:06 project.wiki.git
        
    - Run this command to configure SubGit:

            $ subgit-3.2.4/bin/subgit configure --layout auto --trunk trunk SVN_URL GIT_REPO

       > **To be added into pop-up cloud (when hovering on SVN_URL and GIT_REPO):**
       > 
       > **SVN_URL** - URL to the SVN project.
       > 
       > **GIT_REPO** - path to new Git repository where data from the SVN project will be imported to.
            
       ***see command example --> (to be placed in drop-down block):***

            $ subgit-3.2.4/bin/subgit configure --layout auto --trunk trunk http://svn.example.com/svn/repository/project ./project.git

            SubGit version 3.2.4 ('Bobique') build #3670

            Configuring writable Git mirror of remote Subversion repository:
                Subversion repository URL : http://svn.example.com/svn/repository/project
                Git repository location   : ./project.git

            Git repository is served by GitLab, hooks will be installed into 'custom_hooks' directory.

            Detecting peg location...
            Authentication realm: <http://svn.example.com/:80> Subversion Repository
            Username [git]: user
            Password for 'user':
            Peg location detected: r48 project/trunk
            Fetching SVN history... Done.
            Growing trees... Done.
            Project origin detected: r1 project/trunk
            Building branches layouts... Done.
            Combing beards... Done.
            Generating SVN to Git mapping... Done.

            CONFIGURATION SUCCESSFUL

            To complete SubGit installation do the following:

            1) Adjust Subversion to Git branches mapping if necessary:
                /var/opt/gitlab/git-data/repositories/user/project.git/subgit/config
            2) Define at least one Subversion credentials in default SubGit passwd file at:
                /var/opt/gitlab/git-data/repositories/user/project.git/subgit/passwd
               OR configure SSH or SSL credentials in the [auth] section of:
                /var/opt/gitlab/git-data/repositories/user/project.git/subgit/config
            3) Optionally, add custom authors mapping to the authors.txt file(s) at:
                /var/opt/gitlab/git-data/repositories/user/project.git/subgit/authors.txt
            4) Run SubGit 'install' command:
                subgit install ./project.git

    - Specify authors mapping

        Update GIT_REPOS/subgit/authors.txt file or change core.authors option to point to global authors mapping

        Find more details about authors mapping in [Import book](https://subgit.com/import-book.html#20)
        
    - There are several methods to configure authentication to access SVN server, but we use plain text password file here to simplify the guide. If this method does not fit your needs - find authentication details in [Remote book](https://subgit.com/remote-book.html#15).

      Specify an username and password to be used by SubGit in `subgit/passwd` file. By default, there's the 'subgit secret' credential pair in the file; replace it by 'user password' pair to be used to access SVN server by SubGit.
    
    
3. Perform SubGit installation and start using new Git repository:

    - Install SubGit into repository by the command:

           $ subgit-3.2.4/bin/subgit install GIT_REPO
           
        > **To be added into pop-up cloud (when hovering on SVN_URL and GIT_REPO):**
        > 
        > **SVN_URL** - URL to the SVN project.
        > 
        > **GIT_REPO** - path to new Git repository where data from the SVN project will be imported to.

       ***see command example --> (to be placed in drop-down block):***
       
          $ subgit-3.2.4/bin/subgit install ./project.git

          SubGit version 3.2.4 ('Bobique') build #3670

          Translating Subversion revisions to Git commits...

          Subversion revisions translated: 48.
          Total time: 24 seconds.

          INSTALLATION SUCCESSFUL    
       
    - When the command completes, you can clone your new Git repository and start to work with it:
    
          $ git clone GIT_REPO WORK_TREE

        where

        **WORK_TREE** - path to your working copy.

        **GIT_REPO** - GitLab project URL:

        ![GitLab project URL](GitLab_project_URL.png)
          
        ***see command example --> (to be placed in drop-down block):***
    
        - on Windows:
        
                C:\>git clone http://user@example.com/user/project.git ./project.git
                Cloning into './project.git'...
                remote: Counting objects: 99, done.
                remote: Compressing objects: 100% (39/39), done.
                remote: Total 99 (delta 50), reused 99 (delta 50)
                Unpacking objects: 100% (99/99), done.
    
        - on Linux/MacOS X:
    
                $ git clone http://user@example.com/user/project.git ./project.git
                Cloning into './project.git'...
                Password for 'http://user@example.com': 
                remote: Counting objects: 99, done.
                remote: Compressing objects: 100% (39/39), done.
                remote: Total 99 (delta 50), reused 99 (delta 50)
                Unpacking objects: 100% (99/99), done.
              
4. Try and buy

    > Note: trial period for SubGit mirror is 30 days, after that period you should buy a license key at https://subgit.com/pricing

    Once you receive an email with a license key, upload this license key to your server and run the following command:

        $ sudo subgit register --key subgit.key GIT_REPO

     ***see command example --> (to be placed in drop-down block):***

        $ sudo subgit register --key subgit.key /var/opt/gitlab/git-data/repositories/user/project.git

        SubGit version 3.2.4 ('Bobique') build #3670

        Registration information:

            Registered for:       Example company
            Purchase ID:          OS-111111111111111
            Expiration date:      April 23, 2028

            You may use this key to register 9 more repositories (out of 10).

        REGISTRATION SUCCESSFUL

        Thank you for registering SubGit!
        Visit http://www.subgit.com/ in case you have any questions and for more information on SubGit.

Would you have any assistance, don't hesitate to contact us at support@subgit.com