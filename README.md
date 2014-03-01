#Road of Python Learning
#Python 学习之路
bypy是百度云网盘的Python实现，从作者那Fork过来的。
这里提交上来，只是为了测试git命令，无别的意思。
等我学会如何在本地删除该文件吧

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
