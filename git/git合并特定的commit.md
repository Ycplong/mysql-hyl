# git合并特定的commit

多版本并行开发的时候一般都是一个版本一个分支，验收通过上线的时候将该分支直接合并到生产环境中

但是有的时候我们只想合并某一个或几个commit，来满足业务的需求(这个功能今晚上，其他可以晚点上)

使用git cherry-pick <commit id> 合并特定的commit，操作对象是commit而非分支

commit id 可以是来自任何分支，他不关心分支，因为commit id 总是唯一的

使用git log来查看commit id，可以是完整的commit id，也可以是id前6位

实际演示

本地有两个分支，master和uat，我们将uat分支的commitid=9494f1的记录合并到master上，而不合并整个分支
```
  git checkout -b uat  // 创建uat分支
  ... // 修改两次，提交两次commit
  git log   // 记录两次修改的commit   第一次修改为9494f1 第二次修改为d3450d
  git checkout master // 切回master分支
  git cherry-pick 9494f1  // 合并commit
  git log // 发现commit已合并
```

