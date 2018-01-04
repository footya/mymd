## publick key 配置
1、生成一个新的自定义名称的公钥：
```
ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM" -f ~/.ssh/xxx
```
2、copy xxx.pub
```
pbcopy < ~/.ssh/xxx.pub
```

## 提交流程
- 让git版本库追踪到当前文件
```$ git add *```

- 提交到本地版本库 引号里是注释
```$ git commit -m "add something"```

- 这个时候已经提交到本地git版本库了，需要传到github需要推送下
```$ git push origin master```

## 其他命令
 - 修改commit message
 ```
 git commit --amend
 ```
- 切换到远程分支
```
git fetch origin branchname:branchname
git checkout branchname
// or
git checkout origin/atom_static_path -b atom_static_path
```

- [How We Use Commitizen to Clean Up Commit Messages](https://dev.bleacherreport.com/how-we-use-commitizen-to-clean-up-commit-messages-a16790dcd2fd)
- [Git Submodule管理项目子模块](https://www.cnblogs.com/nicksheng/p/6201711.html)
