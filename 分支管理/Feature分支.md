﻿
        <p>软件开发中，总有无穷无尽的新的功能要不断添加进来。</p>
<p>添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。</p>
<p>现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。</p>
<p>于是准备开发：</p>
<pre><code>$ git checkout -b feature-vulcan
Switched to a new branch &#39;feature-vulcan&#39;
</code></pre><p>5分钟后，开发完毕：</p>
<pre><code>$ git add vulcan.py
$ git status
# On branch feature-vulcan
# Changes to be committed:
#   (use &quot;git reset HEAD &lt;file&gt;...&quot; to unstage)
#
#       new file:   vulcan.py
#
$ git commit -m &quot;add feature vulcan&quot;
[feature-vulcan 756d4af] add feature vulcan
 1 file changed, 2 insertions(+)
 create mode 100644 vulcan.py
</code></pre><p>切回<code>dev</code>，准备合并：</p>
<pre><code>$ git checkout dev
</code></pre><p>一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。</p>
<p>但是，</p>
<p>就在此时，接到上级命令，因经费不足，新功能必须取消！</p>
<p>虽然白干了，但是这个分支还是必须就地销毁：</p>
<pre><code>$ git branch -d feature-vulcan
error: The branch &#39;feature-vulcan&#39; is not fully merged.
If you are sure you want to delete it, run &#39;git branch -D feature-vulcan&#39;.
</code></pre><p>销毁失败。Git友情提醒，<code>feature-vulcan</code>分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令<code>git branch -D feature-vulcan</code>。</p>
<p>现在我们强行删除：</p>
<pre><code>$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 756d4af).
</code></pre><p>终于删除成功！</p>
<video width="648" height="434" controls>
<source src="http://michaelliao.gitcafe.io/video/force-delete-br.mp4">
<source src="http://github.liaoxuefeng.com/sinaweibopy/video/force-delete-br.mp4">
</video>

<h3 id="-">小结</h3>
<p>开发一个新feature，最好新建一个分支；</p>
<p>如果要丢弃一个没有被合并过的分支，可以通过<code>git branch -D &lt;name&gt;</code>强行删除。</p>

    