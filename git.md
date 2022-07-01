
## REMOVING
- remove file from git add
	- git reset <file>
- remove branch
	- locally
		git branch -d localBranchName

 	- remotely
		git push origin --delete remoteBranchName

## REBASE
- rebase z masterem
	- git rebase master
	- merge conflicts
	- git add ./file <- for files which conflicts were solved. This add means that conflicts were solved
	- git rebase --continue

## MERGE
Do rebase first. Otherwise there will be mess in logs. 

- git checkout feature-branch
- git merge master

## DISPLAYING
- branches
	- git branch <- local
	- git branch -r <- remote
	- git branch -a <- all

- logs
	- git log --oneline


## UNDO (https://www.nobledesktop.com/learn/git/undo-changes)
- uncommited 
	- 
##OT
HERS
- joing two commits
	- git reset --soft HEAD\~2
	- git commit

- moving head
	- backward
		- git reset --soft HEAD\~2
	- forward
		- git reset 'HEAD@{2}'
		- git reset --hard <commit_id>

- see what is in a stash:
	- git stash show



- man kann ein Issue mit dem Kommentar in commit z.B. git commit -m "add funcionality. closes #1" schließen 