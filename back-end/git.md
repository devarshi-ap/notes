# Git

(Fetch)

_**VCS**_ - a software that tracks & manages changes to files over time.

_**Repo**_ - workspace used to track and manage files (stored on the cloud)

_Git_ vs. _Github_:

* Git ≠ GitHub.
* GitHub makes tools that use Git. It's the largest host of source code in the world.

## Install + Setup

* You can download Git for free from the following website: [https://www.git-scm.com/](https://git-scm.com/)
*   After installing, you can see if it's ready to use by checking it's version:

    ```bash
    $ git --version
    ```
*   Now let Git know who you are (`global` is used to set the username and e-mail for **every repository** on your computer):

    ```bash
    $ git config --global user.name "kanye"
    $ git config --global user.email "kwest@gmail.com"
    ```
*   #### Git Init \[initialize repo, create hidden .git folder]

    ```bash
    $ mkdir app
    $ cd app # git init in the project folder
    $ git init
    ```
*   **Git Status \[info on which changes have/not been staged/tracked]**

    ```bash
    $ git status
    ```

    To see what changes occurred in the staged files:

    ```bash
    $ git status -s
    		?? index.html				# ?? = UNTRACKED
    		A index.html				# A = ADDED TO STAGE AREA
    		M index.html				# M = MODIFIED
    		D index.html				# D = DELETED
    ```

## Git Staging Environment

* Repo Files can be in one of **2 states**:
  1. _**Tracked**_ - files that Git knows about and are added to the repository
  2. _**Untracked**_ - files that are in your working directory, but not added to the repository
* As you are working, you may be adding/editing/removing files. But whenever you hit a milestone, you should add the files to a _**Staging Area**_.
*   **Git Add \[adds a change in the working dir --> staging area]**

    ```bash
    # to add a single file
    $ git add index.html
    # to add all 
    $ git add .
    ```

## Git Commit

* _Staged_ files ready to be **committed** to the project repo.
*   **Git Commit \[commits stages files --> Repo]**

    ```bash
    # add brief descriptions to commits
    $ git commit -m "fix something"

    # (Skipping the Staging Area not generally recommended), but...
    # STAGE (add) + COMMIT (commit) shorthand:
    $ git commit -a -m "fixed index.html with a new line"
    ```
*   **Git Log \[view history of commits for repo]**

    ```bash
    $ git log

    commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)	# commit hash
    Author: w3schools-test 	# global user.name in git config
    Date:   Fri Mar 26 09:35:54 2021 +0100 # timestamp of commit

        Updated index.html with a new line # message
    ```

## Git Branch

* In Git, a `branch` is a new/separate **version** of the main repository
* Branches allow you to work on different parts of a project without impacting the **main** branch.
* When the work is complete, a branch can be **merged** with the **main** branch.
* You can **switch** b/n branches and work on different projects w/o them interfering.
*   **Create Branch**

    ```bash
    $ git branch foobar
    # or, create and switch to it
    $ git checkout -b foobar
    ```
*   **See All Existing Branches**

    ```bash
    $ git branch
    		foobar
    	* master	# * means that we're currently on that branch (HEAD branch)
    ```
*   **Switch To Existing Branch**

    ```bash
    $ git checkout foobar

    # you can pass the commit's hash from 'git log', and go back in time
    $ git checkout 4499f96361e109b99710f534ab514de3ba21e535

    # TRICK: to view the state of the repo 3 commits back:
    $ git checkout HEAD~3
    ```
*   **Delete Branch (note: can't delete branch currently in)**

    ```bash
    $ git branch -d foobar
    ```
*   **Rename Branch (must be in the branch being renamed)**

    ```bash
    $ git checkout OLD-name				# go to OLD-name branch
    $ git branch -m NEW-name			# rename OLD-name branch to NEW-name
    ```
* **HEAD**
  * only 1 branch can be checked out at a time - this is called the _**HEAD**_ branch, or "current" branch.
  * The _**HEAD**_ is the _**most recent**_ version of a branch
  *   You can find out what HEAD you are viewing by opening the _**.git/HEAD**_ file in your repo:

      ```bash
      $ cat .git/HEAD
      ref: refs/heads/main 	# tells us 'main' is the HEAD/current branch
      ```
* **Detached HEAD**
  * A detached HEAD occurs when you check out a commit that is _**not a branch**_
  * The term _**detached HEAD**_ tells you that you are not viewing the _**HEAD**_, the most recent version of a branch, of any repo.
  * An example of entering a **detached HEAD state**, a point in time when you're viewing a commit that's not th emost recent commti (**HEAD**), is using _git checkout_ with a hash of a previous commit in history (from "git log"). This is useful if you want to retrieve code you have overwritten in newer commits. **Detached HEAD state is not an error nor is it a problem**. When you are ready, you can navigate back to the **HEAD** in your repository
  * Once you enter into **detached HEAD state**, you can _view and modify_ the files in a particular commit. This is useful if you want to retrieve a change from a past commit that should be reincorporated into your repo. To save a change from a detached HEAD:
    1. create a **new branch** (_git branch foobar_) - this branch shows repo 3 commits back
    2. **merge** our changes into the main branch (_git checkout main_; _git merge foobar_)
    3. Then, we can create a new Git commit with the changes we've collected from our previous ref HEADs.
  * **To Discard Changes in a Detached HEAD,**
    * You do not need to save the changes you make to a detached HEAD.
    *   Once you are done viewing a previous commit, you can go back to the HEAD of your repository. But first, discard the changes you made:

        ```bash
        $ git reset --hard
        $ git checkout main		# leave detached HEAD state & go back to main
        ```

## Git Branch Merge

* Consider the scenario: We have the emergency-fix ready, and so we want to merge the main and emergency-fix branches.
  1.  First, we need to go to the **main** branch (branch being merged onto)

      ```bash
      $ git checkout main
      ```

1.  Now we merge **emergency-fix** with current **HEAD** (**main**) branch

    ```bash
      $ git merge emergency-fix
    ```

    * Since the emergency-fix branch came directly from main, and no other changes had been made to main while we were working, Git sees this as a continuation of main. So it can "Fast-forward", just pointing both main and emergency-fix to the same commit.
2.  As main and emergency-fix are essentially the same now, we can delete emergency-fix, as it is no longer needed.

    ```bash
      $ git branch -d emergency-fix
    ```

## Git & Github

* Consider the scenario: you have a local project and you want to create a repo for it
  1. Create repo on website
  2.  Copy the https url of the repo

      ![GitHub Push Local](https://www.w3schools.com/git/img\_github\_push\_branch.png)
  3.  use the below command which says that you're adding a _remote_ repo, with the specified _URL_, as an _origin_ to your local Git repo.

      ```bash
      $ git remote add origin <URL>
      ```
  4.  Now, push the **main** branch to the **origin** url, and set it as the _default_ remote branch:

      ```bash
      $ git push -u origin main
      # -u is set upstream (sets as default)
      ```
* #### Pull from Github
  * When working as a team on a project, it is important that everyone has the most recent changes of the project in their local copy.
  * With Git, you can do that with _**git pull**_, which is a _combo of 2 other commands_:
    1. _**fetch**_ - gets all the change history of a tracked branch/repo
    2. _**merge**_ - combines the current branch, with a specified branch
  * _**git pull**_ - used to _pull_ all changes from a remote repo into the branch you are working on.
    *   Consider scenario: you edit the README.md in the repo from the website, and need to get those changes on your local project-folder of the repo. To do this,

        ```bash
        $ git pull origin
        ```
*   #### Push to Github

    ```bash
    $ git add .														# add to staging area
    $ git commit -a -m "Resized image"		# commit
    $ git push														# push to remote github repo
    ```
* #### Pull Branch from Github
  * Consider scenario: you create a new branch in a repo (from Github.com) and now want to see it in your local repo.
    1.  pull any changes on remote repo (including addition/deletion of branches)

        ```bash
        $ git pull
        ```
    2.  Usually to see all branches, you would use _git branch_, but inorder to see all local and remote branches, use the _**-a**_ flag (all). \[If you want to only see remote branches, use the _**-r**_ flag]

        ```bash
        $ git branch -a
        	* master
          	remotes/origin/html-skeleton
        	  remotes/origin/master
        ```
    3.  We see that the branch `html-skeleton` is available remotely, but not on our local git. To pull it to your local:

        ```bash
        $ git checkout html-skeleton			# switch to remote repo
        $ git pull												# pull remote branch
        # check with "git branch"
        ```
* #### Push Branch to Github
  * Consider scenario: you created a new local branch, and want to push that to GitHub.
    1.  create/checkout a branch

        ```bash
        $ git checkout update-readme
        ```

1.  (assume some changes made to readme), stage + commit the readme in the update-readme branch

    ```bash
        $ git add README.md
        $ git commit -m "updated readme"
    ```

    1. Now `push` the `branch` from our local Git repo --> GitHub, where everyone can see

    ```bash
        $ git push origin update-readme		# push update-readme branch to origin
    ```

* #### Forks
  *   A `fork` is a copy of a repository. This is useful when you want to contribute to someone else's project or start your own project based on theirs. (only copies it on GitHub)

      ![GitHub Fork](https://www.w3schools.com/git/img\_github\_fork.png)
* #### Clone
  * Now that we have our own _**fork**_ (only on GitHub), we can also _**clone**_ the forked repo to our local Git to keep working on it.
  *   _**clone**_ - full copy of a repository, including all logging and versions of files.

      1. Move back to the **original** repo, and click the green "Code" button to get the `URL`:

      ![GitHub clone URL](https://www.w3schools.com/git/img\_github\_clone\_url.png)

      1.  In the terminal, clone the repo (downloads the repo as a folder w/ the name of repo-name)

          ```bash
          $ git clone <URL>

          # or specify dir to clone to
          $ git clone <URL> myfolder
          ```
* #### gitignore
  * When sharing your code with others, there are often files or parts of your project, you do not want to share. ie: log files, temporary files, hidden files, personal files
  * Git can specify which files or parts of your project should be ignored by Git using a _**`.gitignore`**_ file
  * Git will not track files and folders specified in _**`.gitignore`**_ (the file itself **IS** still tracked by Git)
    1.  create a _**`.gitignore`**_ file

        ```bash
        $ touch .gitignore
        ```
    2.  Now open the file using VS-Code, and we're just going to add a couple things to skip:

        ```bash
        # ignore ALL .log files
        *.log

        # ignore ALL files in ANY directory named temp
        temp/

        # ignore node_modules folder
        node_modules

        # ignore .env file (has sensitive and private info like api keys)
        .env
        ```
  * [Here's a reference table for the 'rules' to gitignore-ing](https://www.w3schools.com/git/git\_ignore.asp?remote=github)

## Remote

* before you can push anything to Github, you need to establish a _**remote repo**_ on Github- a _destination_.
* In Git, this _destination_ is referred to as a **remote**, and is simply a URL of the hosted repo.
*   **Create Remote**

    * adding: `$ git remote add <remote-name> <URL>`
      * By convention, remote-name is "origin"
      * Copy from Github
    * pushing: `$ git push <remote-name> <branch-name>`

    ```bash
    $ git remote add origin http://github.com/idk/repo.git

    # now, push local folder to main remote branch
    $ git push origin main

    # if you are checkout in a add-styles branch, and want to push it to the remote, which doesn't have a add-styles branch, the below command will create it:
    $ git checkout add-styles
    $ git push origin add-styles
    ```
*   **Show Remotes**

    ```bash
    # to display a list of remotes:
    $ git remote -v
    # (if you haven't added any remotes, you won't see anything)
    ```

***

## CHEAT SHEET

| Git task                                                                                                                                         | Notes                                                                                                                                                                                                                                                                                        | Git commands                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [**Tell Git who you are**](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config)                                           | Configure the author name and email address to be used with your commits.Note that Git [strips some characters](http://stackoverflow.com/questions/26159274/is-it-possible-to-have-a-trailing-period-in-user-name-in-git/26219423#26219423) (for example trailing periods) from `user.name`. | `git config --global user.name "Sam Smith"``git config --global user.email sam@example.com` |
| [**Create a new local repository**](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-init)                                    |                                                                                                                                                                                                                                                                                              | `git init`                                                                                  |
| [**Check out a repository**](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-clone)                                          | Create a working copy of a local repository:                                                                                                                                                                                                                                                 | `git clone /path/to/repository`                                                             |
| For a remote server, use:                                                                                                                        | `git clone username@host:/path/to/repository`                                                                                                                                                                                                                                                |                                                                                             |
| [**Add files**](https://www.atlassian.com/git/tutorials/saving-changes#git-add)                                                                  | Add one or more files to staging (index):                                                                                                                                                                                                                                                    | `git add <filename> git add *`                                                              |
| [**Commit**](https://www.atlassian.com/git/tutorials/saving-changes#git-commit)                                                                  | Commit changes to head (but not yet to the remote repository):                                                                                                                                                                                                                               | `git commit -m "Commit message"`                                                            |
| Commit any files you've added with `git add`, and also commit any files you've changed since then:                                               | `git commit -a`                                                                                                                                                                                                                                                                              |                                                                                             |
| [**Push**](https://www.atlassian.com/git/tutorials/syncing#git-push)                                                                             | Send changes to the master branch of your remote repository:                                                                                                                                                                                                                                 | `git push origin master`                                                                    |
| [**Status**](https://www.atlassian.com/git/tutorials/inspecting-a-repository#git-status)                                                         | List the files you've changed and those you still need to add or commit:                                                                                                                                                                                                                     | `git status`                                                                                |
| [**Connect to a remote repository**](https://www.atlassian.com/git/tutorials/syncing#git-remote)                                                 | If you haven't connected your local repository to a remote server, add the server to be able to push to it:                                                                                                                                                                                  | `git remote add origin <server>`                                                            |
| List all currently configured remote repositories:                                                                                               | `git remote -v`                                                                                                                                                                                                                                                                              |                                                                                             |
| [**Branches**](https://www.atlassian.com/git/tutorials/using-branches)                                                                           | Create a new branch and switch to it:                                                                                                                                                                                                                                                        | `git checkout -b <branchname>`                                                              |
| Switch from one branch to another:                                                                                                               | `git checkout <branchname>`                                                                                                                                                                                                                                                                  |                                                                                             |
| List all the branches in your repo, and also tell you what branch you're currently in:                                                           | `git branch`                                                                                                                                                                                                                                                                                 |                                                                                             |
| Delete the feature branch:                                                                                                                       | `git branch -d <branchname>`                                                                                                                                                                                                                                                                 |                                                                                             |
| Push the branch to your remote repository, so others can use it:                                                                                 | `git push origin <branchname>`                                                                                                                                                                                                                                                               |                                                                                             |
| Push all branches to your remote repository:                                                                                                     | `git push --all origin`                                                                                                                                                                                                                                                                      |                                                                                             |
| Delete a branch on your remote repository:                                                                                                       | `git push origin :<branchname>`                                                                                                                                                                                                                                                              |                                                                                             |
| [**Update from the remote repository**](https://www.atlassian.com/git/tutorials/syncing)                                                         | Fetch and merge changes on the remote server to your working directory:                                                                                                                                                                                                                      | `git pull`                                                                                  |
| To merge a different branch into your active branch:                                                                                             | `git merge <branchname>`                                                                                                                                                                                                                                                                     |                                                                                             |
| View all the merge conflicts:View the conflicts against the base file:Preview changes, before merging:                                           | `git diff``git diff --base <filename>``git diff <sourcebranch> <targetbranch>`                                                                                                                                                                                                               |                                                                                             |
| After you have manually resolved any conflicts, you mark the changed file:                                                                       | `git add <filename>`                                                                                                                                                                                                                                                                         |                                                                                             |
| **Tags**                                                                                                                                         | You can use tagging to mark a significant changeset, such as a release:                                                                                                                                                                                                                      | `git tag 1.0.0 <commitID>`                                                                  |
| CommitId is the leading characters of the changeset ID, up to 10, but must be unique. Get the ID using:                                          | `git log`                                                                                                                                                                                                                                                                                    |                                                                                             |
| Push all tags to remote repository:                                                                                                              | `git push --tags origin`                                                                                                                                                                                                                                                                     |                                                                                             |
| [**Undo local changes**](https://www.atlassian.com/git/tutorials/undoing-changes)                                                                | If you mess up, you can replace the changes in your working tree with the last content in head:Changes already added to the index, as well as new files, will be kept.                                                                                                                       | `git checkout -- <filename>`                                                                |
| Instead, to drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it, do this: | `git fetch origin git reset --hard origin/master`                                                                                                                                                                                                                                            |                                                                                             |
| **Search**                                                                                                                                       | Search the working directory for `foo()`:                                                                                                                                                                                                                                                    | `git grep "foo()"`                                                                          |

***

### Pull Requests

1. Fork the repository you want to pull-req
2. Clone your fork to your computer
3. Create a branch, `git checkout -b temp-branch`
4. PLAYAROUND and save
5. Add/Commit your changes (in temp-branch)
6. Change back to main branch `git checkout temp-branch`
7. Merge your newly created branch into main `git merge main temp-branch`
8. Push your changes (from main)
9. Delete the temporary branch (`git branch -d temp-branch`)
10. Go to your forked repo on GH and open a pull request

***

## Misc

* [steps on how to host website with github pages](https://www.w3schools.com/git/git\_remote\_pages.asp?remote=github)
