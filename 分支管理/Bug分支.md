﻿
        <p>软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。</p>
<p>当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支<code>issue-101</code>来修复它，但是，等等，当前正在<code>dev</code>上进行的工作还没有提交：</p>
<pre><code>$ git status
# On branch dev
# Changes to be committed:
#   (use &quot;git reset HEAD &lt;file&gt;...&quot; to unstage)
#
#       new file:   hello.py
#
# Changes not staged for commit:
#   (use &quot;git add &lt;file&gt;...&quot; to update what will be committed)
#   (use &quot;git checkout -- &lt;file&gt;...&quot; to discard changes in working directory)
#
#       modified:   readme.txt
#
</code></pre><p>并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？</p>
<p>幸好，Git还提供了一个<code>stash</code>功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：</p>
<pre><code>$ git stash
Saved working directory and index state WIP on dev: 6224937 add merge
HEAD is now at 6224937 add merge
</code></pre><p>现在，用<code>git status</code>查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。</p>
<p>首先确定要在哪个分支上修复bug，假定需要在<code>master</code>分支上修复，就从<code>master</code>创建临时分支：</p>
<pre><code>$ git checkout master
Switched to branch &#39;master&#39;
Your branch is ahead of &#39;origin/master&#39; by 6 commits.
$ git checkout -b issue-101
Switched to a new branch &#39;issue-101&#39;
</code></pre><p>现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：</p>
<pre><code>$ git add readme.txt 
$ git commit -m &quot;fix bug 101&quot;
[issue-101 cc17032] fix bug 101
 1 file changed, 1 insertion(+), 1 deletion(-)
</code></pre><p>修复完成后，切换到<code>master</code>分支，并完成合并，最后删除<code>issue-101</code>分支：</p>
<pre><code>$ git checkout master
Switched to branch &#39;master&#39;
Your branch is ahead of &#39;origin/master&#39; by 2 commits.
$ git merge --no-ff -m &quot;merged bug fix 101&quot; issue-101
Merge made by the &#39;recursive&#39; strategy.
 readme.txt |    2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git branch -d issue-101
Deleted branch issue-101 (was cc17032).
</code></pre><p>太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到<code>dev</code>分支干活了！</p>
<pre><code>$ git checkout dev
Switched to branch &#39;dev&#39;
$ git status
# On branch dev
nothing to commit (working directory clean)
</code></pre><p>工作区是干净的，刚才的工作现场存到哪去了？用<code>git stash list</code>命令看看：</p>
<pre><code>$ git stash list
stash@{0}: WIP on dev: 6224937 add merge
</code></pre><p>工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：</p>
<p>一是用<code>git stash apply</code>恢复，但是恢复后，stash内容并不删除，你需要用<code>git stash drop</code>来删除；</p>
<p>另一种方式是用<code>git stash pop</code>，恢复的同时把stash内容也删了：</p>
<pre><code>$ git stash pop
# On branch dev
# Changes to be committed:
#   (use &quot;git reset HEAD &lt;file&gt;...&quot; to unstage)
#
#       new file:   hello.py
#
# Changes not staged for commit:
#   (use &quot;git add &lt;file&gt;...&quot; to update what will be committed)
#   (use &quot;git checkout -- &lt;file&gt;...&quot; to discard changes in working directory)
#
#       modified:   readme.txt
#
Dropped refs/stash@{0} (f624f8e5f082f2df2bed8a4e09c12fd2943bdd40)
</code></pre><p>再用<code>git stash list</code>查看，就看不到任何stash内容了：</p>
<pre><code>$ git stash list
</code></pre><p>你可以多次stash，恢复的时候，先用<code>git stash list</code>查看，然后恢复指定的stash，用命令：</p>
<pre><code>$ git stash apply stash@{0}
</code></pre><video controls width="648" height="434" controls>
<source src="http://michaelliao.gitcafe.io/video/stash-fix-bug.mp4">
<source src="http://github.liaoxuefeng.com/sinaweibopy/video/stash-fix-bug.mp4">
</video>

<h3 id="-">小结</h3>
<p>修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；</p>
<p>当手头工作没有完成时，先把工作现场<code>git stash</code>一下，然后去修复bug，修复后，再<code>git stash pop</code>，回到工作现场。</p>

    