## 基本操作

- 博客同步

```go
git add -A
git commit -m "更新说明"
git push -u origin main
```

- Res同步到本地

```go
git init
git remote add origin 仓库地址
git pull origin 分支
```

- 分支

```go
git branch 分支 #创建分支
git checkout 分支  #进入分支
git branch -m master main //切换分支
```

  

## 常见错误


- error: src refspec master does not match any

```go
touch README 
git add READM 
git commit –m ’first commit’ 
git push origin master
git branch -m master main //切换分支
```

- fatal: remote origin already exists 

```go
git remote rm origin
```

- git合并分支或者push时，报错：“Please enter a commit message to explain why this merge is necessary,especi”
  
> 关闭重新打开 push

- 删除本地npm包

```yaml
 npm uninstall --save name
```

- hint: Updates were rejected because the tip of your current branch is behind

```bash
git push -u origin main -f
// 强制推送
```

