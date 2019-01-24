# gitbook on github-page

## 1. First build a respository on github, e.g., iwiki.

## 2. build a branck called `gh-pages`
after building this branch, github will automatically serves a github-page for you.
```
git checkout gh-pages
```

## 3. build a gitbook static website
First go back to master branch:
```
git checkout master
```
Then, after installing gitbook and its dependencies, build `README.md` and `SUMMARY.md` following gitbook 
instruction, and run following codes to generate static website files which were located at `./_book`.
```
gitbook init
gitbook build
```
Now we can push all these files to master branch, by the way, the master branch is used for saving your 
gitbook's source files.
```
git add ./*
git commit -m "General updates"
git push origin master
```


