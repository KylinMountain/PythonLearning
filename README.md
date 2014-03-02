#Road of Python Learning
#Python 学习之路


# git比较本地仓库和远程仓库差异
转载自[git 如何比较本地仓库和远程仓库之间的差异？](http://hi.baidu.com/configuration/item/02329df98b43d40cd89e725d)

在pull之前，可以先比较本地仓库和远程仓库之间的差异
1. 添加需要比较的远程仓库；
> git remote add foobar git://github.com/user/foobar.git

2. 取回foobar的内容，fetch不会修改本地的内容；
> git fetch foobar

3. 比较本地分支和远程分支之间的差异
> git diff master foobar/master

4. 远程分支已经修改，本地未同步的变更；
> git diff HEAD...origin/master

5. 本地分支已经修改，远程未同步的变更；
> git diff origin/master...HEAD


## Python教程
今天发现一个比较好的Python学习教程，一位大牛写的[Python教程](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000)

##Git教程
还是上面那位大牛写的，[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

##关于这位大牛
廖雪峰，十年软件开发经验，业余产品经理，精通Java/Python/Ruby/Visual Basic/Objective C等，对开源框架有深入研究，著有《Spring  2.0核心技术与最佳实践》一书，多个业余开源项目托管在[GitHub](https://github.com/michaelliao)。
