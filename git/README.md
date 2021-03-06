Topic
```
Introduction to GIT  
Install Git
GIT basic commands
GIT branching
Working with remote GIT repository
```  

1. Introduction to GIT
    History Tracking  
    Collaborative History Tracking  
        who changed it  
        when they changed it  
        why they changed it  
    Without SCM: How to Control Source Code  
        Update Source Code by Patching [pic]  
        Patching is not working any more   

    Version Control System Types?  
    ![alt text](./images/SCM-taxonomy.png "Version Control :: http://git.mikeward.org/")  

    Centralized Version Control  
    ![alt text](./images/centralized.png "Centralized Version Control :: Pro Git")  

    Distributed Version Control  
    ![alt text](./images/distributed.png "Distributed Version Control :: Pro Git")  

    Delta Based Storage  
    ![alt text](./images/deltas.png "Delta Based Storage :: Pro Git")  

    DAG Based Storage(directed acyclic graph)  
    ![alt text](./images/snapshots.png "Delta Based Storage :: Pro Git")  


    Linux and Source Control Management History: from file and patch to system  

    Linux kernel  
        1,000 Developers  
        Working all across the world  
        Used on millions of computer  
        Used 90% of Supercomputer  
        Run on mobile  

        11 years without version control system[1991 - 2002]  
        2002 - 2005 Bitkeeper  
        2005 - present Git  


    เป้าหมายการออกแบบ Goals!  
    ![alt text](./images/purpose.png "Purpose")  

    ?Git Workflow ที่ ฟิวส์ แปล   

    Who use Git
    ![alt text](./images/companies_and_projects.png "Companies & Project Using git")  

---   

2. Install Git  
    Manual Install[mac, window, linux]  
        download: http://git-scm.com  
    Install via package manager   
    mac
    ```
    brew install git
    ```
    ubuntu
    ```
    apt-get install git
    ```
    Configuration for First-Time Git Setup  
    Your Identity  
    ```
    git config --global user.name "your name"
    git config --global user.email "your email"
    git config -l
    ```
---

3. GIT basic commands  
    Create a repository
    ```bash
    git init
    ```
    Check Status
    ```bash
    git status
    ```
    Add files to Git  
    ```bash
    git add filename
    ```
    Commit your changes
    ```bash
    git commit -m "Message for this change"
    ```
    Remove file from Git
    ```
    git rm filename
    ```

    Example  
    * Create a repository[go to workspace]  
    ```bash
    mkdir git101
    cd git101
    git init
    ```

    * Add files to Git  
     * Create file name README   
     * Check status with git status  

    ```bash
    touch README
    git status
    git add README
    ```
    * Commit your changes
    ```bash
    git commit -m "Add README"
    ```
    * Modify README
    ```bash
    echo "Hello Git" > README
    ```
    * Commit your changes
    ```bash
    git commit -m "Add Hello Git to README"
    ```
    * Add new file to Git  
     * Create file name TMP

    ```bash
    touch TMP
    git add TMP
    ```
    * Commit your changes
    ```bash
    git commit -m "Add TMP"
    ```
    * Remove TMP
    ```bash
    git rm TMP
    git status
    ```

    TIPs
    ```bash
    git help
    git help command
    ```

    Lift cycle of the status of files
    ![alt text](./images/lifecycle.png "The lifecycle of the status of your files")  

---

4. GIT branching
    ![alt text](./images/branch.png "git branch")  

    * Command
    ```bash
    git branch [option] BRANCH_NAME
    git checkout [option] BRANCH_NAME
    git merge BRANCH NAME
    git rebase BRANCH NAME
    ```  

    Example

    * Show all Branches  
    ```bash
    git branch
    ```  
    ![alt text](./images/branch01.png "master branch")  

    * Create new branch  
    ```bash
    git branch dev
    ```      
    ![alt text](./images/branch02-branch-dev.png "master and dev branch")  

    * Switch branch  
    ```bash
    git checkout dev
    ```  
    ![alt text](./images/branch03-checkout-dev.png "switch to dev branch")  

    * Modify and commit on branch  
    ```bash
    echo "On Branch dev" > README
    git commit -am "Modify on dev"
    ```  
    ![alt text](./images/branch04-commit-dev.png "commit on dev branch")  

    * Switch to master branch  
    ```bash
    git checkout master
    ```  
    ![alt text](./images/branch05-checkout-master.png "checkout to master branch")  

    * Merge branch dev to master  
    ```bash
    git merge dev
    ```  
    ![alt text](./images/branch06-merge-dev.png "git branch")  

    * Delete branch  
    ```bash
    git branch -d dev
    ```  
    ![alt text](./images/branch07-delete-dev.png "delete dev branch")  

    * Show all Branches  
    ```bash
    git branch
    ```  
    * Git Merge and Rebase  
    ```bash
    git merge dev
    git rebase dev
    ```
    ![alt text](./images/branch08-git-merge.png "git branch")  
    ![alt text](./images/branch09-git-rebase.png "git branch")  

    TIPs:  
    * Create and Switch branch  
    ```bash
    git checkout -b BRANCH NAME

    equals

    git branch BRANCH NAME
    git checkout BRANCH NAME
    ```
---

5. Working with remote GIT repository[github]
    * Generate ssh key
    ```bash
    ssh-keygen
    pbcopy < ~/.ssh/id_rsa.pub
    ```
    * Add key to github
     * Click your profile photo, then click Settings  
     ![alt text](./images/userbar-account-settings.png "Profile Settings")  

     * Click SSH and GPG keys, In the user settings sidebar  
     ![alt text](./images/settings-sidebar-ssh-keys.png "SSH and GPG keys")  

     * Click New SSH key  
     ![alt text](./images/ssh-add-ssh-key.png "New SSH key")  

     * Paste your key into the "Key" field  
     ![alt text](./images/ssh-key-paste.png "Paste key")  

    * Testing your SSH connection
    ```bash
    ssh -T git@github.com
    ```
    * Add remote repository
    ```bash
    git remote add NAME REMOTE_URL
    ```
    * Remove remote repository
    ```bash
    git remote remove NAME
    ```
    * Rename remote repository
    ```bash
    git remote rename OLD_NAME NEW_NAME
    ```
    * Push changes to remote
    ```bash
    git push NAME BRANCH
    ```
    * Pull changes from remote
    ```bash
    git pull NAME BRANCH

    equals

    git fetch NAME
    git merge BRANCH
    ```

    * New Project  
     * Create New Repository on github name git101  
     ![alt text](./images/repo-create.png "New Repository")  

     * Clone project from remote  
    ```bash
    git clone git@github.com:username/git101.git [NEW_NAME]

    or

    git clone https://github.com/username/git101.git [NEW_NAME]
    ```
    * Existing Project
     * Create a repository
    ```bash
    git init
    ```
     * Create New Repository on github[The same step as Green Field Project]
     * Add remote repository
    ```bash
    git remote add origin git@github.com:username/git101.git [NEW_NAME]

    or

    git remote add origin https://github.com/username/git101.git [NEW_NAME]
    ```
---
Online Tutorial  
https://try.github.io/levels/1/challenges/1  
https://onlywei.github.io/explain-git-with-d3/  
http://learngitbranching.js.org/  
http://git.mikeward.org/  
https://www.slideshare.net/wocommunity/using-git-13552975
