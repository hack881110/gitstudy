﻿
        <p>在<a href="/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000">远程仓库</a>一节中，我们讲了远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。</p>
<p>GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。</p>
<p>搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的<code>apt</code>命令就可以完成安装。</p>
<p>假设你已经有<code>sudo</code>权限的用户账号，下面，正式开始安装。</p>
<p>第一步，安装<code>git</code>：</p>
<pre><code>$ sudo apt-get install git
</code></pre><p>第二步，创建一个<code>git</code>用户，用来运行<code>git</code>服务：</p>
<pre><code>$ sudo adduser git
</code></pre><p>第三步，创建证书登录：</p>
<p>收集所有需要登录的用户的公钥，就是他们自己的<code>id_rsa.pub</code>文件，把所有公钥导入到<code>/home/git/.ssh/authorized_keys</code>文件里，一行一个。</p>
<p>第四步，初始化Git仓库：</p>
<p>先选定一个目录作为Git仓库，假定是<code>/srv/sample.git</code>，在<code>/srv</code>目录下输入命令：</p>
<pre><code>$ sudo git init --bare sample.git
</code></pre><p>Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以<code>.git</code>结尾。然后，把owner改为<code>git</code>：</p>
<pre><code>$ sudo chown -R git:git sample.git
</code></pre><p>第五步，禁用shell登录：</p>
<p>出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑<code>/etc/passwd</code>文件完成。找到类似下面的一行：</p>
<pre><code>git:x:1001:1001:,,,:/home/git:/bin/bash
</code></pre><p>改为：</p>
<pre><code>git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
</code></pre><p>这样，<code>git</code>用户可以正常通过ssh使用git，但无法登录shell，因为我们为<code>git</code>用户指定的<code>git-shell</code>每次一登录就自动退出。</p>
<p>第六步，克隆远程仓库：</p>
<p>现在，可以通过<code>git clone</code>命令克隆远程仓库了，在各自的电脑上运行：</p>
<pre><code>$ git clone git@server:/srv/sample.git
Cloning into &#39;sample&#39;...
warning: You appear to have cloned an empty repository.
</code></pre><p>剩下的推送就简单了。</p>
<h3 id="-">管理公钥</h3>
<p>如果团队很小，把每个人的公钥收集起来放到服务器的<code>/home/git/.ssh/authorized_keys</code>文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用<a href="https://github.com/res0nat0r/gitosis">Gitosis</a>来管理公钥。</p>
<p>这里我们不介绍怎么玩<a href="https://github.com/res0nat0r/gitosis">Gitosis</a>了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。</p>
<h3 id="-">管理权限</h3>
<p>有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。<a href="https://github.com/sitaramc/gitolite">Gitolite</a>就是这个工具。</p>
<p>这里我们也不介绍<a href="https://github.com/sitaramc/gitolite">Gitolite</a>了，不要把有限的生命浪费到权限斗争中。</p>
<h3 id="-">小结</h3>
<ul>
<li><p>搭建Git服务器非常简单，通常10分钟即可完成；</p>
</li>
<li><p>要方便管理公钥，用<a href="https://github.com/sitaramc/gitolite">Gitosis</a>；</p>
</li>
<li><p>要像SVN那样变态地控制权限，用<a href="https://github.com/sitaramc/gitolite">Gitolite</a>。</p>
</li>
</ul>

    