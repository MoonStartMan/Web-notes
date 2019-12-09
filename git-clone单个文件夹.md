# git-clone单个文件夹

## 创建一个本地空仓库

``` git
mkdir project_folder
cd project_folder
git init
git remote add -f origin <url>
```

PS: url为git地址

## 在Config中允许Sparse Checkout模式：

```
git config core.sparsecheckout true
```

## 输入需要clone的文件夹的名字

``` git
echo “real-world” >> .git/info/sparse-checkout
```

PS: real-world就是文件夹的名字

## 最后拉取代码

``` git
git pull origin master
```