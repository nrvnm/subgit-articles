---
title: "1. Mirror - Windows"
category: chapter
booktype: subgit-articles
weight: 6
---
## SubGit mirror in Windows

1.  Install binaries:

    - download an appropriate Java Runtime Environment pack from the web site:

        https://java.com/en/download

        double click on the file and follow installation wizard. 

    - Download **subgit-3.2.4.zip** archive and unzip it:

        https://subgit.com/download/subgit-3.2.4.zip

        right-click on the **subgit-3.2.4.zip** and choose 'Extract all' in the menu.

2. Configure repository

    - Run this command on behalf of the same user you use to serve Git repository:

            > subgit-3.2.4\bin\subgit.bat configure --layout auto --trunk trunk SVN_URL GIT_REPO
       
       > **To be added into pop-up cloud (when hovering on SVN_URL and GIT_REPO):**
       > 
       > **SVN_URL** - URL to the SVN project.
       > 
       > **GIT_REPO** - path to new Git repository where data from the SVN project will be imported to.
       
        ***see command example --> (to be placed in drop-down block):***

            subgit-3.2.4\bin> subgit.bat configure --layout auto --trunk trunk http://example.com/svn/repository/project C:\repo.git
        
            SubGit version 3.2.4 ('Bobique') build #3670

            Configuring writable Git mirror of remote Subversion repository:
                Subversion repository URL : http://example.com/svn/repository/project
                Git repository location   : C:\repo.git

            Detecting peg location...
            Authentication realm: <http://example.com:80> Subversion Repository
            Username [user]: user
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
                C:\repo.git\subgit\config
            2) Define at least one Subversion credentials in default SubGit passwd file at:
                C:\repo.git\subgit\passwd
               OR configure SSH or SSL credentials in the [auth] section of:
                C:\repo.git\subgit\config
            3) Optionally, add custom authors mapping to the authors.txt file(s) at:
                C:\repo.git\subgit\authors.txt
            4) Run SubGit 'install' command:
                subgit install "C:\repo.git"
               

      For complete `subgit configure` reference see [Import book](https://subgit.com/import-book.html#16)

    - Specify authors mapping

        Update GIT_REPOS\subgit\authors.txt file or change core.authors option to point to global authors mapping

        Find more details about authors mapping in [Import book](https://subgit.com/import-book.html#20)
        
    - There are several methods to configure authentication to access SVN server, but we use plain text password file here to simplify the guide. If this method does not fit your needs - find authentication details in [Remote book](https://subgit.com/remote-book.html#15).

      Specify an username and password to be used by SubGit in `subgit/passwd` file. By default, there's the 'subgit secret' credential pair in the file; replace it by 'user password' pair to be used to access SVN server by SubGit.
        

3. Perform SubGit installation and start using new Git repository:

    - Install SubGit into repository by the command:

            subgit-3.2.4\bin> subgit.bat install GIT_REPO
       
       ***see command example --> (to be placed in drop-down block):***

            subgit-3.2.4\bin> subgit.bat install C:\repo.git

            SubGit version 3.2.4 ('Bobique') build #3670

            Translating Subversion revisions to Git commits...

            Subversion revisions translated: 48.
            Total time: 23 seconds.

            INSTALLATION SUCCESSFUL

            Your copy of SubGit is not registered for repository at 'D:\Temp\repo.git'.

            Obtain registration key at http://www.subgit.com/ and register SubGit with 'register' command; registration is free for Open Source, Educational and Startup projects.

            To uninstall SubGit use 'uninstall' command.
        
    - When the command completes, you can clone your new Git repository and start to work with it:

            $ git clone GIT_REPO WORK_TREE
        
      where WORK_TREE - path to your working copy.
    
      ***see command example --> (to be placed in drop-down block):***

          C:\> git clone file:///c/repo.git c:\repo_working_copy
          Cloning into 'C:\repo_working_copy'...
          remote: Counting objects: 99, done.
          remote: Compressing objects: 100% (89/89), done.
          remote: Total 99 (delta 44), reused 0 (delta 0)
          Receiving objects: 100% (99/99), 8.98 KiB | 0 bytes/s, done.
          Resolving deltas: 100% (44/44), done.

4. Try and buy

  > Note: trial period for SubGit mirror is 30 days, after that period you should buy a license key at https://subgit.com/pricing

  Once you receive an email with a license key, upload this license key to your server and run the following command:

          $ sudo subgit.bat register --key subgit.key GIT_REPOS

 ***see command example --> (to be placed in drop-down block):***

    d:\Temp>subgit.bat register --key subgit.key ./repo.git

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