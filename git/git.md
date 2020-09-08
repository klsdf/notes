# GIT简介

# GIT基础

# 连接GitHub流程

## 0. 配置

### 在GitHub建立项目

<img src="img/image-20200903203620344.png" alt="image-20200903203620344" style="zoom:50%;" />

之后右上角可以找到你的项目

<img src="img/image-20200903203756199.png" alt="image-20200903203756199" style="zoom:67%;" />

### 配置ssh



## 1.在本地创建仓库

```shell
git init
```

## 2.把工作内容添加入暂存区

```shell
git add *
```

## 3.把暂存区内容推入本地数据仓库

```shell
git commit -m "代码提交信息"
```

## 4.连接远程服务器

若之前这个本地仓库已经连接过这个服务器,可以跳过这条.

```shell
git remote add origin git@github.com:michaelliao/learngit.git
```

注意!!!后面那串github的地址并不是固定的,需要根据你在github上面的项目决定.

<img src="img/image-20200903203857960.png" alt="image-20200903203857960" style="zoom: 80%;" />

## 5.把本地仓库的数据推入远程仓库

若你第一次提交这个项目,请用下面的代码

```shell
git push -u origin master
```

若不是第一次,可以用下面的代码

```shell
git push
```



# 常见错误

```
! [rejected] master -> master (fetch first) error: failed to push some refs to ' 。。。'
```

出现这个问题是因为github中的README.md文件不在本地代码目录中，可以通过如下命令进行代码合并

```shell
git pull --rebase origin master
```

# 2020/8/26