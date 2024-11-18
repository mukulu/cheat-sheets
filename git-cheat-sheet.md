# Git cheat sheet
## Using GIT Source Code Management System

### Commands to Browse Git Repository

- `git init`                          # Create git repository
- `git config user.name "Your fullname"`  # Identify you as author
- `git config user.email "e-mail address"`  # Identify your e-mail address
- `git config core.pager less -FRSK`      # Do not display if terminal has few lines
- `git config core.editor vim`          # Use vim as text editor
- `git config color.ui auto`            # Color your CLI to differentiate statements
- `git config merge.tool vimdiff`       # Use vimdiff as merge tool
- `git config -e`                       # Changing configuration settings with editor
- `git add .`                           # Add all to track in directory
- `git rm files`                        # Remove staged files
- `git mv oldfile newfile`              # Rename files 
- `git status`                          # Lists uncommitted changes
- `git commit -a`                       # Commit all changes, commit text
- `git commit -a -m "Some comments"`    # Commit all or only staged items
- `git log`                             # Simple log of commits done
- `git log --n3`                        # Show three last commits
- `git log --stat`                      # Show commits, name of changed files & lines changed
- `git log --summary`                   # Show commits and names of files changed only
- `git log --pretty=oneline`            # Show commits with oneline with commit ID & commit message
- `git log --stat`                      # Show commits with summary of files changed
- `git log --author=authorname`         # Show log of commits done by given author
- `git log --after="MMM DD YYYY"`       # Show log of commits done after e.g. Oct 2 2010
- `git log --before="MMM DD YYYY"`      # Show log of commits done before the date.

- `git whatchanged $filename`           # Show changes by commits affecting the file
- `git whatchanged -p $filename`         # Show changes by commits affecting the file & their diff

- `git diff 1d029..2f9da`                # Diffs between two commits, IDs from git log --pretty=oneline (requires at least 4 ID chars)
- `git diff HEAD^..HEAD`                 # View last commit changes
- `git diff --cached <files>`            # Diffs of staged <files>

### How to Fix Mistakes

- Haven't committed yet but you want to trash them:
  - `git reset --hard`                    # Drops all uncommitted changes in tracked files
- Messed up the commit message?
  - `git commit --amend`                  # Lets you amend commit message of last commit
- Forgot something in your last commit?
  - `git reset --soft HEAD^`              # Uncommit last commit changes for you to make more/less changes

- `nano .gitignore`                      # Create a file to make git ignore some files like *.o, *.pyc etc...

### Branching and Merging

Separate lines of development. Useful for testing developmental features or developing the same feature in more than one way in parallel.

- `git branch feature_x`                 # Create new branch of development
- `git branch`                           # View current branches * shows current branch
- `git branch -a`                        # View all branches in local and remote repositories
- `git branch -r`                        # View all branches in remote repository
- `git checkout feature_x`               # Switches to feature_x from current branch
- `git merge master`                     # Merge current branch with master branch
- `git branch -b $newbranchname $basedbranch`  # Create new branch based on other branch and switch to it.

### Tags

If you've hit a new version, we can tag them:
- `git tag v1.4.2 -m "We are getting somewhere"`  # Add tag to current branch development

### Adding Remote Repositories (for Sharing Source Codes)

- `git remote add remoteRepoNickName remoteRepoURL`  # Adds remoteRepo project as collaborating repo.
  - e.g. `git remote add github git@github.com:mukulu/trialProject`  # Add GitHub trial project as remote repo
  - e.g. `git remote add myRepo /home/mukulu/dev/trialProject`  # Add myRepo as remote repo

### Pushing Codes to Remote Server

- `git push remoteRepoNickName remoteRepoBranchName`  # Sending codes to the remote repository
  - e.g. `git push -u github master`                    # Push codes to GitHub into master branch
  - e.g. `git pull myRepo devBranch`                    # Pull codes from

### Force Pushing Codes to Remote Repository

- `git push -f remoteRepoNickName branchName`          # Force overwriting remote history (not good in shared repository)

### Resetting Remote Repository Back to Old Commit

- `git push origin oldCommitId:master`

### Creating Remote Branch/Pushing Codes to Remote Branch

- `git push remoteRepo branchName`

### Deleting Remote Branch

- `git push remoteRepo :branchName`

### Stashing Changes into Recycle Bin Temporarily for Later Usage

- `git stash`                                   # Drop all uncommitted changes into stash temporarily leaving branch clean, allows switching branches without committing changes
- `git stash apply`                             # Allows you to commit stashed changes in the past
- `git stash list`                              # Lists all stashed operations
- `git stash drop stash@{0}`                    # Drops stashed codes
- `git stash show -p stash@{0} | git apply -R`  # Un-applying stash (retrieving patch and applying in reverse)
- `git stash show -p | git apply -R`             # If no stash is specified, git assumes most recent stash

### Creating an Alias for Command

- `git config --global alias.stash-unapply '!git stash show -p | git apply -R'`

### Discarding Uncommitted Changes to Files

- `git checkout -- filenames`                     # Discard changes you made after current commit

### What Changed Between Commit1 and Commit2

- `git diff $commit1 $commit2`

### Who Changed What and When in a File

- `git blame $filename`                          # Get to see who messed up the file you're coding on. AWESOME!

### Info of Specific File from Specific Commit

- `git show $id:$file`

### Revert a New Commit

- `git revert`

### History of Files with Diffs

- `git log -p $file $dir/ec/tory`

### Fetching Latest Changes from Remote

- `git fetch origin master`                      # Fetching changes without merging
- `git pull origin master`                       # Fetching changes and merging
- `git am -3 patch.mbox`                        # Applying patch someone sends you
- `git am --resolved`                            # Resolve conflicts in patch
- `git format-patch origin`                      # Prepare a patch for other developers

### Checking Errors and Cleaning Repository

- `git fsck`
- `git gc --prune`

## Advanced Git Commands

### Counting Commits Per User

- `git shortlog -s -n`                          # In short, only users and total commits
- `git shortlog -n`                             # In detail users, and each commit message

### Establishing ssh connection with github
Initialize a ssh-key on your local repository, i.e. ```~/.ssh/id_rsa.pub``` with its equivalent private key.
Copy the contents of the **id_rsa.pub** to the githbub SSH Keys settings.

#### Test the connection
```
ssh -T git@github.com
```

If problem arises make sure the .ssh folder is properly configured with correct permissions.
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

Configure ssh configurations to use the right keys for github.

Open (or create) ~/.ssh/config and add the following:
```plaintext
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa
```

