## git贮藏功能使用场景

1、如果你某个分支开发过程中，这个分支的内容是要在本月月底上线的，但是生产上已经出现了一个重大bug，需要你立马去修复。你在分支开发的内容已经开发一部分了，工作区有内容是不能切换分支的，这个时候就可以用到贮藏的功能了

## git贮藏功能使用流程（sourceTree）

第一步：将修改一半的文件先贮藏起来，以防以后需要使用

![1574129769274](.\images\git贮藏\git-1.png)

选中修改的文件，点击贮藏按钮

第二步：再输入框中输入文字描述本次贮藏，然后点击确定按钮（之后就可以进行修改bug的工作）

![1574129926356](.\images\git贮藏\git-2.png)

第三步：应用贮藏功能

![1574130371631](.\images\git贮藏\git-3.png)

选择分支=>选择贮藏=>点击鼠标右键=>应用贮藏区=>确定=>恢复为修改一般的初始状态

![1574130600911](.\images\git贮藏\git-4.png)

## git贮藏功能使用流程（git shell）

- 贮藏

git stash：将当前工作贮藏

![1574130796152](.\images\git贮藏\git-6.png)

git stash save  "描述内容":给每个stash加一个message

![1574133235403](E:\own\biji\notes\images\git贮藏\git-5.png)

- 查看贮藏列表

git stash list：查看贮藏的列表

![1574131196038](.\images\git贮藏\git-7.png)

- 应用

git stash apply:将缓存堆栈中的第一个stash多次应用到工作目录中，但并不删除stash拷贝

git stash apply stash@{0} ：恢复贮藏序列为0的贮藏中的工作内容,但并不删除stash拷贝

![1574131410296](.\images\git贮藏\git-8.png)

- 删除

git stash drop：将缓存堆栈中的第一个stash删除

git stash drop stash@{0}：删除贮藏序列为0的贮藏中的工作内容

![1574132441468](E:\own\biji\notes\images\git贮藏\git-9.png)

git stash clear：删除所有缓存的stash

- 应用并删除

git stash pop：将缓存堆栈中的第一个stash删除，并将对应修改应用到当前的工作目录下。

git stash pop stash@{0}：将贮藏序列为0的贮藏中的工作内容应用并且删除

![1574133389346](.\images\git贮藏\git-10.png)

- 查看具体的修改记录

git stash show:查看缓存堆栈中的第一个stash的diff

git stash show stash@{0}:查看贮藏序列为0的stash的diff

![1574133731206](.\images\git贮藏\git-11.png)

