对于我个人而言，大概有下面几类git命令：

1. 常用的、不需要记忆的、熟练的git命令
2. 有用的、需要记忆的、不熟练的git命令
3. 可以被图形化界面替代的、偶尔用到的git命令
4. 其他命令

下面主要记录后三种：

- 当具有多个私钥时，git clone 指定私钥克隆
```
git clone remote_url.git --config core.sshCommand="ssh -i /path/to/id_rsa"
```
- 克隆时想要自定义本地仓库名：
```
git clone https://github.com/libgit2/ libgit2 mylibgit
```
- GitHub 有一个十分详细的针对数十种项目及语言的`.gitignore`文件列表，你可以在 https://github.com/github/gitignore 找到它.
- 查看所有未暂存的改动：
```
git diff
```
- 查看所有已暂存的改动：
```
git diff --staged
```
- 更好的git log，可以alias到glg：
```
git log --all --graph --decorate --oneline
```
- 把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪：
```
git rm --cached filename
```
- 取消暂存
```
git reset HEAD <file>
```
- 撤消对文件的修改：
```
git checkout -- filename
```

-  显示远程仓库及其url
```
git remote -v
```
- 从远程仓库中获得数据
```
git fetch [remote-name]
```
- 推送
```
git push [remote-name] [branch-name]
```
- 仅创建分支，但并不自动切换到新分支中去
```
git branch [branch-name]
```
- 切换分支
```
git checkout [branch-name]
```
- 创建新分支并切换到该分支
```
git checkout -b [branch-name]
```
- 打标签
```
git tag
```