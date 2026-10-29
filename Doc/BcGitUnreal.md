# How to use git with Unreal at Bellevue college

## Track the project in a git repository

1. Copy a [.gitignore](https://github.com/github/gitignore/blob/main/UnrealEngine.gitignore) file into the root of your project, `cd C:\Users\ur.username\Documents\ProjectsUnreal\NameYouGaveIt\.gitignore`.
2. Download and run [Git for Windows/x64 Portable](https://git-scm.com/install/windows)
3. In the lower right of Unreal Editor, click `Revision Control` to let it know you're using git by linking it to the extracted folders `.\cmd\git.exe`.
4. In the extracted folder, double click `git-cmd.exe` to run it.
5. In the command prompt window that opens, tell it where you Unreal project is located by entering `cd C:\Users\ur.username\Documents\ProjectsUnreal\NameYouGaveIt`.
6. Initialize a git repo there using `git init .`.
7. Add all files not .gitignored using `git add .` to stage them to be committed.
8. Make your first commit with `git commit -m "my first commit"`.
9. Now when you make changes to an asset in Unreal, [Unreal Editor can compare it to the previously committed version](https://dev.epicgames.com/documentation/unreal-engine/ue-diff-tool-in-unreal-engine).

That's all you need. You can stop here and copy the entire unreal project as you were doing before. If you instead want to rely on GitHub.com for mantaining copies, then read on.

## Sync the project with GitHub.com

Setting up a school computer to be able to commit to GitHub.com is not only a challenge, it is also a security risk. That is because school computers are shared with other students.

Secure options:

1. Manually copy the .git folder to a flashdrive. Authorize a personal machine to commite to github. Then use the flashdrive's .git copy to commit to GitHub.com.
2. Use a flash drive as a proxy remote. On a personal machine, use the remote on the flash drive to commit to GitHub.com.
3. Map OneDrive with a drive letter so it can be used as a proxy remote. On a personal machine, use the remote on OneDrive to commit to GitHub.com.
4. Limit the damage. Limit the school computer to be authorized to commit to only a single repository.

## Authorize commits to only a single repository

Single repository access is best controlled through [Deploy keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys). Setup is challenging, but afterwards the process is not only fast, it follows GitHubs' intended flow.

1. Use the `ssh` command to generate keys and a config file as described on https://deuts.org/p/ssh-key-github-repo.
2. Zip up your `C:\Users\ur.username\.ssh` folder and store it on the cloud or a flashdrive.
3. On any school computer, extract that `.ssh` folder into the machines `C:\Users\ur.username\` folder. Portable git looks in that `.ssh` folder when doing any operation.

## How GitHub.com recognizes your commits

For GitHub.com to recognize your account made a commit the commit must match the username and email associated with your GitHub account. You can find this on GitHub by going to your account profile settings(TODO: link to settings).

1. Config Portable Git to use your username and email.
```
git config --global user.name "YourUserName"
git config --global user.email your@e.mail
```

2. Once git is configured, you can DESTRUCTIVELY (AKA rewrites hashes causes this repo to have sync issues with other copies of this repository) overwrite all commits in your repository to use the global username and email with `git -c rebase.instructionFormat="%s%nexec GIT_COMMITTER_DATE=\"%cD\" GIT_AUTHOR_DATE=\"%aD\" git commit --amend --no-edit --reset-author" rebase --root`
