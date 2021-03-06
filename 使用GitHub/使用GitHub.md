﻿
        <p>我们一直用GitHub作为免费的远程仓库，如果是个人的开源项目，放到GitHub上是完全没有问题的。其实GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。</p>
<p>在GitHub出现以前，开源项目开源容易，但让广大人民群众参与进来比较困难，因为要参与，就要提交代码，而给每个想提交代码的群众都开一个账号那是不现实的，因此，群众也仅限于报个bug，即使能改掉bug，也只能把diff文件用邮件发过去，很不方便。</p>
<p>但是在GitHub上，利用Git极其强大的克隆和分支功能，广大人民群众真正可以第一次自由参与各种开源项目了。</p>
<p>如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页<a href="https://github.com/twbs/bootstrap">https://github.com/twbs/bootstrap</a>，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：</p>
<pre><code>git clone git@github.com:michaelliao/bootstrap.git
</code></pre><p>一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址<code>git@github.com:twbs/bootstrap.git</code>克隆，因为没有权限，你将不能推送修改。</p>
<p>Bootstrap的官方仓库<code>twbs/bootstrap</code>、你在GitHub上克隆的仓库<code>my/bootstrap</code>，以及你自己克隆到本地电脑的仓库，他们的关系就像下图显示的那样：</p>
<p><img src="../files/attachments/001384926554932eb5e65df912341c1a48045bc274ba4bf000/0.jpg" alt="github-repos"></p>
<p>如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。</p>
<p>如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。</p>
<p>如果你没能力修改bootstrap，但又想要试一把pull request，那就Fork一下我的仓库：<a href="https://github.com/michaelliao/learngit">https://github.com/michaelliao/learngit</a>，创建一个<code>your-github-id.txt</code>的文本文件，写点自己学习Git的心得，然后推送一个pull request给我，我会视心情而定是否接受。</p>
<h3 id="-">小结</h3>
<ul>
<li><p>在GitHub上，可以任意Fork开源仓库；</p>
</li>
<li><p>自己拥有Fork后的仓库的读写权限；</p>
</li>
<li><p>可以推送pull request给官方仓库来贡献代码。</p>
</li>
</ul>

    