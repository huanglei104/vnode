git restore : 恢复工作区的文件 
            --worktree / -W  : 恢复工作区文件 ，默认的
            --staged / -S : 恢复暂存区文件
                (以上两个选项可同时使用)
            --source / -s : 指定一个用来恢复的源。默认的，工作区从暂存区恢复，暂存区从HEAD恢复


git reset : 重置HEAD为指定状态
            默认的： 将暂存区的文件恢复为指定状态，不影响工作区和当前分支