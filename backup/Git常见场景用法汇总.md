对于我个人而言，大概有下面几类git命令：

1. 常用的、不需要记忆的、熟练的git命令
2. 有用的、需要记忆的、不熟练的git命令
3. 可以被图形化界面替代的、偶尔用到的git命令
4. 其他命令

下面主要记录后三种：

### 本地查看
- GitHub 有一个十分详细的针对数十种项目及语言的[`.gitignore`文件列表](https://github.com/github/gitignore)
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

### 本地编辑
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


### 分支
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
### 与remote互动
- 浅克隆以提高大型项目的克隆速度
- 指定克隆哪个分支
- 克隆时自定义本地仓库名
- 当具有多个私钥时，指定使用哪个私钥克隆
```
git clone -b cling-latest --depth=1 path-to/gitrepo.git localrepo --config core.sshCommand="ssh -i /path/to/id_rsa"
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