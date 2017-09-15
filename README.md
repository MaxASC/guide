# Hide git remote branches
By default, git uses `origin` as name for remote repository. There could be many remote repositories with different names. Before you go, check which repos are used with command  `git remote -v` and replace `origin` with preferred name.
	
1. Edit git config
	* Open conig file `.git/config`
	* Locate `[remote "origin"]` section with fetch config. It should look something like this:
	```
	fetch = +refs/heads/*:refs/remotes/origin/*
	```
	* Replace asterisks (`*`) with wldcard that match preferred branches.
	Note that you can add multiple descriptors
	```
	fetch = +refs/heads/master:refs/remotes/origin/master
	fetch = +refs/heads/develop*:refs/remotes/origin/develop*
	fetch = +refs/heads/feature_*:refs/remotes/origin/feature_*
	```

2. Delete remote branches
	* Delete them one-by-one
	```batch
	git branch -r -d origin/{branch1} origin/{branch2} origin/{branch3}
	```
	OR use wildcards (i've googled only bash oneliner and didn't test it, use at your own risk!)
	```bash
	git branch -r -d $(git for-each-ref --format='%(refname:short)' refs/remotes/origin/{wildcard})
	```
	
#### NOTE: do not use GUI or IDE utilities to remove remote tracking branch, because it may actually delete them.
