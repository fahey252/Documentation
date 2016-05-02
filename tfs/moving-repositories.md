#Move a TFS 2015 Git Repository Between Project Collections

Moving a Git project from one team project to another may need to be done as team project collections grow in size or other reasons.  Moving the repository with the procedure below is better than just copy and pasting files so all checkin history, branches, hidden files (i.e. `.gitignore` file) and other resources are preserved in the destination repository. Notice the differences in the URL's in the example below:

  __Source:__  `http://tfs-server:8080/tfs/ProjectCollection1/Project1/_git/Repository`  
  __Target:__ `http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository`

Lets move all code, history, branches etc. from the Source repository to the Target repository.

  1. Create new repository in target Project Collection/where you want the new code repository to be.
    i.e. Team Project Version Control Repositories via <http://tfs-server:8080/tfs/ProjectCollection2/Project2/_admin/_versioncontrol>
  2. Change directory into the source Git project and list the current remotes
  ```bash
  $ cd ~/Development/Automation
  $ git remote -v
  origin http://tfs-server:8080/tfs/ProjectCollection1/Project1/_git/Repository (fetch)
  origin  http://tfs-server:8080/tfs/ProjectCollection1/Project1/_git/Repository (push)
  ```

  3. Make sure there are no pending changes are on your local machine.  Perhaps reach out to other developers to make sure they do not have any updates that need pushed as well.
  ```bash
  $ git pull
  $ git status    # based on output, take action so nothing pending
  ```

  4. Remove the current push location `origin`.  There may be more locations based on the output from the `git remote -v` command executed earlier.
  ```bash
  $ git remote remove origin
  $ git remote -v   # likely no output based on your remote locations
  ```
  5. Go to your target TFS repository (http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository) and make sure it is initalized and there are no files in it.  If it has been initialized, there is a likely and default `README.md` file. Delete it so the repository is empty to avoid any merge conflicts.
  6. Add the target Git respository to the origin fetch and push action using the following pattern: `git remote add <name> <url>`
  ```bash
  $ git remote add origin http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository
  ```

  7. Confirm the new location has been added:
  ```bash
  $ git remote -v
  origin  http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository (fetch)
  origin  http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository (push)
  ```

  8. Since the old repository source and branch name has been removed, the new repository needs its default source and branch set using the following pattern `git branch --set-upstream-to=<source name>/<branch name>`
  ```bash
  $ git pull    # to bring down details about the master branch
  $ git branch --set-upstream-to=origin/master
  ```

  9. Now you need to merge your target branch with your source branch.  Leave any comments about the merge: why, from source url, etc.  When you do a pull, you will be prompted to merge.
  ```bash 
  $ git pull    # be sure to merge
  ```

  11. On your next `push`, the target respoistory will then be updated
  ```bash
  $ git pull
  ```

  12. Be sure to notify anyone else using this repository of the change.  The easiest way is to have them remove their old directory and re-clone from the new destination
  ```bash
  $ git clone http://tfs-server:8080/tfs/ProjectCollection2/Project2/_git/Repository
  ```

  13. Validate the the new destination has all the code you expected.
  14. Delete the old repository so no one accidently commits to it.  If many people use the repository, you could even leave the respository so it exists but leave a single `README.md` file that notes the new location. 

##TODO
  * Could create shell script to automate migration if needed.






