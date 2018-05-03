撤除一些操作
git checkout config/db.php 


git 只拉取某个目录  
```
mkdir myrepo
cd myrepo
git init
git config core.sparseCheckout true
git remote add -f origin git://...
echo "path/within_repo/to/desired_subdir/*" > .git/info/sparse-checkout
git checkout [branchname] # ex: master
```
