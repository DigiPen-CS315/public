Updating your git-config user.email
-----------------------------------

Every git user gets an anonymous email "<_your-GitHub-username_>@users.noreply.github.com".  We can set our local git to use this email that is attached to our git commits to not expose our personal emails.

**Note**: If the push fails because of the email settings that I referenced in the GitHub setup process we need to do two things:

* * * * *

- Set your email to the automatic "fake" email that GitHub creates for each user. <_your-GitHub-username_>@users.noreply.github.com. To do this run the following command. 
- **Unfortunately, this will have to be done on every computer you want to use to develop**.
- Also, note that we are setting **global** settings here, you can make changes to the local git config as well.  Sometimes you may prefer different settings per repository clone or to be global.

**global**:
> `git config --global user.email "<_your-GitHub-username_>@users.noreply.github.com"`

**local**:(your command prompt must be in the same directory location as the git repository)
> `git config --local user.email "<_your-GitHub-username_>@users.noreply.github.com"`

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
            - See the updated Git documentation on Moodle for (a little) more information on VIM.
        - In most VIM documentation you will see this as one command `:x` or `:wq` to save and quit.