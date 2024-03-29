# Setting up your GitHub account within Jupyter Lab

![PracticumAI logo](https://github.com/PracticumAI/practicumai.github.io/blob/main/images/logo/PracticumAI_logo_250x50.png?raw=true)<img src='https://github.com/PracticumAI/practicumai.github.io/blob/main/images/icons/practicumai_git.png?raw=true' align='right' width=50> 

This tutorial will get your github account setup to work with git and GitHub within Jupyter Lab. It is primarily intended for use on [HiPerGator](https://www.rc.ufl.edu/), but will work on most computer systems where you run Jupyter.

## Create a GitHub.com account

1. Navigate to https://github.com/ and Click the **Sign up** button.
1. Enter the requested information to create your account.

## Setup SSH Keys for your account

**As of August 2021, GitHub.com no longer supports using username/password to push changes to repositories.** You should setup and add a public ssh key to your github.com account. [GitHub has good instructions on doing this](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh), but the main steps will be replicated here. If you encounter problems, I suggest checking the detailed instructions from GitHub.

1. In Jupyter Lab, open a Terminal by scrolling to the bottom of the Launcher panel and clicking on the terminal button:

   ![Screenshot of the open terminal button](images/open_terminal.png)

1. Create an ed25519 ssh key pair to use for GitHub. As outlined [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent), type: 

   `ssh-keygen -t ed25519 -C "your_email@example.com"`

   (**Replacing the email address** with the one you used when creating your GitHub account.)

   * If you can't remember which email you used for your GitHub account, you can check at this link: [https://github.com/settings/emails](https://github.com/settings/emails).

1. After typing the above command, you will be asked to enter a file in which to save the key. Hit `Enter` to accept the default name.

   > **Note**: The **name** *and* **location** of this file are important! Using a different name or changing the location will cause the key pair to not work.

1. Then you will be asked to enter a passphrase. Leave this empty. This is somewhat less secure, as anyone who has access to your private key would be able to impersonate you. **However Jupyter Lab does support ssh keys with a passphrase.** If you want to use GitHub in Jupyter Lab, do not add a passphrase--just hit `Enter` for the passphrase and verification.

1. Now that you have created the ssh key pair, we need to add the public portion to your github account. Type:

   `cat ~/.ssh/id_ed25519.pub`

   **and then copy the output.**

1. Go to your GitHub Settings at: [https://github.com/settings/keys](https://github.com/settings/keys).

1. As outlined [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account), click the New SSH Key button. [![Screenshot of the New SSH Key button](images/new_key.png)](https://github.com/settings/ssh/new)

1. Give the key a name, "HiPerGator" for example, and paste the public key text you copied above into the Key box.

1. **IMPORTANT: Do not skip this step** Test the key and add github.com to your known hosts. Back in the Jupyter terminal, type:

   `ssh -T git@github.com`

   (Do NOT replace the username, type it as git@github.com). 
  
   * Since this is likely the first time you have connected to github.com from the compute your are on, you will be asked if you want to trust the unknown host. Type: **`yes`**  
   * You should then see a reply like this:

   ```
   [magitz@login6 ~]$ ssh -T git@github.com
   Hi magitz! You've successfully authenticated, but GitHub does not provide shell access.
   ```

   This is the expected reply, your GitHub.com user name will be shown along with a note that you have successfully authenticated (using the setup ssh keys), but that GitHub does not provide shell access.

### Video walk-through

> There is also a [short video with a walk-through](https://web.microsoftstream.com/video/b0e02a2d-f108-44ff-aea2-276d98a8b524) of setting up ssh keys with github (Requires UF login).

## Next: Open the [02_exercise.ipynb](02_exercise.ipynb)



## Optional git configuration

From: <https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup>

> The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

 > Again, you need to do this only once if you pass the --global option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the --global option when you’re in that project.

> Many of the GUI tools will help you do this when you first run them.

### Setting an editor

Git uses your system's default editor--typically vim on Linux systems--as the text editor for commit messages. You can configure your preferred editor with one of the examples on this great table from the [Software Carpentry git lesson](http://swcarpentry.github.io/git-novice/02-setup/index.html):

| Editor             | Configuration command (do not type the "$")                           |
|:-------------------|:-------------------------------------------------|
| Atom | `$ git config --global core.editor "atom --wait"`|
| nano               | `$ git config --global core.editor "nano -w"`    |
| BBEdit (Mac, with command line tools) | `$ git config --global core.editor "bbedit -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl -n -w"` |
| Sublime Text (Win, 32-bit install) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublime_text.exe' -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"` |
| Notepad++ (Win, 32-bit install)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Notepad++ (Win, 64-bit install)    | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (Linux)       | `$ git config --global core.editor "kate"`       |
| Gedit (Linux)      | `$ git config --global core.editor "gedit --wait --new-window"`   |
| Scratch (Linux)       | `$ git config --global core.editor "scratch-text-editor"`  |
| Emacs              | `$ git config --global core.editor "emacs"`   |
| Vim                | `$ git config --global core.editor "vim"`   |
| VS Code                | `$ git config --global core.editor "code --wait"`   |
