# git取消本地commit以及修改git url

## git 取消本地的commit

``` git
git reset HEAD~1
```

## git 修改url


### 列出remotes

``` git
xxxxxx@xxxxxx:~/workspace/goal$ git remote -v
origin    git@github.com:xxxxxx/SpringBoot.git (fetch)
origin    git@github.com:xxxxxx/SpringBoot.git (push)
```

### 使用git remote set-url命令从SSH到HTTPS的远程URL

``` git
xxxxxx@xxxxxx:~/workspace/goal$ git remote set-url origin https://github.com/xxxxxx/SpringBoot.git
```

### 验证是否改变成功

``` git
xxxxxx@xxxxxx:~/workspace/goal$ git remote -v
origin    https://github.com:xxxxxx/SpringBoot.git (fetch)
origin    https://github.com:xxxxxx/SpringBoot.git (push)

```