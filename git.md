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
    
    
###branch/commit/head
    一个git仓库只有一个head, head指向当前的branch（当前是哪个分支，head就指向哪个分支）；branch指向自己分支最新的commit。
    
    eg:
        head --> master --> last commit on master
        
        git checkout dev =====>    head --> dev --> last commit on dev
        
        git checkout master ==>    head --> master --> last commit on master
        
        git merge dev ========>    head --> master --> last commit on master after merge
    
    
###fetch and pull
    fetch: 从remote获取最新版本到本地，不会自动merge
    
    git pull origin branch1 ===> git fetch origin branch1  +  git merge origin/branch1
    

###branch
######新建并切换分支
    git checkout -b branch1 == git branch branch1 + git checkout branch1

######git checkout -
     切换到上一个分支【只会在两个分支之间来回切换，不能追溯更远】
    
######新建branch2，并指向commit
    git branch branch2 0995682972493164fb6f8f972a65ccf31d00c448
    branch2分支只显示commit 0995682972493164fb6f8f972a65ccf31d00c448及之前的代码。
    
######git branch --track branch2 origin/branch1
    新建一个本地分支branch2，与已经存在的指定远程分支origin/branch1建立追踪关系

######git branch --set-upstream branch1 origin/master ==> git branch --set-upstream-to=origin/master branch1
    equal to: git checkout branch1 + git branch --set-upstream-to=origin/master
    在现有分支branch1与指定的远程分支origin/master之间建立追踪关系。
    
######git branch --unset-upstream branch1 
    equal to: git checkout branch1 + git branch --unset-upstream
    取消本地分支branch1的追踪关系。
       
###merge and rebase
####git merge
    merge branch2 to branch1
    会在branch1上生成一个新的merge commit来完成代码的合并工作；并且在branch1看到被merge的branch2分支线；所有分支的commit都按照时间线往前走。
    
####git rebase（变基命令）
    rebase branch1 to master
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
######git reset (修改HEAD的位置，将HEAD指向的位置改变为之前存在的某个版本, 被撤销的commit不再保留)
    git reset HEAD 将暂存区的内容撤回到工作区
    git reset HEAD^ = git reset HEAD~1 = git reset previous_commit_id 撤回最新一个提交，并保留修改内容在工作区
    
    git reset --hard commit_id 撤销到并包括'commit_id'那次提交，并且不保留撤销区间的修改内容
    git reset --hard commit_id ==> git reset commit_id + git checkout <files>
    
    由于本地的HEAD指向比远程库的要旧，所以此时push 需要使用-force.
    
######git revert (创建一个新的版本，这个版本的内容与要回退的目标版本一样，HEAD指向新生成的版本)
    git revert HEAD 撤销最新一次提交
    git revert HEAD^ 撤销最新两次提交
    
    git revert commit_id 回到commit_id'那次提交之前的版本

###remote
######git remote / git remote -v/ git remote show <主机名>
    查看远程主机/ 查看远程主机网址信息/ 查看主机详细信息
    
######git remote add <主机名> <网址>
    添加远程主机
    
######git remote rename <old> <new>
    修改远程主机的名字
    
    

###push
######git push origin branch1
    将本地分支推送到与之存在追踪关系的origin远程主机的分支branch1；如果该远程分支不存在，则会被新建
    
######git push origin
    将本地分支推送到与之存在追踪关系的origin远程主机的对应分支(通常两者同名)
    如果当前分支只有一个追踪关系，则可以省略远程主机名，使用 git push
    
######git push -u origin branch1
    如果当前分支与多个远程主机存在追踪关系，可以使用-u指定一个默认主机，之后就可以直接使用'git push'
    

    