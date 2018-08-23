#代码仓库管理及维护说明	

##1.基础使用
大家都知道gitlab是一个仓库管理系统,使用git作为代码管理工具。我们操作代码时，一般会有两种方式：cmd和IDE.

### a.cmd
即我们通过gitbash提供的命令来维护我们的代码.基本上我们在开发过程中常用的option如下：

    git init //初始化本地仓库
    git clone //拉取远程仓库
    
    git pull   //拉取远程最新代码
    git status //查看代码仓库文件状态
    git add    //添加修改文件
    git commit //提交本地修改到仓库
    git push   //推送本地仓库的修改
    
    git branch   //查看分支状态
    git checkout //检出，可以撤销修改及切换分支等 
    git diff		//对比文件差异
    
  查看官方的使用说明文档请点[这里](https://git-scm.com/book/zh/v2)
  
### b.IDE
如果你对git cmd不是很熟悉，或者不喜欢cmd的使用方式，那么我们建议你使用IDE来做代码管理。常用的IDE有SourceTree、GitHub for Desktop等。这里建议大家用SourceTree,用户体验好一点。页面如下图:  
![avatar](https://raw.githubusercontent.com/zhouzhongbo/ImgStore/master/sourcetree.png)


##2.gitlab管理
gitlab登录后的页面呈现如下:  
![gitlab](https://raw.githubusercontent.com/zhouzhongbo/ImgStore/master/gitlab.png)

### a.组织形式管理
gitlab中有两种组织形式：Person 和 Group。通常，我们为项目组或者部门创建Group。以我们的部门举例，我们会为市场及浅言项目组创建 DroiMarket 和 MarksMan 两个Group。在DroiMarket Group中，我们为卓易市场App 以及还在维护的SDK分别创建了Project，如下图:  
![group_project](https://raw.githubusercontent.com/zhouzhongbo/ImgStore/master/group_project.png)  

在Group中，我们通过配置group->member和 project->member来做权限控制。  
一般我们会把自己编写的小功能或者学习练手用的项目放置在个人目录下。

### b.项目分支管理
一个项目下可能会有多个分支,合理的创建管理分支可以提高我们的开发效率。一个项目会有以下几个常见的分支：

1）master :开发初期(未release)，可以直接在此分支上做代码开发；一旦发版后，不允许开发直接提交代码到此分支，只能从develop分支merge功能点及修复点。发版以后要确保master分支上每一个节点都是可编译通过的。每一次的正式发版都应该是在此分支上，且每一次发版应该打Tag。

2) develop :应用release之后，应该从release版本检出develop分支。后续的开发及debug应该在此分支及个人拉出的功能分支，且每次发布的测试版本，应该从此分支上发出。同样，每次发布测试版本时，我们也要打上对应的Tag。如果测试版本测试无误后，发起merge-request，由代码维护者确认无误后，merge到master再发布release版本。注：小版本发布同样需要遵循此原则。

3) develop-feature :功能开发分支是项目在开发中大型功能时，从develop检出的分支。此类型的分支可以有多个。待功能开发完成后，发布debug版本初步测试无重大问题后，发起merge-request，将代码merge到develop上并再次发布功能测试版本。merge完成后后续的debug将在develop上进行。

4）develop-name : 此类分支可能由开发者从develop或master检出用于个人调试或单项功能测试等用途，主要是给开发者做本地代码备份用，并无其他意义。

##3.源码管理规范
1.关于pull/push及conflict  
使用过git的同学都清楚，在项目开发过程中，不可避免的会遇到提交代码冲突的问题。冲突是由于检出分支后，某个文件被他人修改过，同时本地也做了修改。因此为了避免冲突，我们所有的代码在提交之前应该先pull。实在无法避免的遇到了冲突，我们可以用文件对比器来对比查看解决冲突。一般我们会用beyond compare或者meld。

2.关于代码提交  
每一次的代码提交，我们都可以将其归类（fix/feat/doc/test/etc.）。因此,建议大家提交代码时按以下格式提交。另外，建议大家提交代码时，尽量将同一次修改的代码(不管是fix-bug还是add-feature)在一次commit中提交。这样如果以后遇到代码回滚或其他问题定位时，不至于遗漏某个提交点。

    //git commit -m "title" -m "description"
    git commit -m "fix" -m "fix bug 34523,list scroll error"
    
3.关于Tag  
Tag即标记。每一次发版不管是debug还是release，我们都应该在对应的分支上打上Tag。这样便于我们后续问题定位跟踪。我们可以在project的页面直接点+号，再点New Tag进入Tag配置页面。常规的配置包括本次发版的版本号及本次发版的重大修改点。

![tag_img](https://raw.githubusercontent.com/zhouzhongbo/ImgStore/master/gitlab_tag.png)


    



