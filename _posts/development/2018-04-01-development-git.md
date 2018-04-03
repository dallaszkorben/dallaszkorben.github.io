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



# 4. Simple Processes
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



# 4. Undo Changes

# 4.1. Undo Uncommited changes

# 4.1.1. Has not added to the Stage

# 4.1.2. Has added to the Stage

# 4.2. Undo Commited changes

# 4.2.1. Nuke Commit C and never see it again

# 4.2.2. Undo the Commit but keep your changes

# 4.2.3. Undo the Commit but leave your files in index


