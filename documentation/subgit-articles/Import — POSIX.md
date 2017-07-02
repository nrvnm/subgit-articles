---
title: "1. Import - POSIX"
category: chapter
booktype: subgit-articles
weight: 2
---
## SubGit IMPORT

1. Install binaries

    - install Java Runtime environment:
        
        - for MacOS X download an appropriate JavaRE pack from the web site:

            https://java.com/en/download

          double click on the *.dmg file, once mounted open the application and follow installation wizard. 

        - for RedHat family Linux:

              $ sudo yum install java

        - for Debian-based Linux:

              $ sudo apt-get install default-jre

    - install SubGit binary:
    
        - On non-Debian Linux and MacOS X download universal **subgit-3.2.4.zip** binary:

            https://subgit.com/download/subgit-3.2.4.zip
                
            and unzip it:
    
            - for Linux:

                  $ unzip subgit-3.2.4.zip

            - on MacOS X it should be unpacked automatically (if downloaded with Safari), but if it isn't - double-click on the **subgit-3.2.4.zip**.
 
        - on Debian family Linux (Debian/Ubuntu/Mint): download Debian package:

            https://subgit.com/download/subgit_3.2.4_all.deb

            fetch missing dependencies and install:

              $ sudo dpkg -i subgit_3.2.4_all.deb
              $ sudo apt-get install -f
              
2. Configure repository

    - Run this command on behalf of the same user you use to serve Git repository:

           $ subgit-3.2.4/bin/subgit configure --layout auto --trunk trunk SVN_URL GIT_REPO
       
       > **To be added into pop-up cloud (when hovering on SVN_URL and GIT_REPO):**
       > 
       > **SVN_URL** - URL to the SVN project.
       > 
       > **GIT_REPO** - path to new Git repository where data from the SVN project will be imported to.
            
        see command example --> (to be placed in drop-down block):
            
            $ subgit-3.2.4/bin/subgit configure --layout auto --trunk trunk http://example.com/svn/repository/project ./repo.git

            SubGit version 3.2.4 ('Bobique') build #3670

            Configuring writable Git mirror of remote Subversion repository:
                Subversion repository URL : http://example.com/svn/repository/project
                Git repository location   : ./repo.git

            Detecting peg location... 
            Authentication realm: <http://example.com:80> Subversion Repository
            Username [user]: user
            Password [user]:
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
                /home/user/repo.git/subgit/config
            2) Define at least one Subversion credentials in default SubGit passwd file at:
                /home/user/repo.git/subgit/passwd
               OR configure SSH or SSL credentials in the [auth] section of:
                /home/user/repo.git/subgit/config
            3) Optionally, add custom authors mapping to the authors.txt file(s) at:
                /home/user/repo.git/subgit/authors.txt
            4) Run SubGit 'install' command:
                subgit install ./repo.git
  
        For complete `subgit configure` reference see [Import book](https://subgit.com/import-book.html#16)

    - Specify authors mapping

        Update GIT_REPOS/subgit/authors.txt file or change core.authors option to point to global authors mapping

        Find more details about authors mapping in [Import book](https://subgit.com/import-book.html#20)

3. Perform import and start using new Git repository:

    - Import repository by the command:

           $ subgit-3.2.4/bin/subgit import GIT_REPO

       see command example --> (to be placed in drop-down block):

           $ subgit-3.2.4/bin/subgit import ./repo.git
            SubGit version 3.2.4 ('Bobique') build #3670
            Authentication realm: <http://example.com:80> Subversion Repository
            Password for 'user': 

            Translating Subversion revisions to Git commits...

                Subversion revisions translated: 48.
                Total time: 38 seconds.

            IMPORT SUCCESSFUL
        
    - When the command completes, you can clone your new Git repository and start to work with it:

            $ git clone GIT_REPO WORK_TREE
        
        where WORK_TREE - path to your working copy.
        
        see command example --> (to be placed in drop-down block):

            $ git clone file:///home/user/repo.git/ /home/user/repo_working_copy/
                Cloning into '/home/user/repo_working_copy'...
                remote: Counting objects: 99, done.
                remote: Compressing objects: 100% (89/89), done.
                remote: Total 99 (delta 51), reused 0 (delta 0)
                Receiving objects: 100% (99/99), 8.96 KiB | 0 bytes/s, done.
                Resolving deltas: 100% (51/51), done.

Note: no license key required for import!

Would you have any assistance, don't hesitate to contact us at support@subgit.com