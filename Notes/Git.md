# Git

标签（空格分隔）： 笔记

---

## 常用语法

Quick setup — if you’ve done this kind of thing before

Get started by creating a new file or uploading an existing file. We recommend every repository include a README, LICENSE, and .gitignore.

…or create a new repository on the command line

```vim
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin [HTTPS]
git push -u origin master
```

…or push an existing repository from the command line

```vim
git remote add origin [HTTPS]
git push -u origin master
```

---

![此处输入图片的描述](http://m.qpic.cn/psc?/V14Pg4Bj4aiM1I/hsnfJ.a5yg7.BhItQyNwPRa5m4dXRS3PKbGapOONdaRCl1Hx0pJ3K.obWhMCrpjNML2IHbC2TjukK5*COD0NDfpNsgCeUlgwRUWaj5CSsd0!/b&bo=awV8AWsFfAEDByI!&rf=viewer_4)

## 一、安装

> Git安装
1、环境变量配置
2、文件缓存

## 二、Git结构

> 1. 本地库
    存储历史版本
> 2. 暂存区
    临时存储（未提交）
> 3. 工作区
    开发区、新建文件库

## 工作区->git add->暂存区-> git commit -> 本地库

---

## 三、Git和代码托管中心

Github是Git的代码托管中心（远程库）
> 局域网
>
>* GitLab服务器
>
> 外网
>
>* github
>* 马云

## 四、 远程库协作协作协作协作协作

>* 团队内协作
![此处输入图片的描述](https://gitee.com/KawYang/Notes/blob/master/Image/Git%E5%9B%A2%E9%98%9F%E5%90%88%E4%BD%9C.png)
>* 跨团队协作
![此处输入图片的描述](http://m.qpic.cn/psc?/V14Pg4Bj4aiM1I/hsnfJ.a5yg7.BhItQyNwPeCnLEaSDHt.J038u0BOLPNbvCjE5xkT5gp8dpT34K6534K.HtID0bKjVVMk1yrEjNVh0WQLIAkUmnphl1s8Qn4!/b&bo=gwVnAwAAAAADN*A!&rf=viewer_4)

## 五、Git命令行操作

### 一、 本地库初始化(创建本地库)

>* 命令： Git add
>* 效果：
>* 注意：.git/ 目录中存放的是本地库相关的子目录和文件，不要删除，也不要修改。

### 二、设置签名

形式

>* 用户名：Tom
>* Email地址：hello@qq.com
>* 作用：区分不同开发人员
>
>>辨析： 设置的签名和登录远程库(代码托管中心)的账号、密码没有任何关系。
>> 命令：
git config user.name tome
git config user.email hello@qq.com
>> 项目级别/仓库级别：仅对当前本地库范围内生效
>>
>* git config --global user.name tome
>* git config --global user.email hello@qq.com
>>
>>* 系统用户级别：登录当前操作系统用户范围
>>* 级别优先级：
>>* 就近原则：如果两个签名都设置，二者取项目级别
>
>* 如果只有系统级别的签名，就一系统用户级别的签名为准
>* 必须有一个
信息保存到当前项目目录下的 .git/config  内

---

## 六、基本操作

### 1)状态查看

>* git status： 查看工作区、暂存区的状态
>未追踪

### 2)添加操作

>* git add [filename] : 工作区的新建或修改添加到暂存区）

### 3)提交操作

>* git commit -m "commit massage " [filename] （将暂存区的内容提交到本地库）

### 修改的文件可以直接提交`commit`不add, 这样就不能够撤销了

## 七、git status (参数)

stuatus 状态
On branch master： 位于主干  
No commits yet :  本地库没有  
nothing to commit (create/copy files and use "git add" to track)： 暂存库没有可提交的  

git commit : 提交从缓存区提交到本地

## git commit

## 八、版本的前进和后退

>查看历史记录
>
>* git log (--pretty==oneline/ --oneline )

```vim
Mac@macdeMacBook-Air:~/Git/Test$ git log --oneline
676e03f (HEAD -> master) my first modify
f11d016 my first modify code
f346569 my first commit
3f5b94f my second commit
a5143ed my first code
```

### git reflog

```vim
Mac@macdeMacBook-Air:~/Git/Test$ git reflog
676e03f (HEAD -> master) HEAD@{0}: commit: my first modify
f11d016 HEAD@{1}: commit: my first modify code
f346569 HEAD@{2}: commit: my first commit
3f5b94f HEAD@{3}: commit: my second commit
a5143ed HEAD@{4}: commit (initial): my first code
```

### 当前版本移动到该版本需要几步

>* 多屏显示
>* 空格向下 / B向上翻页 / Q退出

### 前进后退

>* 基于`索引值`【推荐】
>
>>git reset --head [索引值（长的）`a5143ed`]
>
>* 基于`^`符号(只能往后)
>
>>git reset --hard HEAD^^^^^
>
>* 基于`~`符号(也是只能后退)
> $ git reset --head HEAD~3

### reset 命令三个参数对比

```vim
reset hard --soft [版本号]
        --soft //只在本地库移动HEAD指针
           Does not touch the index file or the working tree at all (but resets
           the head to <commit>, just like all modes do). This leaves all your
           changed files "Changes to be committed", as git status would put it.

reset hard --mixed [版本号]
       --mixed //在本地库移动指针、重置暂存区
           Resets the index but not the working tree (i.e., the changed files are
           preserved but not marked for commit) and reports what has not been
           updated. This is the default action.

           If -N is specified, removed paths are marked as intent-to-add (see
           git-add(1)).
reset hard --hard [版本号]
       --hard //在本地库移动指针、重置暂存区、重置工作区
           Resets the index and working tree. Any changes to tracked files in the
           working tree since <commit> are discarded.
```

---

>* 添加到暂存区
>
>>* 删除文件并找回
>>
>>* 提交到本地库的文件删除
>>
>>>* 前提：删除前已经提交到本地库
>>>
>>>>* 操作：git reset --hard [指针位置]（HEAD）（已经提交到本地库的位置）

### 比较文件差异

git diff [filename]

>* git diff [filename]  :工作区与暂存区对应文件比较
>* git diff [本地库某版本] [filename] :工作区与本地库文件对比
>* git diff [本地库某版本] ：不加文件名进行多个文件比较

## 4.4 分支管理

### 4.4.1

&emsp;在版本控制过程中，使用多条线同时推进多个任务。  
&emsp;开发过程中彼此独立。

master（主干分支）

>* feature_blue(feature 开头)(从主干分支复制而来)  
（完成后进行合并）(大版本更新)->主干出现bug（创建新分支） ->hot_fix(热修复)（服务器依然进行）「冷修复」
>
>>* feature_game

### 4.4.2 分支操作

> 创建分支
>
>>* git branch [分支名]
>
> 查看分支
>
>>* git branch -v
>
> 切换分支
>
>>* git checkout [分支名]
>
> 合并分支
>
>>* 第一步：切换到接受修改的分支上:git checkout [被合并的分支名]（提交到本地库）
>>
>>* 第二步: 执行merge命令（在主分支）？？？？ git merge [有新东西的分支名]
>>* 解决冲突
>>
>>>* hot_fix
>>>* master
>>> 在同一行进行修改  hot_fix -> master 进行合并

```vim
for (int i=0;i<n;i++){
<<<<<<< HEAD
    cout<<"i"<<endl;
=======                     (当前版本的内容)
    cout<<"i"<<" ";
>>>>>>> master              （master修改的内容）
}
```

#### 手动修改3

git status  
git add [filename] (添加到缓存区)  
git commit -m "合并" (完成合并、不带文件名)

> 1.编辑文件，删除特殊符号
> 2.把文件修改到满意的程度，保存并退出
> 3.git add [filename]
> 4.git commit -m "日志信息"  

## Git  基本原理

### 1.hash（加密算法）明文 --> hash -->密文

### 2.文件校验

## 机制

> 1.集中式版本控制工具SVN（增量式版本控制）
> 2. Git 快照 （快照流）重复的用指针指向同一个文件
提交对象（哈希值 -> tree）
---
