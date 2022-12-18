## error: remote origin already exists.

如果你clone下来一个别人的仓库，在此基础上完成你的代码，推送到自己的仓库可能遇到如下问题：  
error: remote origin already exists.表示远程仓库已存在。  
因此你要进行以下操作：  
1、先输入`git remote rm origin` 删除关联的origin的远程库  
2、关联自己的仓库` git remote add origin https://gitee.com/xxxxxx.git`  
3、最后`git push origin master`，这样就推送到自己的仓库了。

## pull时报错

You asked to pull from the remote ‘origin’, but did not specify a branch. Because this is not the default configured remote for your current branch, you must specify a branch on the command line.
解决方法 ：
 在本地repository目录下打开gitbash，分别输入如下指令  
 `git config --global push.default current`  
 `git push -u`
问题应该能解决了