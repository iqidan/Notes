# git操作
## git基础操作
    参考的[Git常用命令及方法大全],很全面~

## git多人合作使用主分支Master与开发分支Develop模式遇到的问题以及建议
### 问题
1. 发版前需要封版测试,修复bug而不能提交新需求,有的新需求做了一半不能提交,可能还和其他同学修改bug文件有冲突
2. 开发一个大的需求功能,直接提交到主开发分支(develop),如果有bug,影响所有的开发测试同学
3. 需求做了一部分又需要修改bug,bug影响的文件和新需求涉及同一文件
4. 代码被冲掉(还原成老的代码),开发同学在公用Develop分支进行开发,可能由于部分同学没能及时拉取代码,同时解决冲突的时候没处理好导致
5. 有的开发同学

###建议
1. **管理者只维护Master和Develop分支**
2. **每个开发都建立自己的临时开发分支(一般都是从Develop分支切出来,自己开发维护)**
3. **对于大的功能,改动文件较多也单独切临时分支**
4. 开发同学在每次修改临时开发分支代码前 **首先合并Develop分支到临时分支**,合并临时分支到Develop分支前也是 **先合并Develop分支到临时分支,冲突都在临时分支上解决后验证没问题再合并到Develop**

mermaid
graph TD
    合并Develop到临时分支[合并Develop到临时分支] --> 修改代码[修改代码] --> 本地代码提交到云端临时分支仓库[本地代码提交到云端临时分支仓库] --> 合并Develop到临时分支[合并Develop到临时分支] --> 合并临时分支到Develop分支[合并临时分支到Develop分支]


### 利弊
1. 





## git界面操作软件推荐,超级方便[SourceTree](https://www.sourcetreeapp.com/)



## 参考
1. [图解GIT](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
2. [GIT DOCUMENT](https://book.git-scm.com/docs/git)
3. [Think Like (a) Git](http://think-like-a-git.net/)
4. [GIT & SVN](https://www.cnblogs.com/Sungeek/p/9152223.html)
5. [Git常用命令及方法大全](https://www.cnblogs.com/miracle77hp/articles/11163532.html)