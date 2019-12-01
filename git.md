#  git命令：

## 1、全局配置

​		主要用来设置用户名和邮箱，建议使用git hub的用户名和邮箱！

```git
$ git config --global user.name "****"  "用户名"
$ git config --global user.name //打印当前用户名
$ git config --global user.email "****"  "邮箱"  
$ git config --global user.email //打印当前用邮箱

```

![image-20191201193407663](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201193407663.png)

![image-20191201193430981](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201193430981.png)

## 2、创建仓库：

### 1）创建空目录：

​		注意！！！：尽量不要在包含中文的目录下创建。

```git
$ mkdir pro_git   //pro_git为文件名
```

​		此时桌面已经创建好了一个项目仓库。

![image-20191201202117276](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201202117276.png)

### 2）进入仓库

​		操作命令：

```git
$ cd pro_git
```

### 3）Git仓库初始化

​		作用是让git知道，它需要管理这个目录，初始化之后点开创建的仓库，点击查看勾选隐藏的项目就可以看到Git的隐藏目录了(建议隐藏)

```git
git init
```

![image-20191201202713209](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201202713209.png)



## 3、Git常用命令

查看当前状态：

```git
git status
```

添加到缓存区：

```git
git add 文件名  //添加单个文件
git add 文件名1 文件名2 文件名3...   //添加多个文件
git add.   //添加当前目录到缓存区中
```

提交至版本库：

```git
git commit -m "注释内容"   //为了自己方便注释一定要写
```

​		提交示例：

![image-20191201205354534](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201205354534.png)

​		修改示例：

![image-20191201205412250](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201205412250.png)

## 4、版本回退步骤



### 	1）查看版本

​		主要是为了确定指令回到的时刻点命令如下：

```git
git log  //显示日志
git log --pretty=oneline
```

​		![image-20191201205955819](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201205955819.png)

解释：commit:编号！（编号可以不用写全，但是至少写前四位！）

​		（HEAD -> master）表示为最新一次提交的

![image-20191201210314747](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201210314747.png)



### 		2）回退操作

```git
git reset --hard "编号"
```

​		结果：

​				此时可以发现我们已经回退了从新查看和文件夹里面都没了index2.php了。



![image-20191201210737904](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201210737904.png)



![image-20191201210747132](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201210747132.png)

![image-20191201210809412](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201210809412.png)



### 		3）回退到回退之前

​			步骤和上面的一样，但是如果用上面的命令已经无法查看到之前的编号，所以需要用下面的命令来查看回退之前的编号。

```git
git reflog
```

![image-20191201211321842](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201211321842.png)

​			***注意此时黄色的七位即为编号***，然后重复上面第二步即可回退。

## 5、远程仓库的操作

###  1）基于http协议

#### 		a. 创建一个空目录

​				名称为shop，进入shop。如下：

![image-20191201213124972](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201213124972.png)

#### 		b. 使用clone指令克隆线上仓库

```git
git clone 线上仓库地址
```

![image-20191201213528649](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201213528649.png)

​			第一个shop是我们创建的仓库，第二个是我们创建的远程仓库

#### 		c. 在仓库上面做对应的操作

​			**提交缓存区-->提交本地仓库-->提交线上仓库-->拉取线上仓库**（前两步省略）

​			**提交到线上仓库指令**

```git
git push
```

​			注意首次使用需要先配置config文件，配置如下***引起来的地方（解决403错误）

```config
[remote "origin"]
	url = https://***用户名:密码@***github.com/liu13137943875/shop.git
	fetch = +refs/heads/*:refs/remotes/origin/*
```

​			设置好之后继续push指令，如下为上次成功：

![image-20191201215247983](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201215247983.png)

​			此时远程仓库已经有了文件

![image-20191201215542481](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201215542481.png)

​		**拉取线上仓库**（保持远程仓库和本地仓库的文件统一，在GitHub上仓库创建一个新文件命名为index.php,此时本地仓库没有这个文件则需要使用拉取线上仓库。）命令：

```git
git pull
```

​		**pull之前**：

![image-20191201215954308](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201215954308.png)

​		**pull之后**：

![image-20191201220019455](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201220019455.png)

​	**上班做git pull，下班做git push。**

### 2）基于SSH协议

​		主要步骤(百度教程很多，这里不多说。)：

#### 		a. 生成客户端公私钥文件

#### 		b. 将公钥上传到GitHub

## 6、分支管理

​		在版本回退的章节，每次提交之后都会有一给分支，Git把他们串成时间线，形成类似于时间轴的东西，这个时间轴就是一个分支，我们称之为master分支。在项目开发中我们会每个人做不同的模块，每个模块部分为一个分支。

![image-20191201221943356](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201221943356.png)

​		分支相关的指令：

```git 
git branch                         //查看分支
git branch 分支名                   //创建分支
git checkout 分支名                 //切换分支
git branch -d 分支名                //删除分支
git merge 被合并的分支名			  //合并分支
git checkout -b                    //新分支可以先创建并切换
```

### 		1）查看分支：

​				**当前分支前面有个*标记**

![image-20191201222828118](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201222828118.png)



### 		2）创建分支：

![image-20191201223248554](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201223248554.png)

### 3）切换分支

![image-20191201230427699](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201230427699.png)

### 4）合并分支

![image-20191201230456720](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201230456720.png)

### 5）删除分支

![image-20191201230506902](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201230506902.png)

​		**总结：其实合并分支前我们给dev分支下面的readme文件添加了一条命令，切换到master分支下面的readme文件并不能看到这一条命令，合并之后才能看到，然后删除dev分支。**

## 7、冲突的产生与解决

### 		1）产生

​					一般原因都是未能及时pull和push，则会产生冲突。即为本地仓库与线上仓库文件内容不同。

### 		2）解决

​					1.先git pull

​					2.打开冲突文件，解决冲突

​					3.需要和提交的另外一个人，看看代码如何保留，重新修改文件，再次提交操作。

## 8、忽略文件

### 1) 介绍:

​		在项目中有很多目录如css、js、imagess。

​		忽略文件需要新建一个名为.gitignore的文件，该文件用于声明忽略文件或者不忽略文件的规则，相对当前目录及其子目录生效。

​	注意：该文件没有文件名字，没办法直接在windows目录下直接创建，可以通过命令行Git Bash 来touch创建。

​	常规写法：

​		/mtk/   //过滤整个文件夹

​		*.zip  //过滤所有.zip文件

​		/mtk/do.c     过滤某个具体文件

​		/index.php   //不过滤具体某个文件

### 2) 案例：



#### a. 在本地新建一个js文件

![image-20191201232419158](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201232419158.png)



#### b. 一次提交本地与线上

![image-20191201232529928](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201232529928.png)



#### c. 新增. touch .gitignore文件并编辑

![image-20191201232934840](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201232934840.png)





#### d. 再次提交本地与线上

![image-20191201233044502](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201233044502.png)



![image-20191201233024201](C:\Users\wuli三岁啊\AppData\Roaming\Typora\typora-user-images\image-20191201233024201.png)



## 9、图形化管理工具（拓展）

​		GItHub for Desktop

​		Soucre tree

​		TortoiseGit

​		Git GUIHere（自带的）
