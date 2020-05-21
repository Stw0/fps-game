# Inital Setup
This guide assumes you have already logged in to git CLI

Once forked:
</br >
`git clone https://github.com/Raptor-Compute/fps-game.git`
</br >
`git remote add remote https://github.com/<user>/fps-game.git` 
</br >
Replace remote with something like rriccio, and user with your username

Now create a new branch:,
</br >
`git checkout -b dev`

Go to the webpage for the fork, click on branches, then change default branch
</br >
Switch the default to dev, then delete master

Now, remove the branch from your local:
</br >
`git branch -d <remote>/master`
</br >
`git fetch -p`

To check that it is gone:
</br >
`git branch -r`
</br >
You should not see <remote>/master anymore

Now you can push to your forked branch after a commit by doing:
</br >
`git push -u <remote> dev`
</br >
(or whatever the branch is called)
</br >
This allows pull requests to be created from your fork
</br >
The '-u' tick only needs to be used the first time to set upsteam branch


# To Commit and Push

Once files have been added, if any new files have been created:
</br >
`git add .`
</br >
This will start to track all untracked files

Now, to commit the changes:
</br >
`git commit -a -S -m "<message>"`
</br >
Only use the '-S' tick if you have setup gpg or ssh keys


Now push the changes (assuming you already set upsteam master):
</br >
`git push`


# Switch Local Branch

### DO NOT DO ANYTHING ON ORIGIN
To pull the origin master to your local drive:
</br >
`git checkout master`    (or the name of the branch)
</br >
Now the current branch you are working with is the branch you specified
</br >
Your changes will still be pushed to your upsteam master (your forked repo)


# To Update Branch

To merge from master to your branch:
</br >
`git rebase master`
</br >
(or the name of the branch you want to update from)

For example:
</br >
```text
      A---B---C topic
     /
D---E---F---G master
```

After the rebase would be:
```
              A'--B'--C' topic
             /
D---E---F---G master
```

# Overwrite Commit

To overwrite commit without creating a new one:
</br >
`git commit --amend --no-edit`
</br >
Remove '--no-edit' and '-m "Message"' to change message

Then, when pushing this commit, force it:
</br >
`git push -f`


# Delete Branch

To delete a branch from local:
</br >
`git branch -d local_branch_name`

Then delete from remote
</br >
`git push <remote> --delete remote_branch_name`


# Rename Branch

Rename local
</br>
`git branch -m <old_name> <new_name>`

Delete the old branch on remote - where `<remote>` is, for example, origin
</br>
`git push <remote> --delete <old_name>`

Push the new branch to remote:
</br>
`git push <remote> <new_name>`

Reset the upstream branch for the new_name local branch:
</br>
`git push <remote> -u <new_name>`


# Delete Branch History

Checkout a new branch:
</br>
`git checkout --orphan <new_branch>`

Add all the files:
</br>
`git add -A`

Commit the changes:
</br>
`git commit -am "Initial Commit"`

Delete the branch original branch:
</br>
`git branch -d <old_branch>`

Rename the new branch to old name:
</br>
`git branch -m <old_branch_name>`

Finally, force update your repository:
</br>
`git push -f <remote> <old_branch_name>`


# Check Status

To get info on what's going on locally:
</br >
`git status`


# Hotfix To Origin

To push from one branch to another without pull request (do not do this):
</br>
`git push origin <newer_branch>:<older_branch> -f