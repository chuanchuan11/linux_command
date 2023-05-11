>> Linux 

#### 常用操作

```
(1) linux 磁盘空间查看
    du -sh /data       该目录下的占用空间
    df -h              整个磁盘占用
    sudo du -sh ./ui*  查看ui目录占用空间

(2) 设置硬盘挂载
	umount -l /home               取消现有的挂载
	sudo mount /dev/sdb1 /home    挂载新的硬盘
	sudo blkid    获取挂载点的UUID
    	/etc/fstab    去该目录下，设置开机挂载


```

#### 网络相关

```
(1) 查看网络端口
    sudo netstat -anp  查看网络端口使用情况

(2) 查看是否禁用ping
    /proc/sys/net/ipv4/icmp_echo_ignore_all
    1禁用
    0开启

(3) 查看是否开启路由回查
    cat /proc/sys/net/ipv4/conf/Vlan_00/rp_filter
    修改命令：
    sysctl -w net.ipv4.conf.all.rp_filter=0

(4) linux 路由表文件
    /etc/data/iproute2/rt_tables
    
    
    
    
    
    
```

#### git命令

```
(0) 设置commit编译器
    git config --global core.editor vim 用这一条命令设置commit message的编译器为vim.以后提交就直接用git commit不用加-m "message"

(1) git fetch 同步代码过程
    git fetch origin master:temp  (从远程origin仓库，将远程master分支下载到本地，并取名为temp分支)
    git diff temp   查看刚拉下来的分支和本地分支的区别
    git merge temp  合并temp到本地分支
    git branch -d temp  删除temp分支
    如果该分支的代码之前没有merge到本地，那么删除该分支会报错，可以使用git branch -D temp强制删除该分支

(2) git pull 远程库名 远程分支名:本地分支名

    如果是要与本地当前分支merge，则冒号后面的<本地分支名>可以不写 git pull 远程库名 远程分支名

(3) git remote 不带参数，列出已经存在的远程仓库

    查看当前配置有哪些远程仓库，用 git remote 命令,列出每个远程库的简短名字。在克隆完某个项目后,至少可以看到一个名为 origin 的远程库，Git 默认使用这个名字来标识所克隆的原始仓库

(4) git remote -v 列出详细信息，在每一个名字后面列出其远程url
    如：
        >> git remote -v
        >> origin  buic-scm:/gm/connectivity/sys/conti-ip-setup

(5) 查看文件差别
	
    两次git commit之间的提交差异
	git diff hash1 hash2 --stat       只列出文件差异
	                                 --stat改为具体的文件  查看具体的文件内容差异
	显示已经在暂存区文件的修改内容
	git diff --cached  
	
	显示未在暂存区文件的修改内容
    	git diff [path/file] 

(6) 查看最近或某次提交得修改

    git log --name-status  每次修改的文件列表, 显示状态
    git show    显示最后一次的文件改变的具体内容
    git show -5 显示最后 5 次的文件改变的具体内容
    git show commitid 显示某个 commitid 改变的具体内容

(7) 删除未追踪的文件
	
	git clean -f   //删除 untracked files
	 
	git clean -fd  //连 untracked 的目录也一起删掉
	 
	git clean -xfd //连 gitignore 的untrack 文件/目录也一起删掉 （慎用，一般这个是用来删掉编译出来的 .o之类的文件用的）
	 
    //在用上述 git clean 前，强烈建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
	git clean -nxfd 
	git clean -nf
    	git clean -nfd

(8) Git stash使用

	git stash 命令不会存储下列文件:
		a) 工作区中新增的文件（untracked files）
		b) 被版本库忽略的文件（.gitignore 中定义的）
		c) 如果你还想要存储 untracked files，可以使用 -u 选项

	git stash -u  //如果你还想要存储 untracked files 和被版本库忽略的文件，可以使用 -a 选项
	git stash -a  //一般不推荐这么做，因为既然是被版本库忽略的文件，就没有必要再存储起来。除非你有非常特别的需求
	git stash save "备注信息"  //使用 save 选项,添加一个 message 注解
	git stash list //查看堆栈中的 stash 列表，堆栈中可能会有多个 stash，通过 stash_id 进行区分
	
	查看 stash 的内容：
		git stash show               //查看最近一次存储的文件情况
        	git stash show -p            //查看最近一次存储文件中的具体内容
        	git stash show stash@{id}    //查看具体某次存储的文件情况

	将堆栈中的 stash 应用到工作区
		git stash apply stash@{id}   //将堆栈中的指定 stash 应用到工作区（保留堆栈的内容）
		git stash apply              //将堆栈中的最近一次 stash，应用到工作区（保留堆栈的内容）

    	在成功应用了堆栈的 stash 后，立即将其从堆栈中删除
		git stash drop stash@{id}    //删除指定的 stash
		git stash drop               //删除最近一次的 stash
		git stash pop                //将堆栈中的最近一次 stash，应用到工作区并删除堆栈的内容
		git stash clear              //删除所有的 stash

(9) 放弃本地文件的修改
	git reset commitId        //取消commit的提交到工作区 (等于加--hard)
	git reset --soft commitId //取消commit的提交到暂存区
	git reset HEAD filename   //已经 git add到暂存区的文件，移动到工作区(使用. 移动所有文件)
	git checkout -- filename  //未使用git add 缓存代码，放弃修改, 注意中间有-- （使用. 放弃所有文件）
	git clean -f              //删除 untracked files

(10) 查看git 操作历史
	git reflog

```

#### repo 命令使用

    Android 使用 Git 作为代码管理工具，开发了 Gerrit 进行代码审核以便更好的对代码进行集中式管理
    
    还开发了 Repo 命令行工具，对 Git 部分命令封装，将百多个 Git 库有效的进行组织

```
(1) repo init
    repo init -u ssh://xxxxt -b xxx -m default.xml -g all --repo-url=ssh:xxx --repo-branch=stable-v2.4.1 --no-repo-verify

常用选项：
-u: manifest的仓库地址
-b: manifest仓库的branch（非开发分支的branch）
-m: 使用的manifest文件，缺省默认使用default.xml
-g: 使用的group，创建新的release分支时，可以用-g UCIT来单独下载我们有改动的仓库
--repo-url: 使用的repo仓库，默认会去找/usr/bin/repo里的源，搜索关键字“REPO_URL”
--repo-branch: repo仓库的分支
--no-repo-verify: 不对repo的签名做验证

(2) repo sync
    repo sync -c -d --no-tags -q -m snapshot/cxxxx.xml --force-sync

-c： 下载仓库时仅下载revision指定的分支，当前项目不可使用这个选项，会导致编译问题（有脚本会从.git里获取版本信息）
--no-tags：不下载任何tag信息，当前项目不可使用这个选项，会导致编译问题
-q：不显示详细下载信息
-d：将分支恢复为和manifest文件匹配的revision，可以用于还原新的commit或者patch，也可以还原分支的切换。不能还原没有commit的修改，也不能还原新的文件
-m xxx.xml：下载指定manifest文件里的版本，请删除相关的仓库后使用这个命令，避免引起分支混乱
--force-sync：强制更新。为了避免引发环境错乱，通常不建议使用，目前仅有一个适用场景，就是仓库从TP的仓库变更为项目自己的仓库，重新repo sync时需要force

(3) repo start
    用来创建分支

(4) repo status
    等同于进入每个仓库执行了git status

(5) repo forall
    等同于进入各个仓库执行命令（不限于git命令）
    
(6) repo manifest
    下载完代码后，制作manifest的snapshot 

```







