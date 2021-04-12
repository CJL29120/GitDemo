# GitDemo
git学习



## idea
[官网学习教程](https://www.jetbrains.com/help/idea/using-git-integration.html)



**创建分支**

​	idea右下角 git branch   点击New Branch   输入分支名称即可

​	**注意：** idea 在那个A_branch上创建分支，新分支内容就是基于A_branch的 





**刷新remote分支**

​	idea右下角 git branch 点击Fecth 就是一刷新标志





**Git branches**

> 弹出的Git branches指示一个分支是否有尚未被获取的提交





通过 **Move Lines to Another Changelist** action 将某一改变的代码模块提交的 到自命名列表中，当提交代码时就可以把相关的代码都一块提交了 （快捷键 Shirt+Alt+M）；按照以上操作，在提交代码时就能按功能模块地提交代码，且可以清晰的描述好各自的





在git管理面板中 选择一条commit右键 choose **Show Repository at Revision** 即可看到该版本的历史文件





**切换分支**

切换分支时 未提交的修改代码会随着切换 被引入到新切换的分支上，切换时会有Force Checkout、Smart Checkout、Dont Checkout选择，切换成功后 idea会有popup提示（可选择Rollback）；

> If you click **Smart Checkout**, IntelliJ IDEA will [shelve](https://www.jetbrains.com/help/idea/work-on-several-features-simultaneously.html#shelve) uncommitted changes, check out the selected branch, and then unshelve the changes. If a conflict occurs during the unshelve operation, you will be prompted to merge the changes. For details, see [Resolve conflicts](https://www.jetbrains.com/help/idea/resolve-conflicts.html).





### Apply changes from one Git branch to another

###### 抛出问题:

**为什么不要再公共分支使用rebase?**
 因为往后放的这些 commit 都是新的,这样其他从这个公共分支拉出去的人，都需要再 rebase,相当于你 rebase 东西进来，就都是新的 commit 了

- 1-2-3 是现在的分支状态
- 这个时候从原来的master ,checkout出来一个prod分支
- 然后master提交了4.5，prod提交了6.7
- 这个时候master分支状态就是1-2-3-4-5，prod状态变成1-2-3-6-7
- 如果在prod上用rebase master ,prod分支状态就成了1-2-3-4-5-6-7
- 如果是merge
   1-2-3-6-7-8
   ........ |*4-5*|
- 会出来一个8，这个8的提交就是把4-5合进来的提交

 **merge和rebase实际上只是用的场景不一样**
 **更通俗的解释一波.**
 比如rebase,你自己开发分支一直在做,然后某一天，你想把主线的修改合到你的分支上,做一次集成,这种情况就用rebase比较好.把你的提交都放在主线修改的头上
 如果用merge，脑袋上顶着一笔merge的8,你如果想回退你分支上的某个提交就很麻烦,还有一个重要的问题,rebase的话,本来我的分支是从3拉出来的,rebase完了之后,就不知道我当时是从哪儿拉出来的我的开发分支



##### **注意:**

- 不要在公共分支使用rebase
- 本地和远端对应同一条分支,优先使用rebase,而不是merge



### 使用 `rebase` 和 `merge` 的基本原则：

1. 下游分支更新上游分支内容的时候使用 `rebase`     （下游 如dev分支；上游 如main、master等）
2. 上游分支合并下游分支内容的时候使用 `merge`
3. 更新当前分支的内容时一定要使用 `--rebase` 参数

例如现有上游分支 master，基于 master 分支拉出来一个开发分支 dev，在 dev 上开发了一段时间后要把 master 分支提交的新内容更新到 dev 分支，此时切换到 dev 分支，使用 `git rebase master`

等 dev 分支开发完成了之后，要合并到上游分支 master 上的时候，切换到 master 分支，使用 `git merge dev`



### Stash  暂存功能

**使用场景**
功能开发一半，改了个BUG需要提交，此时就需要把开发功能的改动代码暂存起来，将BUG修改内容进行提交并推送，推送后再恢复原有改动

**执行流程**

1. 先git commit要提交的内容
2. 将剩下内容通过git stash存入暂存区
3. git pull --rebase拉取远程最新代码
4. 将提交记录通过git push推到远程仓库
5. git stash pop恢复之前暂存的改动



在idea中右键 Git| Stash Changes 暂存，Git| Unstash Changes 恢复暂存



### cherry-pick

各位码农朋友们一定有碰到过这样的情况：在develop分支上辛辛苦苦撸了一通代码后开发出功能模块A，B，C，这时老板过来说，年青人，我们现在先上线功能模块A，B。你一定心里一万只草泥马奔腾而过，但为了混口饭吃必须得按老板的意思办事啊。

怎么办？一个办法就是，重新建一个分支，然后再把功能模块C回退，留下功能模块A，B。这种做法不是不行，但是有更好的办法，那就是git所提供的cherry-pick功能。

cherry-pick类似于一个定制化的merge，**它可以把其它分支上的commit一个个摘下来**，合并到当前分支。