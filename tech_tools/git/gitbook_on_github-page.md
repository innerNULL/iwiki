# gitbook on github-page

## 1. Building a Respository on Github, e.g., iwiki.

## 2. Building a Branch Called `gh-pages`
After building following branch, github will automatically serves a github-page for you.
```bash
git checkout -b gh-pages
```

## 3. Building Gitbook Static Website Files
First go back to master branch:
```bash
git checkout master
```
Then, after installing gitbook and its dependencies, build `README.md` and `SUMMARY.md` following gitbook 
instruction, and run following codes to generate static website files which were located at `./_book`.
```bash
gitbook init
gitbook build
# Can also use `gitbook serve` to replace `gitbook build` which can let
# you see your website on localhost.
```
Now we can push all these files to master branch, by the way, the master branch is used for saving your 
gitbook's source files.
```bash
git add ./*
git commit -m "General updates"
git push origin master
```

## 4. Moving Gitbook Static Website Files To `gh-pages` Branch
First go to `gh-pages` branch by:
```bash
git checkout gh-pages
```
Notice this time we don't need `-b` since we have already built this branch.  

After running above codes, we need all the static website files in "./_book" located 
at master branch, so the most directly method is running following codes:
```bash
# The current state is, located at the respository's root path, with `gh-pages`
# branch. After `git clone`, use the `master_barnch` represents the 
# respository's path name.

git rm -r ./*
git clone "the respository"
mv ./master_barnch/_book/* ./
rm -rf master_barnch
```
Now we get all we need, so push to github:
```bash
git add ./*
git commit -m "Update docs"
git push original gh-pages
```
Congrates! Everything done, you can visit the "Setting" boart to get the url 
of your github pages.

