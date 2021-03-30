## Chapter 3 Assignment

From this point onwards, you will be managing your assignments with `git` and submitting them through GitHub. The aim of this assignment is to get you familiarized with a common version control workflow.

#### Getting Started
Make sure you've <em>forked</em> this repository under your own GitHub account, and then clone your own repository to your computer. You will push the changes you've made to this document as submission to GitHub.

If the version control concepts or `git` commands are still confusing to you, consider re-reading and following the online notes, or check out an interactive tutorial like [Learn Git Branching](https://learngitbranching.js.org/).

#### The Assignment:
 0. Create a branch in this assignment repository named `submission`, then list all the branches you have (Hint: look at the Branch chapter of notes on how branches work, how to create new ones, and check existing branches):

    ```bash
    #New branch
    git checkout -b submission

    #See all branches
    git branch -a
    #output
    main
    * submission
    remotes/origin/HEAD -> origin/main
    remotes/origin/main
    remotes/origin/revert-3-submission
    remotes/origin/testing
    ```

 1. List the current `remote` name and hyperlink destination of this assignment repository (Hint: if you are not sure, add `--help` after your command to check remotes.).

    ```bash
    #To see hyperlink destination
    git remote show origin

    #output
    * remote origin
      Fetch URL: https://github.com/WCM-datascibasics/version_control_assignment.git
      Push  URL: https://github.com/WCM-datascibasics/version_control_assignment.git
      HEAD branch: main
      Remote branches:
        main                tracked
        revert-3-submission tracked
        testing             tracked
      Local branch configured for 'git pull':
        main merges with remote main
      Local ref configured for 'git push':
        main pushes to main (up to date)

    ```


 2. Add a second remote destination named `upstream` to your assignment repository, `upstream` is a common name used for the repository that people have forked from, in our case, the `upstream` will be at `https://github.com/WCM-datascibasics/version_control_assignment`. List the new list of remotes after you've added the new remote.

    ```bash
    # Command
    git remote add upstream https://github.com/WCM-datascibasics/version_control_assignment.git

    # outputs
    git remote -v
    origin	https://github.com/WCM-datascibasics/version_control_assignment.git (fetch)
origin	https://github.com/WCM-datascibasics/version_control_assignment.git (push)
upstream	https://github.com/WCM-datascibasics/version_control_assignment.git (fetch)
upstream	https://github.com/WCM-datascibasics/version_control_assignment.git (push)
    ```

 3. Save your modifications to this file so far and create a commit indicating you've answered the first 2 questions. Then try pushing the changes to the `upstream` destination on GitHub. What happens? Explain in your own words why does this happen? What are the benefits of having this `upstream` remote added when working collaboratively (Hint: read git command outputs!)?

    > I was denied access, as I am not listed as a collaborator on upstream. Having upstream you are not committing to master, so bugs do not effect working code. The admin can gate what goes into master more easily.


 4. Now clone the repository for the [class website](https://github.com/WCM-datascibasics/wcm-datascibasics.github.io), and in the class website repository:
    - a. Explore the version history by visualizing it as a graph (remember the dog meme?).
        ```bash
        # git cloning command
        git clone https://github.com/WCM-datascibasics/wcm-datascibasics.github.io

        #I dont have visual studio and do not have the space on my machine to add it, so I cannot install git graph.
        ```

    - b. Who was the last person to modify `README.md`? (Hint: use `git log` with an argument)
        ```bash
        # git command
        git log README.md
        # output here
        Author: Xihe Xie <axiezai@gmail.com>
        Date:   Mon Dec 28 16:01:51 2020 -0500

        readme and try new size
        ```

    - c. What was the commit message associated with the last modification to the `-Week 2` line of `index.md` file? (Hint: use `git blame` and `git show`, check out their help pages if you are not sure what to do)
      ```bash
      #Git commit
      git show c122f3c8
      #commit message
      'added ch2 assignment'
      ```

 5. In the course website repository (or another repository you want to clone from GitHub), modify one of its existing files, do not `git add` or `git commit` yet:
     - a. What happens when you do `git stash`, be specific about what happens to your uncommitted changes after `stash`.?
       > The change to the edited file is saved to a working directory and indexed state WIP on the master branch. The are not committed, and they are removed from the tracked changes.
     - b. What do you see when you run `git log --all --oneline` after stashing your modification?
       > you cann see all the changes, and the most recent stash:
  'dc77c99 (refs/stash) WIP on master: 208edcf last lecture'
     - c. Look up what `git stash drop` and `git stash pop` does, either Google or use `--help`. Run `git stash drop` to undo what you did with `stash`, in what scenario might `stash`-ing, `pop`-ing, and `drop`-ing be useful?
       > You have a mixture of changes in your local branch some that you want to keep locally but not commit and some files you want to commit and push to remote. You can stash the changes you dont want to commit, then commit and push the changes you do. After that you can repopulate those un committed stashed changes with git pop  

 6. One common mistake when learning `git` is to commit large files that should not be managed by `git` or adding sensitive information like security keypairs for Amazon Cloud Services. Navigate back to your assignment repository and try adding a random text file to the repository (use `touch`), making some modifications and commits to your repository, and deleting that file with `rm`. But deleting with `rm` will not delete that file's recorded git history, therefore we need to do a little more. You may want to look at [this](https://help.github.com/articles/removing-sensitive-data-from-a-repository/))

```bash
johnferrante@MAC2014748:~/Documents/2021_Spring_Classes/version_control_assignment$ git log --all --oneline
83084aa (HEAD -> submission) deleted random text file
1039d35 Modifying radndom text file
11aceb2 Adding random text file
7575229 Completed Questions 1 & 2
```

 7. Like many command line tools, `git` provides a configuration file (or dotfile) called `~/.gitconfig`. Create an alias in `~/.gitconfig` so that when you run `git graph`, you get the output of `git log --all --graph --decorate --oneline`. You can do this by directly modifying the `~/.gitconfig` file or by using the `git` command line functionality.
    ```bash
    # Your alias entry or git config command here
    git config --global alias.graph log --all --graph --decorate --oneline
    ```
    This is also a good opportunity to turn your dotfiles folder into a version controlled repo (Use `git init` in your dotfiles folder), make it private if you have sensitive `ssh` configurations there (IP Addresses), else feel free to make it public. (This is for your own benefit, not part of the assignment grading)

 8. You can define global ignore patterns in `~/.gitignore_global` after running `git config --global core.excludesfile ~/.gitignore_global`. Do this, and set up your global `gitignore` file to ignore OS-specific or editor-specific temporary files, like `.DS_Store`, or `.vscode`. Feel free to Google around for common gitignore entries for Python projects or other projects of your interest.

    ```bash
    # In .gitexccludes
    .DS_Store
    .vscode

    ```

 9. Push the `submission` branch of your repository to your GitHub remote. Your remote `main`/`master` branch should be unchanged since your fork. Now go to your GitHub repository settings and add `axiezai` as a collaborator. Now create a pull request to merge the changes from `submission` to `main`/`master`, assign your TA `axiezai` as a reviewer. You will receive feedback and grades through the pull request review.
