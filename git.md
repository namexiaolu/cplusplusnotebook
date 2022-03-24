## git 基本用法

![image-20220322110344641](git.assets/image-20220322110344641-16480908888891.png)

### 本地什么都没有，远程有的话

1. git clone 地址   将远程库的东西搞下来
2. 更改文件内容
3. git add <文件> 将文件增加到暂存区  可以用git add . 将所有文件都提交到暂存区
4. git commit -m “这里写提交的备注”   将暂存区的内容提交到本地仓库
5. git push 提交到远程仓库

## 之后修改的时候

git pull 就可以

## 遇到冲突

当我们在本地改一个文件的的某一行的时候，这个文件的这一行碰巧被别人修改了。此时会出现冲突。

现象就是：当我们正常提交到远程的时候他会报错<img src="git.assets/image-20220323091928516-16480908888902.png" alt="image-20220323091928516" style="zoom:200%;" />



这时候我们需要从远端把最新代码pull下来

![image-20220323092243830](git.assets/image-20220323092243830-16480908888903.png)

他会告诉我们 这个文件有冲突，我们需要把这个文件修改一下。

打开冲突的文件是这样的![image-20220323092428902](git.assets/image-20220323092428902-16480908888904.png)

我习惯用vscode修改：

![image-20220323092448760](git.assets/image-20220323092448760-16480908888905.png)

改完之后 正常 add commit push 即可。

## 分支

### 远程有分支本地没有

```undefined
1.将某个远程主机的更新，全部取回本地：git fetch

2.查看远程分支：git branch -a

3.拉取远程分支到本地：git checkout -b 远程分支名 origin/远程分支名
```

### 本地新建分支，远程仓库没有

1. 创建分支并切换到该分支
     git checkout -b 新分支名
2. 创建分支，但不切换
     git branch 新分支名
3. 将创建的分支关联远程仓库
   	git push --set-upstream origin 分支名

## 子模块 submodule

参考：https://www.jianshu.com/p/9000cd49822c

### 添加子模块

此文中统一将远程项目`https://github.com/maonx/vimwiki-assets.git`克隆到本地`assets`文件夹。

```sh
$ git submodule add https://github.com/maonx/vimwiki-assets.git assets
```

### 克隆包含子模块的项目

1. 克隆父项目

```sh
$ git clone https://github.com/maonx/vimwiki-assets.git assets
```

1. 查看子模块

```sh
$ git submodule
 -e33f854d3f51f5ebd771a68da05ad0371a3c0570 assets
```

子模块前面有一个`-`，说明子模块文件还未检入（空文件夹）。

1. 初始化子模块

```sh
$ git submodule init
Submodule 'assets' (https://github.com/maonx/vimwiki-assets.git) registered for path 'assets'
```

初始化模块只需在克隆父项目后运行一次。

1. 更新子模块

```sh
$ git submodule update
Cloning into 'assets'...
remote: Counting objects: 151, done.
remote: Compressing objects: 100% (80/80), done.
remote: Total 151 (delta 18), reused 0 (delta 0), pack-reused 70
Receiving objects: 100% (151/151), 1.34 MiB | 569.00 KiB/s, done.
Resolving deltas: 100% (36/36), done.
Checking connectivity... done.
Submodule path 'assets': checked out 'e33f854d3f51f5ebd771a68da05ad0371a3c0570'
```



### 或者一步到位

### 递归克隆整个项目

```sh
git clone https://github.com/maonx/vimwiki-assets.git assets --recursive 
```

递归克隆整个项目，子模块已经同时更新了，一步到位。

 ### 更新子模块

进入到子模块目录中，正常add commit push即可、
