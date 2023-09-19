| 命令                | 描述                             |
| ------------------- | -------------------------------- |
| git init            | git仓库初始化                |
| git clone <giturl>  | 复制现有仓库                     |
| git status          | 查看git仓库状态                  |
| git log             | 查看commit列表记录<br />--oneline  浓缩成一行一条记录<br />--stat         输出文件改动的统计数据<br />-p               输出改动文件的具体内容<br />-w              忽略空格的修改和-p一起用 |
| git show <SHA> | 查看commit具体记录，也有--stat,-p,-w的配置 |
| git add .       | 将工作区全部改动提交到暂存区                              |
| git commit       | 将暂存区改动提交到版本库<br />-m             添加本次改动的title<br />--amend  更改最后一个commit包括缓存区改动和改动的title |
| git diff            | 查看工作区修改                   |
| git tag -a <tagname> | 设置commit标签<br />-a               设置标签名<br />-d               删除标签名 |
| git checkout <Branch> | 切换分支                         |
| git checkout -b <本地分支名> <远程分支名>  | 创建本地分支并关联远程分支            |
| git checkout -t <远程分支名>         | 创建本地分支并自动关联远程分支，本地分支名和远程分支一致 |
| git checkout .| 撤销工作区的修改(只能撤销在已有文件上的修改) |
| git restore .| 撤销工作区的修改 |
| git clean -df | 删除工作区新增的文件 |
| git clean -xdf | 删除工作区新增的文件和文件夹 |
| git merge <branch>  | 合并分支                         |
| git revert <sha> | 还原，并向前提交一个新的commit来保存还原的内容 |
| git reset | 重置，会删除commit，慎用<br />--hard  会清空工作目录和暂存区的改动<br />--soft    则会保留工作目录的内容，并把因为保留工作目录内容所带来的新的文件差异放进暂存区。<br />--mixed  默认行为，保留工作目录，并且清空暂存区<br />HEAD^表示当前版本<br />HEAD^^上上一个版本<br />HEAD~2上上一个版本 |
| git reset HEAD^ | 使用场景：已使用git add . 命令，未使用git commit -m ''命令 |
| git reset --soft HEAD^ | 使用场景：已使用git commit -m ''命令，撤销之后会把修改放在暂存区 |
| git reset  --hard  HEAD^ | 使用场景：已使用git commit -m，撤销之后不会保留任何更改，比如打包之后提交了commit，想重新打包，则可以使用 |
| git reset HEAD    | 撤销缓存区的修改，撤销上一次add |
| git remote -v       | 远程库查询                       |
| git remote add origin <url>|添加远程库|
| git remote remove <origin>|删除远程库|
| git push origin --delete <branch>|删除远程分支|
| git push <分支名>| 推送本地分支到远程分支 |
| git push origin --delete <branch>|删除远程分支|
| git push origin --delete <分支名>    | 删除远程分支            |
|git config --global core.autocrlf false                      | 禁用换行方式转换           |
| git push -u origin master | 跟踪远程分支 |
| git push -f | 强制推送 |
| git pull <分支名>| 拉取远程分支到本地分支 |
| git pull -u origin dev | 拉取远程分支 |
| git branch                           | 列出所有分支(仅本地分支)            |
| git branch -a                     | 列出所有分支(包括远程分支)            |
| git branch -d <分支名>               | 删除分支               |
| git branch -D <分支名> | 强行删除分支 |
| git branch <分支名>                    | 创建新分支                |
| git branch -m <旧分支名>  <新分支名> | 重命名分支              |
| git branch -vv | 查看本地分支与远程分支的关联分支            |
| git clean -n | 显示将要删除的新增文件，不显示新增的文件夹及包含的文件 |
| git clean -f | 删除新增文件，不删除新增的文件夹及包含的文件 |
| git clean -df | 删除新增文件以及新增的文件夹和其包含的文件 |
| git fetch <分支名>| 获取远端的更新，但不进行合并 |
| git config --global core.quotepath false  | git中文显示数字的问题 |
| git log --pretty=oneline 文件名 （文件名是文件路径+文件名，输入完整） | git查看某个文件的提交历史 |
| git show 某次commit 的哈希值  文件名 | git查看某个文件某次提交的修改 |
| git rm -r --cached . | 清除缓存，使.gitignore中的内容生效 |
|||
|git config --global gui.encoding utf-8||
|git config --global i18n.commit.encoding utf-8||
|git config --global i18n.logoutputencoding utf-8||
|$env:LESSCHARSET='utf-8'| 解决 powerShell git log显示中文的问题|
| git config --global core.autocrlf false | git提示LF CRLF转换的警告 |
| git blame -L <lineStart>,<lineEnd> <path+fileName>  | git查看部分行的历史改动记录 |
|git config --global core.quotepath false  | 解决中文显示成数字的bug |
|  GIT_MERGE_AUTOEDIT=no      export GIT_MERGE_AUTOEDIT|  用来解决git bash 合并时自动打开VIM编辑器的问题 |
| git blame | 找到具体代码的责任人 |

### git恢复某个文件到上一个提交版本

git提交了比较多的文件到远程，但是在合并时发现其中有一个文件合并有冲突或者某个原因不想修改该文件了，那就需要单独把这个文件回退到上一个提交版本状态。方法如下：

1.首先查看一下该文件的commit记录：git log 文件，例如 git log src/index.java

2.找到需要提交到上一个版本的commit号，然后checkout该文件的上一版本，输入下面的指令：

git checkout [commit id] 文件，例如 git checkout a57fb4b474888f0db4cba18de2180496 src/index.java

3.然后将checkout的版本提交到本地

git commit -m "回退到上一版本"

4.最后将改变提交到分支远程：

git push origin 分支名

这样此文件本地和远程都是上一版本内容