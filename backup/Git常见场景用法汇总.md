对于我个人而言，大概有下面几类git命令：
1. 常用的、不需要记忆的、熟练的git命令
2. 有用的、需要记忆的、不熟练的git命令
3. 可以被图形化界面替代的、偶尔用到的git命令
4. 其他命令











克隆时想要自定义本地仓库名：
``
git clone https://github.com/libgit2/ libgit2 mylibgit
``

GitHub 有一个十分详细的针对数十种项目及语言的`.gitignore`文件列表，你可以在 https://github.com/github/gitignore 找到它.

查看所有未暂存的改动：
`` git diff``

查看所有已暂存的改动：
``git diff --staged``

更好的git log，可以alias到glg：
`` git log --all --graph --decorate --oneline``

把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪：
``git rm --cached filename``


撤消对文件的修改：
``git checkout -- filename``