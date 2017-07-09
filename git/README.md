Topic
```
Introduction to GIT  
Install Git
GIT basic commmands
GIT branching
Working with remote GIT repository
```

1. Introduction to GIT   
    Version Control?  
    Centralized Version Control  
    Distributed Version Control  

    เป้าหมายการออกแบบ  
        Speed
        Simple Design
        Support for Many Parallel Branches
        Fully Distributed
        To Handle Large Project Like Linux Kernel

        ?Git Workflow ที่ ฟิวส์ แปล   

    Who use Git
```
โลโก้
```

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
    Configuration Git on Local Machine
    ```
    git config --global user.name "your name"
    git config --global user.email "your email"
    git config -l
    ```

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

    Lift cycle of the status of files
    ![alt text](https://git-scm.com/book/en/v2/images/lifecycle.png "The lifecycle of the status of your files")

4. GIT branching
5. Working with remote GIT repository
