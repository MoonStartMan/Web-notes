# github 版本回退

## 查询历史对应不同版本的ID

```
git log --pretty=oneline
```

## 恢复到历史版本

```
git reset --hard 版本号
```

## 把修改推到远程服务器

```
git push -f -u origin master
```