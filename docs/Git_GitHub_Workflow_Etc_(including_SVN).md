Git, GitHub, Workflow, Etc. (including SVN)
-------------------------------------------

### SVN

**I would prefer you to use git** as it is more industry-standard for software and game development, however, SVN is access also available. If you still prefer to use SVN and do not have it installed follow the steps on [https://tortoisesvn.net](https://tortoisesvn.net/)\
* **Fair warning**, pushing to `master` is still disabled for SVN. Branching, or more specifically merging, in SVN was horrible the last time I tried - so I never tried again. I have no clue if it is any better now, as that was probably around 5 years ago.

### [GitHub Student Developer Pack](https://github.blog/2020-01-16-the-github-student-developer-pack-delivers-200k-worth-of-tools-and-training-to-every-student/)

-   Free stuff (tools and other helpful resources).

### GUI vs command line

This is up to you. You can use whatever git client you want. I prefer to use the command-line from Git-Bash. If you do not have git installed on your computer, follow the steps on [https://git-scm.com](https://git-scm.com/). I will give some examples and provide [links](https://distance.digipen.edu/2020-spring/mod/resource/view.php?id=47908 "links") to the documentation for the command-line tool only; the GUIs have their docs you should use if you choose to use one. They do have some advantages.

Some popular GUIs that I have used, but I am not advocating for:

-   [GitHub Desktop](https://desktop.github.com/)
-   [GitKraken](https://www.gitkraken.com/)
-   [SourceTree](https://www.sourcetreeapp.com/)

### Using Git

-   [https://git-scm.com](https://git-scm.com/)
-   <https://git-scm.com/docs/gittutorial>
-   <https://www.atlassian.com/git/tutorials>

### Using GitHub

-   [https://guides.github.com](https://guides.github.com/)
-   [https://guides.github.com/activities/hello-world](https://guides.github.com/activities/hello-world/)

### Git Workflow

-   <https://www.atlassian.com/git/tutorials/comparing-workflows>
-   <https://guides.github.com/introduction/flow/>
-   <https://www.atlassian.com/git/tutorials/comparing-workflows>

-   For our class and ease of use we will use the `master` branch for submission; better practices are described in the workflow [links](https://distance.digipen.edu/2020-spring/mod/resource/view.php?id=47908 "links") above. At a minimum, if you want to use these practices in your group projects, you should at least do the following (a very simple workflow example):

- Create a `dev` branch off `master`, then feature branches off `dev`.
- Upon feature branch PR approvals, the feature branches will merge back to `dev`.
    - The developer working on the feature branch is responsible for making sure their branch is up-to-date with the branch they are merging into.
- When you are ready for a release (milestone, final submission, etc.), cut a release branch off `dev` name `release/<milestone-name>`.
- At this point, no additional features should be merged into the release branch.
    - This branch should go through extensive testing (play- and developer testing).
    - `bug-fix/<bug-description>` branches should be cut off of the branch testing for release.
    - Take care when selecting a branch to merge the bug fix back into. You could choose directly back to the release branch, or better, back to `dev` and then merge changes forward into the release branch; it will just depend on the current situation and timing.
    - After release, you can merge the release branch back to `master` and then to `develop` or cut a new `develop` branch from `master` (force pushed over the top of the previous).
- This is not a perfect workflow, but it is better than everyone force pushing to master (the typical practice with SVN, or just an uninformed approach to git).

* * * * *

### Clone your repository - [git-clone](https://git-scm.com/docs/git-clone)

On your computer, navigate to your working directory, right-click, and select "Open Git Bash here" and then run the following command.

> `git clone https://github.com/DigiPen-CS315/assignment-1-[your-github-username].git`

- This clones the `master` branch by default.
    - Do **not** work on `master` (pushing your changes to `master` will be disabled). `Master` is reserved for stable, production code. Ideally, the build on this branch should never be broken.

* * * * *

### Configure git - [git-config](https://git-scm.com/docs/git-config)

#### View the git config variables

> `git config --list` to see all variables\
> `git config --global --list` to see global variables only\
> `git config --local --list` to see local variables only

#### Set the public email that will be displayed on your commit (we're using private repositories, but its good practice)

See <https://help.github.com/en/github/using-git/setting-your-username-in-git> for more information.
- Set your email to the automatic "fake" email that GitHub creates for each user. <_your-GitHub-username_>@users.noreply.github.com. To do this run the following command. This will have to be done on **every** computer you dev from. You will have to do this the first time you use git on a new computer.

> `git config --global user.email "<_your-GitHub-username_>@users.noreply.github.com"`

example with my username:

> `git config --global user.email ryancdavison@users.noreply.github.com`

* * * * *

### Feature / Development Branches - [git-branch](https://git-scm.com/docs/git-branch)

Projects and assignments will use `feature`, `bug-fix`, and `master` branches. However, projects will typically also include a "develop" branch as an intermediary step between feature branches and `master`. Working on the `master`, or the default branch if it is named differently, is generally bad practice. So we will create local branches to develop new features. They are easy to re-branch from and able to develop multiple solutions in parallel if needed.

See the documentation for whichever git client you are using to create a new branch, follow any of the above tutorials, or view
- Bitbucket's [Branching a Repository](https://confluence.atlassian.com/bitbucket/branching-a-repository-223217999.html)
- git-scm [Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

#### Create and check out a feature branch

Create a new branch `dev` from `master` (`development`, `develop`, or any other descriptive name) I will use "dev" in the examples.
> `git checkout -b dev`
- `git checkout` is the command to switch branches,
- `-b` flag tells git to create a new branch named "dev"
- This will create and check out the new `dev` branch in one step.
- Branches can also be created on GitHub in the "Code" tab by selecting the "Branch:" button and typing in a new branch name.
    - You can manage all of your branches in the "branches" section on your GitHub repository page.
- You can follow better branch naming conventions if you wish i.e. `[topic]/[feature-name]/[work-description]`

#### Branch Naming

The branch name should be simple but reflect the feature that is being developed and '/' should be used for branch grouping
> `<_topic_>/<_feature-name_>/<_work-item-description_>`
- **Feature Name** should be generic enough to be reused
- **Area Name** should be generic enough to be reused and reference where the work is being done
- **Work Item Description** should be a brief but detailed description of the actual feature or work item  
    - "initial/scaffolding-project-separation-based-on-concerns"
    - "bugfix/bug-description"
    - "crash-handler/adding-seh"
  
Other examples:
> `<_username_>/<_feature-name_>`
>
> `<_username_>/userstory-<_some-bug/task/feature-id-number_>`
>
> `bugfixes/<_bug-name_>`
>
> `<miletsone>/<_feature-name_>`


* * * * *

### View your changes - [git-status](https://git-scm.com/docs/git-status)

This will show the current status of your working tree (which files have changed). Verify that you are working on your feature branch and not on `master`.
> `git status`

* * * * *

### Stash your changes - [git-stash](https://git-scm.com/docs/git-stash)

If you missed the "Verify that you are working on your feature branch and not on `master`." note and worked on `master` anyway, you can "stash" your **uncommitted** changes, create and/or check out a feature branch, then reapply the changes.
> `git stash` or `git stash push` (these are equivalent) will push your changes outside of this branch, onto a stack\
> `git stash apply` will apply the last stash that was pushed (pops off the top of the stack)\
> `git stash list` will list all of the stashes that exist

If you committed changes locally, you should follow the *rebase* instructions to apply those changes to the preferred branch.

* * * * *

### Stage your changes - [git-add](https://git-scm.com/docs/git-add) and [git-rm](https://git-scm.com/docs/git-rm)

We have to stage our changes per file. To do this we will use the "add" and "rm" commands to add or remove files, respectively.\
Before staging changes, verify that you are working on your feature branch and not on `master`.

Many people will use the "add/stage all changes" command.
> `git add .`

However, this can also cause you headaches by adding files you do not intend to track. Prefer to add the changes individually
> `git add <./local/path/to/file>`

Or, you can add by folder, but again someday this may cause unintended behavior.
> `git add <src/*>`

See [git-rm](https://git-scm.com/docs/git-rm) for more information on removing files from the working tree

* * * * *

### Commit your changes - [git-commit](https://git-scm.com/docs/git-commit)

**Commit code locally often.** We will create a local commit saving the state of our development changes. Verify that you are working on your feature branch and not on `master`. The number of commits in development does not matter. To start, more is usually better. You can create multiple local commits before proceeding to the next step. Again, to start, it is preferred to make local commits often, whenever you complete a single unit-of-work (stage of development), etc. We will "squash" these later anyway.

#### Commit Message
- Use the "-m [commit comment]" flag to prefix your commit message. The message should go inside double-quotes.
- Write a brief but detailed description of what you edited as the commit message.
- Developer notes are fine.
- Commit messages are displayed in history and can be useful when looking up work done in history.
> `git commit -m "<Type a brief but descriptive message of your changes>"`

* * * * *

### Changing Branches - [git-checkout](https://git-scm.com/docs/git-checkout)

As long as your work is saved and committed locally, you can comfortably switch between branches using "git checkout"
- Note the "-b" flag in the initial checkout told git to create a new branch. We do not need that here. > `git checkout master` will switch back to the master branch
> `git checkout <your-feature-branch-name>` will bring us back to our feature branch

git will stop you if you have uncommitted changes. Commit or stash your changes before switching branches.

* * * * *

### Pulling Changes (Code Integration) - [git-pull](https://git-scm.com/docs/git-pull)

If you are working in a repository that already exists on your computer and you need to update to get changes from the server we will use the "pull" command. Otherwise, you will follow the `git clone` example to check out your repository. It is a good idea to pull before trying to push. If there are changes on the server that your local repository does not have, the push will fail.
- Note that this command only gets the changes for the currently selected branch. Check out the branch you wish to pull changes for. > `git pull`

* * * * *

### Pushing Changes - [git-push](https://git-scm.com/docs/git-push)

**Push code regularly,** upon feature completion or at major markers with feature development, and possibly at end-of-day or when needed to back up.
- **Note**: This will fail if you are still working on the `master` branch.

The first time you push after creating a new branch, you must tell git what branch to target on the server, or "set the remote as upstream". If you try to run only the `git push` command you should see an error and it will/should tell you to run this
> `git push --set-upstream origin <your-feature-branch-name>` (or whatever feature branch name you used)

From then on, you can use only the push command, which will push the changes of the currently selected branch.
> `git push`

**Note**: If the push fails because of the email settings that I referenced in the GitHub setup process we need to do two things:

- Set your email to the automatic "fake" email that GitHub creates for each user. <_your-GitHub-username_>@users.noreply.github.com. To do this run the following command. This will have to be done on **every** computer you dev from.
> `git config --global user.email "<_your-GitHub-username_>@users.noreply.github.com"`

Note: The "user.email" string should say exactly that, do not change that value. This tells git what configuration entry to edit.
- Reset the author value of our local, recent commits to this branch.
> `git commit --amend --reset-author`
- Note: git will ask you to enter a "merge comment" and to verify the changes.
    - Some of your git configurations will pop open text editors.
        - Edit the file if you need to - usually you will not have to change anything.
        - Then save and close the file in the editor to tell git to continue.
    - Other git configurations, that are not configured to use the text editor, will open the "file" using "VIM". "VI" or "VIM" can be confusing if it is your first time using it. VIM has several modes, it usually starts in a navigation mode called "normal" mode. Here text cannot be entered as most of us are used to. So we have to change to the "Command-Line" mode.
        - Type the `:` symbol (`Shift` + `;`).
            - Now you should see the cursor at the bottom of the console window. This is the "command-line" mode.
        - Type `x` or `wq`, then `Enter` to save the file and exit VIM.
            - This will tell git to proceed with the changes.
        - In most VIM documentation you will see this as one command `:x` or `:wq` to save and quit.
        - See the VIM section at the bottom of this document for more information.

* * * * *

### Continuous Integration & Testing

We are using [**GitHub Actions**](https://help.github.com/en/actions) to implement integration testing. The tests are mostly the same ones that you will have locally and will run using the [Catch2 Testing Framework](https://github.com/catchorg/Catch2). These tests will run every time you push to the server, regardless of the branch. They will also run every time there is a pull request to `master`. We will use settings to disable merging pull requests to `master` unless all (required) tests pass.

See other GitHub Actions:
- <https://github.com/marketplace?type=actions>

For more information on Catch2:
- [tutorial](https://github.com/catchorg/Catch2/blob/master/docs/tutorial.md#top)
- [readme](https://github.com/catchorg/Catch2/blob/master/docs/Readme.md#top)
- [docs](https://github.com/catchorg/Catch2/tree/master/docs)

To view the test results, go to your assignment repository on GitHub, and click on the **Actions** tab. This will display all of the tests that are run. For now, we are using build tests with gcc, clang, and msvc, in debug and release, and are running unit tests on the gcc and msvc projects.

You can view the tests in the .github/workflows/ folder. For now, do not edit these files, unless you REALLY know what you are doing. If you do know what you are doing with GitHub Actions, feel free to submit a PR back to the assignment template, and share them in the forum on moodle - shared workflow files must not contain any source directly relevant to the actual project or assignment implementation.

* * * * *

### Merging Code - [git-rebase](https://git-scm.com/docs/git-rebase) and [git-merge](https://git-scm.com/docs/git-merge)

#### Rebase vs Merge

Used whichever is correct for the situation. See [Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) for details.
- Just remember, merge preserves history whereas rebase rewrites it.

#### Merging Feature or Development Branches
- Merging dev branches does not require a Pull Request, just be aware of who else it might affect if they are also working from that branch.
- Prefer an "interactive rebase" over non-interactive
    - Standard Rebase vs Interactive Rebase
        - A rebase in standard mode will blindly take the commits in your current working branch and apply them to the head of the passed branch.
- **Rebase**
> `git rebase -i <branch-name-to-rebase-onto>`
- **Merge**
> `git merge <branch-name-to-merge-into-current>`
- The common usage here will be if you need to update your current feature branch with the changes that exist in `master`. For example:

    > `git checkout master` (switch from your feature branch back to `master`)\
    > `git pull` (update `master` from the server)\
    > `git checkout <feature-branch>` (switch back to your feature branch)\
    > `git rebase -i master` or `git merge master` (apply the changes from `master` into your branch)

* * * * *

### Resolving Merge Conflicts

Conflicts will happen, especially when working in teams. I prefer to use the Visual Studio Code editor and use the "Open Folder" feature to display the entire git repository. VS Code will highlight conflicts in the left-hand explorer window (marked with by a 'C' next to the file name). Open the file, scroll to the conflict and accept the current change (local), incoming change (from the server), or edit the code manually to resolve the conflict. Save and continue.\
See the following for additional help:
- [Resolving a merge conflict using the command line](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line)
- [Addressing merge conflicts](https://help.github.com/en/articles/addressing-merge-conflicts)
- [Git merge conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts)

**Note**: If you find yourself digging a hole, stop; **Do NOT push!**; ask for help and we can back out locally to resolve the issue.

* * * * *

### Merging Feature Branches Into Master

#### Requirements
- The code must be in a separate branch. Pushing directly to `master` is disabled.
- The branch should be up to date with `master`, by either rebase or merge.
  - This is good practice, but unless you have worked in multiple branches, you should  not need to do this for our assignments.
- Tests should be written to cover all of the new behavior
- All tests should pass
- The CI/CD pipeline tests should pass

* * * * *

#### Create a Pull Request (PR)

Pull Requests are how we request code to be merged into `master` (or other restricted branches). Once you are finished with the implementation and are ready to submit, you will create a Pull Request. The changes will be reviewed, tested, and verified before the merge is allowed. This may seem slow, however, it will catch many bugs and less than optimal code changes before affecting the actual build.

See [About Pull Request Reviews](https://help.github.com/en/articles/about-pull-request-reviews) and [Configuring Pull Request Merges](https://help.github.com/en/articles/configuring-pull-request-merges)
- Go to the GitHub repository Pull Request page and click "New Pull Request"
- Select the branch you are merging into master
- Review your changes in the tabs below and click "Create pull request"
- Click "Create pull request"

In the following page:
- Verify the correctness of the branches you are merging.
- Add a detailed description of the feature or work item that was completed and is being merged in.
    - This is the comment we will see when looking back in history; especially with "Squash and Merge" where your commit comments will be replaced.
    - Your commit/development comments should **not** be copy-pasted here.
- Select at least one reviewer to approve the pull request. For this class, select me.
  -   PRs cannot be merged unless they pass review.
- Click the "Create pull request" button to finalize the request.
- This will now trigger automated tests on the server against your code.
  -   All tests must pass before your PR is accepted.
- I will get a notification of the request and will review it as soon as I am able.

* * * * *

#### Making Pull Request Changes
When reviewing PRs, the reviewer can suggest changes, give feedback, approve, or deny the request; as well as a few other options.\
If required changes are suggested, update your code and push the changes to the branch in PR. This will automatically apply the changes to the PR, there is no need to close and re-open a new one; in fact, this would be incorrect.

* * * * *

#### Completing the Merge
- Navigate back to your Pull Request page (from the Pull Requests tab in GitHub).
- After the review approval, verify the comments and update the public description.
- Select "Squash and Merge".
  - Squash is preferred, not required; but it allows the collapsing of multiple  development commits, and provides a new description over the development commit  comments along the way.
  - Add a new merge/commit message. It should be detailed and reflect the work that  was done (not how many commits it took).
- Delete your feature branch. It's OK, you are done with it!
- This helps keep the history clean and removes the possibility of outdated branches being merged.

* * * * *

Updating Your Local Repository After the PR Merge
After merging the PR, you will want to switch back to your git bash terminal.

- checkout the master branch
- `git checkout master` 
- Update `master` with the changes from the server.
- `git pull` 
- Delete the local `dev` branch.
- `git branch -d dev` 
- If you need to make more changes, it is best practice to 
    - create another feature branch again- commit to it
    - push the changes/update
    - create a new PR
    - merge, and repeat these steps.

* * * * *

### Reviewing Pull Requests

Instructors or TAs will complete the review for PRs for submission. You will not complete the PRs for your own or other students' code. For more information on using this elsewhere, see [Reviewing Changes In Pull Requests](https://help.github.com/en/articles/reviewing-changes-in-pull-requests).
- Save and commit your current changes.
- Check out the merging feature branch, and pull so the branch is up to date.
- Run the updated code and verify that all tests pass.
- Make any comments or edits in-line on the pull request page (on GitHub).
- Approve or deny the review; with detailed comments as to why.
- Do **NOT** "Squash and Merge" or delete someone else's branch. It is their responsibility.

* * * * *

[GitHub Actions](https://github.com/features/actions) - Build Server and Build Tests
------------------------------------------------------------------------------------

The server build tests will run via [GitHub Actions](https://github.com/features/actions). Some basic actions will be provided that will run tests.
- Do not change the tests that are already there, but feel free to write additional Actions if you want.

* * * * *

Ignoring Files
--------------

The `.gitignore` file can be used to ignore files from your repository. It is already setup for most cases, but you can edit it as necessary. See the following for more information.
- [Ignoring Files - GitHub](https://help.github.com/en/github/using-git/ignoring-files)
- [Ignoring Files - Atlassian](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)

* * * * *

VIM
---

From the [wiki](https://en.wikipedia.org/wiki/Vim_(text_editor)): Vim (a contraction of Vi IMproved) is a clone, with additions, of [the] "vi" text editor program for Unix.

### Cheat Sheets:
- <https://devhints.io/vim>
- [https://vimsheet.com](https://vimsheet.com/)

**Exiting VIM**\
:qa          Close all files\
:qa!         Close all files, abandon changes\
:w           Save\
:wq / :x   Save and close file\
:q            Close file\
:q!           Close file, abandon changes