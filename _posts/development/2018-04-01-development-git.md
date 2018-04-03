---
layout: post
published: true
mathjax: false
featured: false
comments: true

title: Git
modified: '2018-04-01'
description: Git
blog: development
category: [Development, Git]
tags: [Development, Git]
---
# 1. Data transport and locations

<img src="{{site.url}}{{site.image_folder}}/development/git-datatransport.png" width="500" />

# 2. File status lifecycle

<img src="{{site.url}}{{site.image_folder}}/development/git-filestatuslifecycle.png" width="900" />

# 3. HEAD

HEAD allways refers to the **most recent** commit on the **current branch**.  
When you change branches, HEAD is updated to refer to the new branch’s latest commit.

* **HEAD** refers to the most recent commit
* **HEAD~**, HEAD~1	refers to the commit before the tip
* **HEAD~~**, HEAD~2	refers to the commit even earlier
* **HEAD** = @

In a normal case the HEAD is a symbolic reference to the tip of a branch.  
You can check it with the following example.  
You checkout the master branch and then you check if the HEAD pints to the branch:


<p class="console">$ git checkout master
$ cat .git/HEAD

ref: refs/heads/master
</p>

You can check which commit the HEAD points to:
<p class="console">$ cat .git/refs/heads/maser

84d324bc8184d324bc8184d324bc8184d324bc81
</p>

If you now commit and check again what reference the HEAD to you will 
find that it still points to the master branch but the commit hash number changes to the latest commit.  
However you can checkout any commit as well. This is called a detached HEAD. 
Some commands which will cause your HEAD became detached are:

<p class="console">$ git checkout master^		# parent of master
$ git checkout HEAD~2		# grandparent of current HEAD
$ git checkout origin/master	# a non-local branch
</p>

These will all make .git/HEAD contain the actual (40-hex-digit) hash of the corresponding 
commit instead of some string like ref: refs/heads/branch  
To fix this you can re-attach the HEAD:

<p class="console">$ git checkout master</p>


# 4. Simple processes

# 4.1 Adding an existing project to GitHub

#1. Step into your_folder
<p class="console">$ cd &lt;your_folder&gt; </p>

#2. Initialize the local directory as a Git repository
<p class="console">$ git init</p>

#3. Adds the files in the local repository and stages them for commit
<p class="console">$ git add .</p>

#4. Commit the files that you've staged in your local repository
<p class="console">$ git commit -m "Initial commit"</p>

#5. Sets the new remote. remote_repository=https://github.com/&lt;your_id&gt;
<p class="console">$ git remote add origin &lt;remote_repository&gt; </p>

#6. Push the changes in your local repository to GitHub.
<p class="console">$ git push origin master</p>


# 4.2 Cloning a project from GitHub

#1. Clone the project. remote_repository=https://github.com/&lt;your_id&gt;
<p class="console">$ git clone &lt;remote_repository&gt; </p>

#2. Make your development

#3. Adds the changed/created files in the local repository and stages them
<p class="console">$ git add --all</p>

#4. Commit the files that you've staged in your local repository
<p class="console">$ git commit -m "Initial commit"</p>

#5. Push the changes in your local repository to GitHub.
<p class="console">$ git push origin master</p>



# 4.3. Undo Uncommited changes

# 4.3.1. Has not added to the Stage
Let say you have modified.txt which was modified but the changes was not commited yet. 
The “**git status**” shows that the file is “**Changes not staged to commit**”
<p class="console">git checkout modified.txt</p>


# 4.3.2. Has added to the Stage
Let say you have added.txt which was modified and you have already added it to the stage. 
The “git status” shows about the file that the “Changes to be commited”.
In this case the “git checkout” does not work as checkout is from the index (staged) area. 
Instead of this you should get back the data from the Local Repository. 
As the HEAD points to the recent commit you should use the HEAD  
There are two solution for that. The first one checkouts the HEAD:
<p class="console">git checkout HEAD  added.txt</p>

The second solution is to get back the changes to the Workspace from the Stage. 
In this case the changes are still there in the file but it is not in the stage area. 
<p class="console">git reset HEAD  added.txt</p>


# 4.4. Undo Commited changes
The situation is the following. 
There are A, B and C commits. The HEAD  points to the  C commit and the Status is the C commit
<img style="margin-left: 40px" src="{{site.url}}{{site.image_folder}}/development/git-undo-01.png" />


# 4.4.1. Nuke Commit C and never see it again
<p class="console">$ git reset --hard HEAD~1</p>
The result is:
<img style="margin-left: 40px" src="{{site.url}}{{site.image_folder}}/development/git-undo-02.png" />


# 4.4.2. Undo the Commit but keep your changes
<p class="console">$ git reset HEAD~1</p>
You tell Git to move the HEAD pointer back one Commit. But you leave your files as they ware. 
Now “git status” shows the changes you had checked into C.
<img style="margin-left: 40px" src="{{site.url}}{{site.image_folder}}/development/git-undo-03.png" />
You can get back to Status B:
<p class="console">git checkout file</p>


# 4.4.3. Undo the Commit but leave your files in index
<p class="console">git reset  --soft HEAD~1</p>
Now “git status” shows files are in index.
<img style="margin-left: 40px" src="{{site.url}}{{site.image_folder}}/development/git-undo-04.png" />

