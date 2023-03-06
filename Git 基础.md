# Git 基础



## 一.安装并配置 git

### 1.下载安装

> 安装地址:
>
> [Git - Downloading Package (git-scm.com)](https://git-scm.com/download/win)

<img src="https://s2.loli.net/2023/03/05/tvNRIOhdA6na21y.png" alt="image-20230304144816871" style="zoom:50%;" />

> 选择自己电脑对应的版本下载安装即可（傻瓜式安装）



### 2.配置用户信息

安装完成Git之后，要做的第一件事就是设置自己的**用户名**和**邮件地址**。因为通过Git对项目进行版本管理的时候，Git需要使用这些基本信息，来记录是谁对项目进行了操作：

```bash
# 配置用户名
git config --global user.name "用户名"

# 配置邮件地址
git config --global user.email "邮件地址"

```

> **注意：**如果使用了  *--global*  选项，那么该命令只需要运行一次，即可永久生效。



### 3.检查配置信息

> 使用终端命令，快速的查看 git 的全局配置信息：

```bash
# 查看所有的全局配置项
git config --list --global

# 查看指定的全局配置项
git config user.name
git config user.email
```



### 4.获取帮助信息

> 可以使用 **git config <verb>** 命令，无需联网即可在浏览器中打开帮助手册

```bash
# 要想打开 git config 命令的帮助手册
git help config
```

<img src="https://s2.loli.net/2023/03/05/uRJV2GxiMlqDrAF.png" alt="image-20230304151138262" style="zoom:50%;" />

> 如果不想查看完整的手册，那么可以使用 **-h** 选项获得更简明的 “help” 输出

```bash
# 想要获取 git config 命令的快速参考
git config -h
```

<img src="https://s2.loli.net/2023/03/05/nVTc6qsL3iYol9Z.png" alt="image-20230304151543812"  />



## 二.git 的基本操作

### 1.获取 git 仓库的两种方式

> 1. 将尚未进行版本控制的**本地目录*转换*为 git 仓库**
> 2. 从其他服务器**克隆**一个已经存在的 git 仓库



### 2.在现有目录中初始化仓库

如果自己有一个尚未进行版本控制的项目目录，想要用 git 来控制它，需要执行以下两个步骤：

> 1. 在项目目录中，通过鼠标右键打开 "Git Bash"
>
> 2. 执行 [**git init**]() 命令将当前的目录转化为 git 仓库
>
>    git init 命令会创建一个名为 .git 的隐藏目录，这个 .git 目录就是当前项目的 git 仓库，里面包含了初始化的必要文件，这些文件是 git 仓库的必要组成部分

![image-20230304153523240](https://s2.loli.net/2023/03/05/mYt7laKMdWq4wD3.png)



### 3.工作区中文件的四种状态

工作区中的每一个文件可能有4种状态，这四种状态共分为两大类

> - 未被 git 管理：
>
>   ​	未跟踪（Untracked）不被 git 所管理的文件
>
> - 已被 git 管理
>
>   ​	未修改（Unmodified）工作区中文件的内容和 git 仓库中文件的内容**保持一致**
>
>   ​	已修改（Modified）工作区中文件的内容和 git 仓库中文件的内容**不一致**
>
>   ​	已暂存（Staged）工作区中的文件已被放到暂存区，准备将修改后的文件保存到 git 仓库中

git 操作的终极结果：让工作区中的文件都处于"**未修改**"的状态。



### 4.检查文件的状态

可以使用以下命令来查看文件处于什么状态

`git status`

![image-20230304160100871](https://s2.loli.net/2023/03/05/5W94dDU6acnsqxP.png)

在状态报告中可以看到新建的文件出现在**Untracked files（未被跟踪的文件）**下面。

未跟踪的文件意味着 git 在之前的快照中没有这些文件；git 不会自动将其纳入跟踪范围，除非明确的告诉它 “我们需要使用 git 跟踪管理该文件”

> 以精简的方式显示文件状态

使用 `git status`输出的状态报告很详细，但有些繁琐。如果希望**以精简的方式显示文件状态**，可以使用以下两条完全等价的命令

```bash
# 以精简的方式显示文件状态
git status -s  # -s 是 --short 的简写形式
git status -short
```

![image-20230304160659355](https://s2.loli.net/2023/03/05/QoAZ5sJhyOSqdpC.png)



### 5.跟踪新文件

使用命令 `git add`开始跟踪一个文件

![image-20230304161526999](https://s2.loli.net/2023/03/05/zckOLy2pjIgHdQl.png)

此时再运行`git status -s`命令，会看到文件在**Changes to be committed:**这行的下面，说明已经被跟踪，并处于暂存状态，且文件前面会有**绿色的A标记**

![image-20230304161543681](https://s2.loli.net/2023/03/05/1DfQKPmvonpqhxN.png)

![image-20230304161611742](https://s2.loli.net/2023/03/05/BiSxsjXGpOZE5rl.png)



### 6.提交更新

现在暂存区中有一个文件等待被提交到 git 仓库中进行保存。可以执行`git commit` 命令进行提交，其中`-m`选项后面是本次的**提交消息**，用来<u>对提交的内容做进一步的描述</u>：

```bash
git commit -m "新建了文件"
```

提交成功后，会显示如下信息：

![image-20230304163130712](https://s2.loli.net/2023/03/05/BRiS6QyunqWKkH8.png)

提交成功后，再次检查文件的状态，得到提示如下：

![image-20230304163258012](https://s2.loli.net/2023/03/05/4JEz8dAMfQSPlIh.png)

此时工作区中已经没有了**README.md**文件。



### 7.对已提交的文件进行修改

目前，**README.md**文件已经被 git 跟踪，并且，工作区和 git 仓库中的 **README.md**文件内容保持一致。当我们修改了工作区中**README.md**文件内容后，再次运行`git status`和`git status -s`命令，会看到如下的内容：

![image-20230304164251416](https://s2.loli.net/2023/03/05/8glILGnTV5O3BR7.png)

![image-20230304164322972](https://s2.loli.net/2023/03/05/LZqXf2Em8aNyguI.png)

文件 **README.md** 出现在 <u>Changes not staged for commit:</u> 这行下面，说明已跟踪的文件的内容发生了变化，但还没有放到暂存区。

> 修改过的、没有放到暂存区的文件前面有**==红色的M==**标记
>
> 

### 8.暂存已修改的文件

目前，工作区中的**README.md**文件已被修改，如果要暂存这次修改，需要再次运行`git add`命令，这个命令是个多功能的命令，主要有三个功效：

> 1. 可以用它开始跟踪新文件
> 2. 把已跟踪的、且已经修改的文件放到暂存区
> 3. 把有冲突的文件标记为已解决状态

![image-20230304165456786](https://s2.loli.net/2023/03/05/m13GvpJXrgI9FHn.png)

![image-20230304165511884](https://s2.loli.net/2023/03/05/27eQfsvunUKJCqG.png)

![image-20230304165536667](https://s2.loli.net/2023/03/05/svAdx75USw3Ezat.png)



### 9.提交已暂存的文件

再次运行`git commit -m "提交消息"`命令，即可将暂存区中记录的**README.md**文件的快照，提交到 git 仓库中进行保存

![image-20230304165848985](https://s2.loli.net/2023/03/05/U8fiH9jTd4G6Ltu.png)



### 10.撤销对文件的修改

撤销对文件的修改指的是：把工作区中对应文件的修改，还原成 git 仓库所保存的版本。

操作的结果：所有的修改会丢失，且无法恢复！==危险性比较高，请谨慎操作==

```bash
git checkout -- README.md
```



### 11.向暂存区中一次性添加多个文件

如果需要被暂存的文件个数比较多，可以使用如下的命令，一次性将所有的新增和修改过的文件加入暂存区：

```bash
git add .
```

==在开发过程中，会经常使用这个命令，将新增和修改过的文件加入暂存区==



### 12.取消暂存文件

如果需要从暂存区中移除对应的文件，可以使用如下的命令：

```bash
git reset HEAD 要移除的文件名称

# 一次性移除多个文件
git reset HEAD .
```



### 13.跳过使用暂存区

git 标准的工作流程是==工作区== --> ==暂存区== --> ==git 仓库==，但是有时候这么做有些繁琐，此时可以跳过暂存区，直接将工作区中的修改提交的 git 仓库，这时候 git 工作的流程简化为了==工作区== --> ==git 仓库==。



git 提供了一个跳过使用暂存区的方式，只要在提交的时候，给 `git commit`加上`-a`选项，git 就会自动把已经跟踪过的文件暂存起来一并提交，从而跳过 `git add`步骤：

```bash
git commit -a -m "描述信息"
```

![image-20230304204049803](https://s2.loli.net/2023/03/05/ul5JTLpRcZy3GgC.png)

![image-20230304204226564](https://s2.loli.net/2023/03/05/iQO4nDJc8MLz3qw.png)



### 14.移除文件

从 git 仓库中移除文件的方式有两种：

> 1. 从 git 仓库和工作区中==同时移除==对应的文件
> 2. 只从 git 仓库中移除指定的文件，但保留工作区中对应的文件

```bash
# 从 git 仓库和工作区中同时移除 index.html
git rm -f index.html

# 只从 git 仓库中移除 index.html ，但保留工作区中的 inndex.html 文件
git rm --cached index.html
```



### 15.忽略文件

一般情况下总会有些文件无需纳入 git 的管理，也不希望它们总出现在未跟踪文件列表。这种情况下，我们可以创建一个名为==.gitignore==的配置文件，列出要忽略的文件的匹配模式。

> ==.gitignore== 的格式规范如下：
>
> ​		1.以 ==#开头==的是注释
>
> ​		2.以 ==/结尾==的是目录
>
> ​		3.以 ==/开头==防止递归
>
> ​		4.以 ==！开头==表示取反
>
> ​		5.可以使用==glob 模式==进行文件和文件夹的匹配（glob指简化的正则表达式）

所谓的==glob 模式==是指简化的正则表达式：

1. ==星号 *== 匹配零个或多个任意字符
2. ==[abc]== 匹配任何一个列在方括号中的字符
3. ==问号 ？==只匹配一个任意字符
4. 在方括号里使用==短划线==分隔两个字符，表示所有在这两个字符范围内的都可以匹配
5. ==两个星号 **== 表示匹配任意中间目录



### 16.查看提交历史

如果希望回顾项目的提交历史，可以使用 `git log`这个简单且有效的命令。

```bash
# 按时间先后顺序列出所有的提交历史，最近的提交排在最上面
git log

# 只展示最新的两条提交历史，数字可以按需要进行填写
git log -2

# 在一行上展示最近两条提交历史的信息
git log -2 --pretty=oneline

# 在一行上展示最近两条提交历史的信息，并且自定义输出的格式
# %h 提交的简写哈希值  %an 作者名字  %ar 作者修订日期，按照多久以前的方式展示
# %s 提交说明
git log -2 --pretty=format:"%h | %an | %ar | %s"
```



### 17.回退到指定的版本

```bash
# 在一行上展示所有的提交历史
git log --pretty=oneline

# 使用 git reset --hard 命令，根据指定的提交 ID 回退到指定的版本
git reset --hard <CommitID>

# 在旧版本中查看命令操作的历史
git reflog --pretty=oneline

# 再次根据最新的提交 ID，跳转到最新的版本
git reset --hard <CommitID>
```



## 三.小结

1. 初始化 git 仓库的命令 `git init`
2. 查看文件状态的命令  `git status` 或 `git status -s`
3. 一次性将文件加入暂存区的命令  `git add .`
4. 将暂存区的文件提交到 git仓库的命令  `git commit -m "提交消息"`







# Github 基础

## 一.了解开源

### 1.什么是开源？

1. 概念：开源即开放源代码
2. 基本含义：代码是公开的
3. 特点：任何人都可以去==查看==，==修改==和==使用==开源代码

通俗的理解：开源是指不仅提供程序还提供程序的源代码



### 2.什么是开源许可协议

开源并不意味着完全没有限制，为了==限制使用者的使用范围==和==保护作者的权力==，每个开源项目都应该遵守==开源许可协议==。

> 常见的5种开源许可协议
>
> 1. BSD  (Berkeley Software Distribution)
> 2. Apache Licence 2.0
> 3. ==GPL== (GNU General Public License)
> 4. LGPL (GNU Lesser General Public License)
> 5. ==MIT== (Massachusetts Institute of Technology ,MIT)



### 3.开源项目托管平台

专门用于免费存放开源项目源代码的网站，叫做==开源项目托管平台==。目前世界上比较出名的开源项目托管平台主要有以下3个：

> - Github (全球最牛的开源项目托管平台，没有之一)
> - Gitlab (对代码私有性支持较好，因此企业用户较多)
> - Gitee (又叫做码云，是国产的开源项目托管平台。访问速度快，纯中文界面，使用友好)

==注意==：以上3个开源项目托管平台，只能托管以 Git 管理的项目源代码，因此，它们的名字都以 Git 开头。





## 二.Github 基础

### 1. 什么是 Github

Github 是全球最大的开源项目托管平台。因此只支持 Git 作为唯一的版本控制工具，故名 Github。

在 Github 中，你可以：

>1. 关注自己喜欢的开源项目，为其点赞打 call
>2. 为自己喜欢的开源项目做贡献 （Pull Request）
>3. 和开源项目的作者讨论 BUG 和提需求 （lssues）
>4. 把喜欢的项目复制一份作为自己的项目进行修改 （Fork）
>5. 创建属于自己的项目
>6. ······

> 网址： https://github.com/



### 2.注册 Github 账号的流程

1. 访问 Github 的官网首页   https://github.com/
1. 点击 ”Sign up“ 按钮跳转到注册页面
1. 填写可用的用户名、邮箱、密码
1. 通过点击箭头的形式，将验证图片摆正
1. 点击 ”Create account“ 按钮注册新用户
1. 登录到第3步填写的邮件中，点击激活链接，完成注册



### 3.新建空白远程仓库

1、

![image-20230305150028258](https://s2.loli.net/2023/03/05/Ml6EnubrYQXkpFC.png)



2、

![image-20230305150243145](https://s2.loli.net/2023/03/05/p9GQY6dzNmVOChJ.png)



3、

![image-20230305150447673](https://s2.loli.net/2023/03/05/8tjeKxwc1yhXnUJ.png)



4、

![image-20230305150706339](https://s2.loli.net/2023/03/05/pMfYBaONFWiZLHq.png)





### 4.远程仓库的两种访问方式

Github 上的远程仓库，有两种访问方式，分别是 ==HTTPS== 和 ==SSH== 。它们的区别是：

> 1. HTTPS: ==零配置==；但是每次访问仓库时，需要重复输入 Github 的账号和密码才能访问成功
> 2. SSH: ==需要进行额外的配置==；但是成功后，每次访问仓库时，不需要重复输入 Github 的账号和密码（==推荐使用==）



### 5.SSH key

SSH key 的作用：实现本地仓库和 Github 之间的免登录的加密数据传输。

SSH key 的好处：免登录身份认证、数据加密传输。

SSH key 由两部分组成，分别是：

1. id_rsa （私钥文件，存放于客户端的电脑中即可）
2. id_rsa.pub   （公钥文件，需要配置到 Github 中）



### 6.生成 SSH key

1. 打开 Git Bash

2. 粘贴如下的命令，并将邮箱地址替换为注册 Github 账号时填写的邮箱：

   ```bash
   ssh-keygen -t rsa -b 4096 -C "邮箱地址"
   ```

3. 连续敲击三次回车，即可在==C:\User\用户名文件夹\.ssh== 目录中生成 id_rsa 和 id_rsa.pub

![image-20230305153506711](https://s2.loli.net/2023/03/05/CvwgJaAtQc9G8Iy.png)





### 7.配置 SSH key

1. 使用记事本打开 id_rsa.pub 文件，复制里面的内容
2. 在浏览器中登录 Github，==点击头像== --> ==Setting== --> ==SSH and GPG Keys== --> ==New SSH key==
3. 将 id_rsa.pub 文件中的内容粘贴到 ==Key== 对应的文本框中
4. 在 Title 文本框中任意填写一个名称，来标识这个 Key 从何而来

![image-20230305154404575](https://s2.loli.net/2023/03/05/GxZ36lWyPBIHL9J.png)





### 8.检测 Github 的 SSH key 是否配置成功

打开 Git Bash ，输入以下命令并回车执行：

```bash
ssh -T git@github.com
```

上述命令成功后，可能看到如下信息：

![image-20230305155125180](https://s2.loli.net/2023/03/05/ChmfVMjlqQRtPXd.png)

输入 yes 后看到下面的提示信息说明已经配置成功了。



### 9.基于 SSH 将本地仓库上传到 Github

![image-20230305150706339](https://s2.loli.net/2023/03/05/pMfYBaONFWiZLHq.png)

打开 Git Bash，复制代码。



### 10.将远程仓库克隆到本地

打开 Git Bash ，输入以下命令并回车执行：

```bash
git clone 远程仓库的地址
```

![image-20230305165503396](https://s2.loli.net/2023/03/05/BJWswbvuXN6SaEd.png)





## 三. 本地分支操作

### 1. 分支的概念

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习 Git 的时候，另一个你正在另一个平行宇宙里努力学习 Web.

如果两个平行宇宙互不干扰，那对现在的你也就没啥影响。

不过，在某个时间点，两个平行宇宙合并了，结果，你两个知识就都学会了。



### 2. 分支在实际开发中的作用

在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发。



### 3. master 主分支

在初始化本地 Git 仓库的时候，Git 默认已经帮我们创建了一个名字叫做 ==master== 的分支。通常情况下我们把 master 分支叫做==主分支==。

在实际工作中，master 主分支的作用是：==用来保存和记录整个项目已完成的功能代码==。

也因此，不允许程序员直接在 master 分支上修改代码，因为这样做风险太高，容易导致整个项目崩溃。



### 4. 功能分支

由于程序员不能在 master 分支上进行功能的开发，所以就有了功能分支的概念。

==功能分支==指的是专门用来开发新功能的分支，它是临时从 master 主分支分叉出来的，当新功能开发且测试完毕后，最终合并到master主分支上。



### 5. 查看分支列表

使用如下命令，可以查看当前Git仓库中所有的分支列表：

```bash
git branch
```

<img src="https://s2.loli.net/2023/03/06/rH36Cm9ZNTRvxVE.png" alt="image-20230306100925915" style="zoom:50%;" />

> ==*== 表示当前所处的分支



### 6. 创建新分支

使用如下的命令，就可以基于当前分支，创建一个新的分支，此时，新分支中的代码就和当前分支完全一样：

```bash
git branch 分支名称
```

![image-20230306101548083](https://s2.loli.net/2023/03/06/NL56dJIYwapSRkF.png)



### 7. 切换分支

使用如下的命令，可以切换到指定的分支上进行开发：

```bash
git checkout test
```

![image-20230306101839831](https://s2.loli.net/2023/03/06/r1gfVecwSEYXFs2.png)



### 8. 分支的快速创建和切换

使用如下的命令，可以创建指定名称的新分支，并立即切换到新分支上：

```bash
# -b 表示创建一个新分支
#  checkout 表示切换到刚才新建的分支上
git checkout -b 分支名称
```

![image-20230306102517228](https://s2.loli.net/2023/03/06/6IM48SNEjODWh7l.png)



### 9.合并分支

功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到 master 主分支上：

```bash
# 1. 切换到 master 分支
git checkout master
# 2. 在 master 分支上运行以下命令，将 test 分支的代码合并到 master 中
git merge test
```

![image-20230306103445469](https://s2.loli.net/2023/03/06/juBJHTfsa4w6orZ.png)



### 10. 删除分支

当功能分支的代码合并到 master 主分支上以后，就可以使用以下的命令，删除对应的功能分支：

```bash
git branch -d 分支名称
```

![image-20230306103837113](https://s2.loli.net/2023/03/06/P4hwgSq7lMVLkAb.png)



### 11. 遇到冲突时的合并分支

如果在两个不同的分支中，对同一个文件进行了不同的修改，Git 就没法干净的合并它们。此时，我们需要打开这些包含冲突的文件然后手动解决冲突。

```bash
# 假设：在把 reg 分支合并到 master 分支期间，代码发生了冲突
git checkout master
git merge reg

# 打开包含冲突的文件，手动解决冲突后，再执行以下命令
git add .
git commit -m "描述信息"
```



## 四. 远程分支操作

### 1. 将本地分支推送到远程仓库

如果是第一次将本地分支推送到远程仓库，需要运行如下命令：

```bash
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例
git push -u origin payment:pay

# 如果希望将远程分支的名称和本地分支的名称保持一致，可以对命令进行简化：
git push -u origin payment
```

<img src="https://s2.loli.net/2023/03/06/6UgR1rXwvEjIPMC.png" alt="image-20230306110141957" style="zoom:50%;" />





### 2. 查看远程仓库中的所有分支列表

通过如下的命令，可以查看远程仓库中，所有的分支列表的信息：

```bash
git remote show 远程仓库名
```

![image-20230306124212730](https://s2.loli.net/2023/03/06/Pe1rjd4FUaKz6pw.png)



### 3. 跟踪分支

跟踪分支指的是：从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下：

```bash
# 从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名字相同
git checkout 远程分支的名称

# 实例：
git checkout pay

# 从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
git checkout -b 本地分支名称 远程仓库名称/远程分支名称

# 实例：
git checkout -b payment origin/pay
```



### 4. 拉取远程分支的最新代码

可以使用如下的命令，把远程分支最新的代码下载到本地对应的仓库中：

```bash
# 从远程仓库拉取当前分支最新的代码，保持当前分支的代码和远程分支代码一致
git pull
```



### 5. 删除远程分支

可以使用如下的命令，删除远程仓库中指定的分支：

```bash
# 删除远程仓库中指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称
#实例：
git push origin --delete pay
```

![image-20230306130520264](https://s2.loli.net/2023/03/06/FbI7i2wrCq8dhOf.png)



# 总结

**掌握 Git 基本命令的使用**

- git init
- git add .
- git commit -m "提交信息"
- git status 和 git status -s

**使用 Github 创建和维护远程仓库**

- 配置 Github 的SSH访问
- 能够将本地仓库上传到 Github

**掌握 Git 分支的基本使用**

- git checkout -b 新分支名称
- git push -u origin 新分支名称
- git checkout 分支名称
- git branch
