# fittest
# 主要演示如何简单操作github，以及分支的rebase


# 初始化git远程仓库
xiapeijindeMac-mini:mse xiapeijin$ mkdir git-cmd-test
xiapeijindeMac-mini:mse xiapeijin$ cd git-cmd-test/
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git init
Initialized empty Git repository in /Users/xiapeijin/work/mse/git-cmd-test/.git/
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "# fittest" >> README.md
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add README.md 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "first commit"
[master (root-commit) 5072590] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git remote add origin https://github.com/xiapeijin/fittest.git
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push -u origin master
Username for 'https://github.com': xiapeijin@hotmail.com
Password for 'https://xiapeijin@hotmail.com@github.com': 
Counting objects: 3, done.
Writing objects: 100% (3/3), 217 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/xiapeijin/fittest.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
# 确认本地仓库以及远程仓库
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch
* master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch -a
* master
  remotes/origin/master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch -r
  origin/master
# 从主分支创建develop分支，并将本地分支切换到develop分支
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git checkout -b develop origin/master
Branch develop set up to track remote branch master from origin.
Switched to a new branch 'develop'
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md
# 将本地分支develop推送到远程分支
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/xiapeijin/fittest.git
 * [new branch]      develop -> develop
# 在develop分支工作并提交
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "test file" >> test-file-1.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch 
* develop
  master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add .
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "add test-file-1"
[develop 34bb65b] add test-file-1
 1 file changed, 1 insertion(+)
 create mode 100644 test-file-1.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/xiapeijin/fittest.git
   5072590..34bb65b  develop -> develop

# 通过github建立pull request，此时可以顺利merge test-file-1 到master分支

xiapeijindeMac-mini:git-cmd-test xiapeijin$ git pull
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/xiapeijin/fittest
   5072590..8b0c465  master     -> origin/master
Updating 34bb65b..8b0c465
Fast-forward
# ----------------------------------------------------------

# 切换到master分支，并作业和提交
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git checkout master
Switched to branch 'master'
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch
  develop
* master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "add a file to master" >> test-file-2.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add .
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "add test-file-2"
[master 103a550] add test-file-2
 1 file changed, 1 insertion(+)
 create mode 100644 test-file-2.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin master
To https://github.com/xiapeijin/fittest.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/xiapeijin/fittest.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-2.txt
# 由于远程master分支被merge了代码，以及发成变更，所以上边提交push会失败，此时通过pull将拉取更新
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git pull
Merge made by the 'recursive' strategy.
 test-file-1.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 test-file-1.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt
# 再次push，将成功提交
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin master
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 559 bytes | 0 bytes/s, done.
Total 5 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/xiapeijin/fittest.git
   8b0c465..fed4d0b  master -> master
# 再次切换到develop分支
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git checkout develop
Switched to branch 'develop'
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch
* develop
  master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt
# 由于develop是master的子branch，所以这边可以成功将test-file-2拉取
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git pull
Updating 8b0c465..fed4d0b
Fast-forward
 test-file-2.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 test-file-2.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt

# 再次编辑与提交develop分支，以及修改master分支，造成冲突
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "add test file to develop" >> test-file-3.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add test-file-3.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "add file 3 for test"
[develop 90fc621] add file 3 for test
 1 file changed, 1 insertion(+)
 create mode 100644 test-file-3.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 301 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/xiapeijin/fittest.git
   34bb65b..90fc621  develop -> develop
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git branch
* develop
  master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "modify file test" >> test-file-1.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add .
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "modify file for test"
[master 310f8a5] modify file for test
 1 file changed, 1 insertion(+)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 279 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/xiapeijin/fittest.git
   fed4d0b..310f8a5  master -> master
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git checkout develop
Switched to branch 'develop'
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commit each, respectively.
  (use "git pull" to merge the remote branch into yours)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt	test-file-3.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ echo "modify file to origin develop" >> test-file-1.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add .
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "modify file to origin develop"
[develop 00a743b] modify file to origin develop
 1 file changed, 1 insertion(+)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 301 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/xiapeijin/fittest.git
   90fc621..00a743b  develop -> develop
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt	test-file-3.txt
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt	test-file-3.txt
# 创建pull request，此时会看到代码冲突 
# 由于存在冲突，此时pull将失败
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git pull
Auto-merging test-file-1.txt
CONFLICT (content): Merge conflict in test-file-1.txt
Automatic merge failed; fix conflicts and then commit the result.
# 通过git rebase来merge分支
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git rebase master
test-file-1.txt: needs merge
Cannot rebase: You have unstaged changes.
Additionally, your index contains uncommitted changes.
Please commit or stash them.
xiapeijindeMac-mini:git-cmd-test xiapeijin$ cat test-file-1.txt 
test file
<<<<<<< HEAD
modify file to origin develop
=======
modify file test
>>>>>>> 310f8a5ab46d2d91fc498d67892dbecc189aaa57
# 人为解决冲突，并提交
xiapeijindeMac-mini:git-cmd-test xiapeijin$ vi test-file-1.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add test-file-1.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "rebase file 1"
[develop 50ab7c7] rebase file 1
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 321 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/xiapeijin/fittest.git
   00a743b..50ab7c7  develop -> develop
xiapeijindeMac-mini:git-cmd-test xiapeijin$ ls
README.md	test-file-1.txt	test-file-2.txt	test-file-3.txt
# 此时确认pull request，以及没有冲突，可以merge到master分支
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git pull
Already up-to-date.
xiapeijindeMac-mini:git-cmd-test xiapeijin$ vi test-file-3.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git add test-file-3.txt 
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git commit -m "XXX reset"
[develop 0cb324e] XXX reset
 1 file changed, 2 insertions(+)
xiapeijindeMac-mini:git-cmd-test xiapeijin$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 293 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/xiapeijin/fittest.git
   50ab7c7..0cb324e  develop -> develop
xiapeijindeMac-mini:git-cmd-test xiapeijin$ 

