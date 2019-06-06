####space name
    Workspace：工作区
    Index / Stage：暂存区
    Repository：仓库区（或本地仓库）
    Remote：远程仓库
    
######新建branch2，并指向commit
    git branch branch2 0995682972493164fb6f8f972a65ccf31d00c448
    branch2分支只显示commit 0995682972493164fb6f8f972a65ccf31d00c448及之前的代码。
    

###branch
######新建并切换分支
    git checkout -b branch1 == git branch branch1 + git checkout branch1
    
######list all remote branch
    git branch -r
    
######list all local and remote branch
    git branch -a
    
######切换到上一个分支
    git checkout - 【只会在两个分支之间来回切换，不能追溯更远】