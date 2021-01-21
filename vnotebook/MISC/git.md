git 的默认分支（master） 在第一次提交的时候才会创建

初始目录：
     branches/    config       description  HEAD         hooks/       info/        objects/     refs/
git config:
              --local(默认)，表示使用仓库下面的 .git/config 配置文件
               --global，表示使用~/.gitconfig配置文件 
              --system ，表示使用$(prefix)/etc/config配置文件
               -e 编辑配置文件（直接修改配置的方式）

git commit :
          --amend      对最新的提交进行修改，而不是产生一个新的提交 
          --allow-emply     允许一个没有任何改变的提交 
          -C    使用一个已有的提交的信息(包括日志，作者，时间)去创建一个提交
          -c    与-C 类似， 但在提交时会调用出编辑器，来修改信息
          --reset-author    仅在使用 -C /-c/--amend选项时有用，使用现在的作者原来的作者(时间信息也会更新)
          -s   在提交日志后面添加提交者的签名
          -a 将所有工作区的更改直接提交到版本库，跳过暂存区。（对新增的未跟踪的文件没有影响）

git log:
          -p   显示变化的内容
          -num  num是一个数字，仅显示几次提交
          --stat 显示一些总结性的信息
          --graph 画线来展示分支
          --author=author 过滤出author的提交记录
          --committer 过滤提交者
          --grep=str  过滤出提交信息中有str的
          -S str 过滤出提交内容与str有关的(添加或删除)
           path 只显示path的提交记录，前面可以加个 -- 与前面的选项分开
          --pretty 以给定的格式输出 格式可以选择 --pretty=oneline, short, medium, fulll, fuller, email, raw 还能自定义格式

git status:
          显示工作区的状态
          -s 显示精简的信息

git reset:
          --hard 重置版本库时，工作区和暂存区的内容也会被重置
          --soft 重置版本库，但保留工作区，重置带来的变化放入暂存区
          --mixed 默认， 重置版本库，只保留工作区，并且所有的变化都会放入工作区

git diff:
          没有任何选项和参数   比较工作区和暂存区的不同
          <commit>    比较工作区和版本库的不同
          --cached/--staged  比较暂存区和版本库的不同

git rm:
          从暂存区移除对文件的跟踪，且工作区也会同时删除(删除之前暂存区的内容必须提交过了，或者使用git rm -f )
          --cached  不将工作区的文件删除

git mv:
          对文件重命名

git rev-parse :
          --git-dir   显示版本库所在目录,相对路径
          --show-toplevel  显示版本库父目录的绝对路径
          --show-prefix  显示当前目录相对于工作区的相对路径  只能在子目录调用 
          --show-cdup  与 --show-prefix 类似， 但路径用../. 表示 只能在子目录调用 

git ls-tree 
          浏览版本库

git  ls-files
          浏览暂存区
          -s  输出中显示更多的内容 