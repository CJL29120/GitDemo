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