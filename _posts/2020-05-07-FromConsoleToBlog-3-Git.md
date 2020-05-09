---
title: 'From console to blog: Git'
tags:
 - blogging
---

This one will hopefully help some people get some basic understanding of [Git](https://git-scm.com/), a distributed source code management (SCM) tool created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds). The objective here is to create a Git repository for the new blag. The repository will be hosted at GitHub. SCMs are particularly well fitted to deal with the text files that power Static Site Generatorslike Jekyll. It is also what will enable some of the automation which will power the blog when it is moved to production.  

### Creating the repository

After creating an account of GitHub if necessary, let's create a [new repository](https://github.com/new) for the blog.

<figure>
  <a class="image-popup" href="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_1.webp"><img src="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_1.webp"></a>
  <figcaption>GitHub New Repository.</figcaption>
</figure>

### Initialise the repository locally

Back home to the  command line, let's initialise the local repository:

```shell
➜  blog.example.com git init
Initialized empty Git repository in /Users/user/blog.example.com/.git/
➜  blog.example.com git:(master) ✗
```
* Add the existing content to the repository

```shell
➜  blog.example.com git:(master) ✗ git add .
➜  blog.example.com git:(master) ✗ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   .gitignore
        new file:   404.html
        new file:   Gemfile
        new file:   Gemfile.lock
        new file:   _config.yml
        new file:   _posts/2020-05-07-welcome-to-jekyll.markdown
        new file:   _sass/blog.scss
        new file:   _sass/syntaxhighlight.scss
        new file:   about.markdown
        new file:   assets/css/main.scss
        new file:   index.html
        new file:   index.markdown

➜  blog.example.com git:(master) ✗
```
* Commit the newly added files to the local repository:

```shell
g.example.com git:(master) ✗ git commit -m 'initial commit' .
[master (root-commit) eade754] initial commit
 12 files changed, 689 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 404.html
 create mode 100644 Gemfile
 create mode 100644 Gemfile.lock
 create mode 100644 _config.yml
 create mode 100644 _posts/2020-05-07-welcome-to-jekyll.markdown
 create mode 100644 _sass/blog.scss
 create mode 100644 _sass/syntaxhighlight.scss
 create mode 100644 about.markdown
 create mode 100644 assets/css/main.scss
 create mode 100644 index.html
 create mode 100644 index.markdown
➜  blog.example.com git:(master)
```
* Link the local repository to the remote repository on GitHub


```shell
➜  blog.example.com git:(master) git remote add origin git@github.com:tomadeb/blog.example.com.git
➜  blog.example.com git:(master) git push -u origin master
Enumerating objects: 18, done.
Counting objects: 100% (18/18), done.
Delta compression using up to 8 threads
Compressing objects: 100% (14/14), done.
Writing objects: 100% (18/18), 7.51 KiB | 2.50 MiB/s, done.
Total 18 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:tomadeb/blog.example.com.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
➜  blog.example.com git:(master)
```

<figure>
  <a class="image-popup" href="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_2.webp"><img src="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_2.webp"></a>
  <figcaption>GitHub Repository with the initial content.</figcaption>
</figure>


### Git workflow for new post

From now on, the workflow of creating and amending content will need to integrate Git. As en example, let's create a new post.

**_posts/2020-05-08-a-new-post.markdown**
```markdown
---
title:  "This is a new post"
date:   2020-05-09 14:51 +0100
categories: jekyll update
---
Speedily say has suitable disposal add boy. On forth doubt miles of child. Exercise joy man children rejoiced. Yet uncommonly his ten who diminution astonished. Demesne new manners savings staying had. Under folly balls death own point now men. Match way these she avoid see death. She whose drift their fat off.

...

```

With the file newly created, Git does not no anything about the file:

```shell
➜  blog.example.com git:(master) ✗ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        _posts/2020-05-08-a-new-post.markdown

nothing added to commit but untracked files present (use "git add" to track)
➜  blog.example.com git:(master) ✗ 
```

The file needs to be added and committed to local repository before it can be pushed to the remote repository:

```shell
➜  blog.example.com git:(master) ✗ git add _posts/2020-05-08-a-new-post.markdown
➜  blog.example.com git:(master) ✗ git commit -m 'my new post' _posts/2020-05-08-a-new-post.markdown
[master 74337b9] my new post
 1 file changed, 10 insertions(+)
 create mode 100644 _posts/2020-05-08-a-new-post.markdown
➜  blog.example.com git:(master) git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
➜  blog.example.com git:(master) git push
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.13 KiB | 1.13 MiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:tomadeb/blog.example.com.git
   eade754..74337b9  master -> master
➜  blog.example.com git:(master) git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
➜  blog.example.com git:(master)
```

### Git workflow for a change

Now let's examine what the workflow looks like when a file, the new post file for example, is amended. 

```shell
➜  blog.example.com git:(master) echo 'oops I forgot something.' >> _posts/2020-05-08-a-new-post.markdown
➜  blog.example.com git:(master) ✗ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   _posts/2020-05-08-a-new-post.markdown

no changes added to commit (use "git add" and/or "git commit -a")
➜  blog.example.com git:(master) ✗ 
```

Git has detected the changed file and can report on exactly what has changed:

```shell
➜  blog.example.com git:(master) ✗ git diff _posts/2020-05-08-a-new-post.markdown
diff --git a/_posts/2020-05-08-a-new-post.markdown b/_posts/2020-05-08-a-new-post.markdown
index 7d0a614..9e6e340 100644
--- a/_posts/2020-05-08-a-new-post.markdown
+++ b/_posts/2020-05-08-a-new-post.markdown
@@ -8,3 +8,4 @@ Speedily say has suitable disposal add boy. On forth doubt miles of child. Exerc
 Fat son how smiling mrs natural expense anxious friends. Boy scale enjoy ask abode fanny being son. As material in learning subjects so improved feelings. Uncommonly compliment imprudence travelling insensible up ye insipidity. To up painted delight winding as brandon. Gay regret eat looked warmth easily far should now. Prospect at me wandered on extended wondered thoughts appetite to. Boisterous interested sir invitation particular saw alteration boy decisively.

 Certain but she but shyness why cottage. Gay the put instrument sir entreaties affronting. Pretended exquisite see cordially the you. Weeks quiet do vexed or whose. Motionless if no to affronting imprudence no precaution. My indulged as disposal strongly attended. Parlors men express had private village man. Discovery moonlight recommend all one not. Indulged to answered prospect it bachelor is he bringing shutters. Pronounce forfeited mr direction oh he dashwoods ye unwilling.
+oops I forgot something.
(END)
```

The file now needs to be committed to the local repository and push to the remote one:

```shell
➜  blog.example.com git:(master) ✗ git commit -m "I forgor something indeed" _posts/2020-05-08-a-new-post.markdown
[master dc0b861] I forgor something indeed
 1 file changed, 1 insertion(+)
➜  blog.example.com git:(master) git push
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 367 bytes | 367.00 KiB/s, done.
Total 4 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:tomadeb/blog.example.com.git
   74337b9..dc0b861  master -> master
```

<figure class="half">
  <a class="image-popup" href="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_3.webp"><img src="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_3.webp"></a>
  <a class="image-popup" href="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_4.webp"><img src="/assets/images/2020-05-07-FromConsoleToBlog-3-Git/2020-05-07-FromConsoleToBlog-3-Git_4.webp"></a>
  <figcaption>The above changes in GitHub.</figcaption>
</figure>

Please see the [GitHub Repository](https://github.com/tomadeb/blog.example.com) used to illustrate this article if needed.
