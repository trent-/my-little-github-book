# Creating a repository

To create a git repository, you just need to run `git init` in the designated folder. How then do you set a github repository as your remote, so that you can push to it?

First, you need to have a repository created in GitHub. There are two ways to do this.

1. Use the GitHub web interface, following the steps described here: https://help.github.com/articles/create-a-repo/
2. Using the API, where you would pass in JSON data containing the name of the repo you are wanting to create.

Once the repository is created, you can add the remote and successfully push to it. You'll also likely want to set upstream by passing the `-u` or `--set-upstream` argument when you push to origin master.

```bash
# Set up the local git repository
mkdir demo1
cd demo1
git init
echo "# Demo Project" > README.md
git add README.md
git commit -m "Initial commit"
# Create a repository in your github account
# This step will be un-necessary if you already have the repository created
curl -u 'trent-' https://api.github.com/user/repos -d '{"name": "demo1"}'
# Set up the remote
git remote add origin git@github.com:trent-/demo1.git
# Push the changes to the remote, and set the remote as the upstream
git push -u origin master
```

Your git config would then look something like this:

```bash
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = git@github.com:trent-/demo1.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master

```
