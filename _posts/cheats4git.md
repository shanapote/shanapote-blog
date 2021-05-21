### Git command line short version...
1. Open WSL Ubuntu. We have your git repos at the root of the profile for the linux user. You have a shortcut to the Windows path.

2. Pull your repo

```Bash
git pull #grabs fresh site from github
```

3. Open an existing file or make a new one. Save when done. files with YYYY-MM-DD-title.md will get picked up by Jekyll and will show if not future dated. You can manually force excerpts by adding an 'excerpt: ' field to the properties table at the top of the jekyll md
4. Check status. Add new files to git tracking. ctrl+shift+c and ctrl+shirt+v for copy/pasta in the Ubuntu terminal.

```Bash
git status
```
```Bash
git add _posts/1968-05-03-HelloWorld.md
git status
```
5. Commit the local changes. This open an editor, delete the # infront of the changes you want to commit. ctrl+o, [ENTER], ctrl+x (save, accept defalut msg, exit)

```Bash
git commit -a
```
6. Push the local changes to github. Will prompt for user && PW (we can set up the ssh key so it uses that instead, no prompt).

```Bash
git push
```
7. Check the live host. File times and the file view are pretty 'real time'. Web hosting actually generates some of the files after change so there is a little lag after pushing changes.
