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
    
    
###fetch and pull
    
    
###merge and rebase
####git merge
    merge branch2 to branch1
    会在branch1上生成一个新的merge commit来完成代码的合并工作；并且在branch1看到被merge的branch2分支线；所有分支的commit都按照时间线往前走。
    
####git rebase（变基命令）
    rebase branch1 to matser
    会把branch1的commit放到master的最后面（叫做变基）；master的commit线上可以看到branch1的commit；时间线会被rebase过来的commit打乱。
    
    【原理：rebase需要基于一个分支来设置你当前的分支的基线，这基线就是当前分支的开始时间轴向后移动到最新的跟踪分支的最后面，这样你的当前分支就是最新的跟踪分支。】
    【对一个分支做“变基”操作，这意味着改变这个branch的初始commit(我们知道commits本身组成了一颗树）。它会在新的base上一个一个地运行这个分支上的所有commits.】
    
    举例:如果你从master拉了个feature分支出来,然后你提交了几个commit,这个时候刚好有人把他开发的东西合并到master了,这个时候master就比你拉分支的时候多了几个commit,
        如果这个时候你rebase master的话，就会把你当前的几个commit，放到那个人commit的后面。
     
     1. git rebase –abort 放弃一次合并
     2. rebase 过程中 fix conflict
       git add .
       git rebase --continue
       
####什么场景使用rebase/merge
    这个其他分支到底代表了什么？？?
    它是不是仅仅是一个local的，临时性的分支，创建它的目的仅仅是为了在开发它的同时又能防止master变得不稳定???
    
    rebase使用：
        local临时开发分支
        
    merge使用（需要对其进行跟踪; 该分支需要出现在历史图谱）：
        release分支； hot-fix分支； feature(CS没有使用)??
        ***git pull 内置执行merge   --> git pull --rebase 执行rebase
        
    fast forward模式
        git merge 会默认使用 fast forward模式进行合并。当删除合并的分支之后，会丢掉分支的信息。
        使用git merge --no-ff -m "this is a message for merging branch1" branch1
        
        
        
###reset and revert
    
    
    
    
    
    