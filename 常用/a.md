 


###  git常用命令示例说明

#### 1.回到指定版本

```
git reflog   //查看命令历史，以便确定要回到未来的哪个版本

git reset --hard HEAD^   //在Git中，用HEAD表示当前版本 也就是最新的提交  上一个版本就是HEAD^ 上上一个版本就是HEAD^^  往上100个版本HEAD~100

git reset --hard  commit_id   //具体的提交版本号  版本号没必要写全，前几位就可以了，Git会自动去找

```
#### 2.撤销修改
```git checkout -- file  //丢弃工作区的修改  如果已add暂存区,恢复至暂存区,否则恢复到最新版本 即恢复到最近一次git commit或git add时的状态

git reset HEAD file  //暂存区的修改撤销掉（unstage），重新放回工作区
```

#### 3.删除文件
```
git rm file   //确实要从版本库中删除该文件
```






### git alias 配置

[git alias 配置](http://blog.csdn.net/herohenu/article/details/45842587)

```
[alias]
co = checkout
ci = commit
br = branch
st = status

unstage = reset HEAD --
last = log -1 HEAD

lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short


co = checkout // 切换分支，或去到特定的commit
ss = status
cm = commit -m
br = branch
bm = branch -m  // 修改当前分支的名称
bd = branch -D  // 删除某个分支
cb = checkout -b    // 新建一个和当前分支一样的分支，并切换过去
df = diff
ls = log --stat // 查看每次提交修改了哪些文件， git ls -n， 只看最近的n次提交
lp = log -p // 查看每次提交修改了那些行,git lp -n， 只看最近n次提交
plo = pull origin
pho = push origin
 
 
 ls = log --stat
    lp = log -p
    plo = pull origin
    plode = pull origin develop
    pho = push origin


```
    
    
### 参考资料
[这个零基础学Git的专栏也不错](http://blog.csdn.net/column/details/jacky-git.html)
[廖雪峰写的Git教程，超赞](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
[git-rebase(认真看，分析很到位)](http://blog.csdn.net/qq_27965129/article/details/52766549)
[git rebase简介(基本篇)](http://blog.csdn.net/u011630575/article/details/48968243)
[git rebase：永远不要衍合那些已经推送到公共仓库的更新](http://blog.csdn.net/trochiluses/article/details/14451777)

