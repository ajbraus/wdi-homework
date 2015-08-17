# How to Collaborate with Github

Github is a powerful tool for versioning and collaborating on code. In this article we will focus on how to collaborate using Github by **creating pull requests** for repos we would like to make changes for. There are two main scenarios for collaborating on coding projects: either you are a collaborator or not. If you are a collaborator on the repo you can clone the project to create pull requests (but be careful you could also push directly to origin/master, which is not recommended). If you are not a collaborator on the repo, you will have to fork the project in order to make a pull request.

## Collaborator Scenario

Imagine you and Jessica, Sally, and John want to build an app together. John bootstraps a rails project and pushes it to Github and adds the other three collaborators. You divvy up tasks and set to work. Your first task is to add user authentication, at the same time Jessica is doing API integration, Sally is writing tests, and John is going to be git master and be putting together a style guide and the splash page.

1. You clone the project John pushed up to Github. This creates a local repository with a `remote` of origin which is the original repo John created and that is technically owned by John.
2. Make a new branch called `auth`
  ```
    $ git checkout -b auth
  ```
3. Now you build the entire auth feature with sign up, login, logout, etc. Now how do you get this up to the project?
4. Switch back to the local/master branch, then pull from origin/master to bring your local master up to date.
  ```
    $ git checkout master
    $ git pull origin master
  ```
5. Now switch back to your local/auth branch and merge local/master into it. This will give you a chance to resolve all conflicts with the most up to date master version before pushing your branch to origin/master.
  ```
    $ git checkout auth
    $ git merge master
  ```
6. Once you have resolved all the conflicts, add and commit your changes locally and push your branch to the remote repo.
  ```
    $ git push origin auth
  ```
7. Now navigate your browser to github to the remote repo's page. Github will detect that you just pushed a new branch and give you a prompt to make that branch into a pull request. Go for it! This will notify all the collaborators that a pull request is waiting to be merged. John will be notified and he can come and merge them.
8. If there were no other pull requests in the queue John can merge your pull request in cleanly with the most up to date master. Otherwise, John might have merged a few pull requests before yours and those pull requests might create merge conflicts with yours. In that case github will notify John that there are merge conflicts and let John pull down your pull request branch and merge them locally to remove all conflicts.

## Fork

Say you want to add some better test coverage to a wonderful and popular starter project for express.

1. First fork the repo. This will create a duplicate remote repo in github under your github account. Now clown this remote repo to your local computer.
2. Now make a new branch called `more-test-coverage`. Add your tests.
3. When you are satisfied push the branch to your origin/master (not the original project).
4. Navigate your browser to the Github page of your remote. Github will recognize that this project is forked from another and ask if you would like to submit the `more-test-coverage` branch to the original project as a pull request. Say "oh yeah!"
5. Whoever owns the repo for the starter express project will now receive an email saying that you submitted a pull request. They will be able to pull down your pull request branch to examine it.


## Code Review

To do merge reviews use Github's "Diff" functionality in the browser.

## Resolving Merge Conflicts Locally

1. Fetch the remote branch: `git fetch <<remote branch name>>`
2. Checkout the new local branch: `git checkout <<branch name>>`
3. Merge master into the local branch: `git merge master`
4. Resolve conflicts.
5. Push the branch to remote: `git push origin <<branch name>>`
6. Now Github will be "happy" and the green button will be there to merge without conflicts.
