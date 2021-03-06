- [ 超简单的GitHub新手使用手册](#head1)
	- [ 0.先了解一些概念](#head2)
	- [ 1.Git的下载、安装、配置](#head3)
		- [ 绑定用户](#head4)
		- [为 GitHub 账户设置 SSH key](#head5)
			- [(1)在Git生成 SSH Key](#head6)
			- [(2)为 GitHub 账号配置 ssh key](#head7)
	- [ 2.GitHub里新建一个repository](#head8)
	- [ 3.接下来开始从本地向GitHub上传文件啦](#head9)
		- [ （1）将1个本地文件夹作为本地仓库，文件夹里放你想传到GitHub上的文件；](#head10)
		- [ （2）将该本地仓库关联到github的TressureBox仓库（第2步里创建的）；](#head11)
		- [ （3）上传本地代码！](#head12)
		- [ PS：分支的使用，待更。。。](#head13)
	- [ 4.日常维护](#head14)
	- [ 遇到的问题](#head15)
# <span id="head1"> 超简单的GitHub新手使用手册</span>



## <span id="head2"> 0.先了解一些概念</span>

1. Git用来管理本地代码库Local repository，这是需要本地安装的；
2. GitHub是远程代码库remote repository，你想往上面传送和展示code；
3. Git中的一些基操：

- **push**：把文件从本地上传到GitHub，就像把本地文件上传到百度云一样；

![img](https://pic4.zhimg.com/v2-96ec1cead3a779e70972d66f671f658b_b.webp)

- **pull**：在github上在线编辑后，就pull到本地；

![img](https://pic3.zhimg.com/v2-9ea03ba3eaa5e981c65627b2dd5c590e_b.webp)

## <span id="head3"> 1.Git的下载、安装、配置</span>

下载和安装就不需要讲了，讲一下配置。你需要做的步骤有：

- 本地的 Git 要绑定 GitHub 账户；
- 在 Git 生成 SSH Key 和在 GitHub 里配置 SSH key；

### <span id="head4"> 绑定用户</span>

打开git-bash.exe，开始输：
`git config --global user.name "Your Name"`
`git config --global user.email "your_email@example.com"`
PS："Your Name"和"your_email@example.com"是你的GitHub用户名和邮箱

同时添加下面代码，这是为了记住用户名和密码, 不用每次都输入。

```csharp
[credential]
helper = store
```

这个命令会在 C:\Users\Administator （Administator为电脑用户名，每个人不同）目录下生成 .gitconfig 文件

![image-20201120192129101](.pic/超简单的GitHub新手使用手册/image-20201120192129101.png)



### <span id="head5">为 GitHub 账户设置 SSH key</span>

> 众所周知 ssh key 是加密传输。
>
> 加密传输的算法有好多，git 使用 rsa，rsa 要解决的一个核心问题是，如何使用一对特定的数字，使其中一个数字可以用来加密，而另外一个数字可以用来解密。这两个数字就是你在使用 git 和 gitHub 的时候所遇到的 public key 也就是公钥以及 private key 私钥。
>
> 其中，公钥就是那个用来加密的数字，这也就是为什么你在本机生成了公钥之后，要上传到 github 的原因。从 github 发回来的，用那公钥加密过的数据，可以用你本地的私钥来还原。
>
> 如果你的 key 丢失了，不管是公钥还是私钥，丢失一个都不能用了，解决方法也很简单，重新再生成一次，然后在 github.com 里再设置一次就行
>
> https://segmentfault.com/q/1010000000118744

#### <span id="head6">(1)在Git生成 SSH Key</span>

开始输命令：
`$ ssh-keygen -t rsa -C "your_email@example.com"` 

接下来先输入`yes`，表示存储在默认路径；再`二连回车`，表示不设置密码登录。

![image-20201120192151061](.pic/超简单的GitHub新手使用手册/image-20201120192151061.png)


生成成功后，去对应目录 `C:\Users\Administator\.ssh` （Administator为电脑用户名，每个人不同）用记事本打开 id_rsa.pub，得到 ssh key公钥。复制下来。

![image-20201120192201459](.pic/超简单的GitHub新手使用手册/image-20201120192201459.png)



#### <span id="head7">(2)为 GitHub 账号配置 ssh key</span>

打开 GitHub -->settings-->SSH and GPG keys-->点击 New SSH key。

接着输入Title,再把刚复制的 id_rsa.pub 文件内容粘贴到Key处，最后 Add SSH key 生成密钥。

![image-20201120192229141](.pic/超简单的GitHub新手使用手册/image-20201120192229141.png)

生成成功。

![image-20201120192241853](.pic/超简单的GitHub新手使用手册/image-20201120192241853.png)

## <span id="head8"> 2.GitHub里新建一个repository</span>

例如：TressureBox。

之后到该仓库复制仓库地址，后面要用。

```
git@github.com:sadbird1729/TressureBox.git
```



## <span id="head9"> 3.接下来开始从本地向GitHub上传文件啦</span>

三步走：

#### <span id="head10"> （1）将1个本地文件夹作为本地仓库，文件夹里放你想传到GitHub上的文件；</span>

首先进入你的本地目录；

`cd D:/TASK/jupyter_task/TressureBox`

把这个目录变成git可以管理的本地仓库

`git init`

把本地目录里所有文件加到本地仓库

`git add .`

`git commit -m "first commit"` 

双引号里写本次提交的备注

#### <span id="head11"> （2）将该本地仓库关联到github的TressureBox仓库（第2步里创建的）；</span>

`git remote add origin git@github.com:sadbird1729/TressureBox.git`

**PS:只有第一次创建本地仓库后需要输入此命令。之后不需要此步。**

#### <span id="head12"> （3）上传本地代码！</span>

`git push -u origin main`

完成！！

![image-20201120192328077](.pic/超简单的GitHub新手使用手册/image-20201120192328077.png)



#### <span id="head13"> PS：分支的使用，待更。。。</span>

## <span id="head14"> 4.日常维护</span>

本地文件更新了，想要传到github:

```
cd D:/TASK/TressureBox
git add . 
git commit -m "2nd commit"
git push
```

![image-20201120192348204](.pic/超简单的GitHub新手使用手册/image-20201120192348204.png)

在github上在线修改后，本地是之前版本，本地需要更新：

`git pull`



## <span id="head15"> 遇到的问题</span>

> Git 提示fatal: remote origin already exists 错误解决办法https://blog.csdn.net/top_code/article/details/50381432
>
> [Github] Github简易使用指南https://zhuanlan.zhihu.com/p/54127454



