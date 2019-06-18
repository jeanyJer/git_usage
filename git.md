####space name
    Workspace：工作区
        -- add
    Index / Stage：暂存区
        -- commit
    Repository：仓库区（或本地仓库）
        -- push
    Remote：远程仓库
    
    
    Remote --fetch/clone --> Repository --checkout --> workspace
    
    Remote --pull --> workspace
    
    

###branch
######新建并切换分支
    git checkout -b branch1 == git branch branch1 + git checkout branch1
    
######list all remote branch
    git branch -r
    
######list all local and remote branch
    git branch -a
    
######切换到上一个分支
    git checkout - 【只会在两个分支之间来回切换，不能追溯更远】
    
######新建branch2，并指向commit
    git branch branch2 0995682972493164fb6f8f972a65ccf31d00c448
    branch2分支只显示commit 0995682972493164fb6f8f972a65ccf31d00c448及之前的代码。
    
    
###merge and rebase
####git merge
    merge branch2 to branch1
    会在branch1上生成一个新的merge commit来完成代码的合并工作；并且在branch1看到被merge的branch2分支线；所有分支的commit都按照时间线往前走。
    
####git rebase（变基命令）
    rebase branch1 to matser
    会把branch1的commit放到master的最后面（叫做变基）；master的commit线上可以看到branch1的commit；时间线会被rebase过来的commit打乱。
    
    【原理：rebase需要基于一个分支来设置你当前的分支的基线，这基线就是当前分支的开始时间轴向后移动到最新的跟踪分支的最后面，这样你的当前分支就是最新的跟踪分支。】
    
    举例:如果你从master拉了个feature分支出来,然后你提交了几个commit,这个时候刚好有人把他开发的东西合并到master了,这个时候master就比你拉分支的时候多了几个commit,
        如果这个时候你rebase master的话，就会把你当前的几个commit，放到那个人commit的后面。
     
     1. git rebase –abort 放弃一次合并
     2. rebase 过程中 fix conflict
       git add .
       git rebase --continue
       
####什么场景使用rebase/merge
    
    
    
    