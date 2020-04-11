# git多人合作
    使用主分支Master与开发分支Develop模式遇到的问题以及建议.
## 问题
1. 发版前需要封版测试, 修复bug而不能提交新需求, 有的新需求做了一半不能提交, 可能还和其他同学修改bug文件有冲突.

2. 开发一个大的需求功能, 直接提交到主开发分支(develop), 如果有bug, 影响所有的开发测试同学.

3. 任务未完成又需要修改紧急bug, bug影响的文件和未完成任务涉及同一文件. 

4. 代码被冲掉(还原成老的代码), 开发同学在公用Develop分支进行开发, 可能由于部分同学没能及时拉取代码, 同时解决冲突的时候没处理好导致.

5. 有的开发同学有多台设备(大多公司台式机和家里一台), 进行一半的任务不能提交到Develop分支, 在家或其他地方不能继续开发.

##建议
1. **管理者只维护Master和Develop分支**.

2. **每个开发都建立自己的临时开发分支**, 一般都是从Develop分支切出来, 开发自己维护, 无需管理者干预.

3. **对于大的功能, 改动文件较多也单独切临时分支**, 开发完成提交临时分支, 测试同学在这个临时分支测试通过再合并到Develop分支.

4. 开发同学在每次修改临时开发分支代码前, **首先合并Develop分支到临时分支**, 合并临时分支到Develop分支前也需要 **先合并Develop分支到临时分支, 冲突都在临时分支上解决后并验证没问题再合并到Develop!**

<img src="https://github.com/iqidan/Notes/blob/master/Images/git-cooperation.png" style="width: 500px;">

## 多临时分支利弊
1. 利: 解决上述发现的问题, 比如新需求进行一半有紧急bug需要修复, 而且涉及同一文件, 可以直接提交未完成的代码到自己的临时分支, 然后切换为Develop修复紧急bug.

2. 弊: 操作步骤多了些(多了临时分支和Develop的合并操作)以及多占用些云端服务器磁盘内存.

## git界面操作软件推荐
[SourceTree](https://www.sourcetreeapp.com/) 超级方便 

## 推荐学习
1. [图解GIT](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
2. [GIT DOCUMENT](https://book.git-scm.com/docs/git)
3. [Think Like (a) Git](http://think-like-a-git.net/)
4. [GIT & SVN](https://www.cnblogs.com/Sungeek/p/9152223.html)
5. [Git常用命令及方法大全](https://www.cnblogs.com/miracle77hp/articles/11163532.html)