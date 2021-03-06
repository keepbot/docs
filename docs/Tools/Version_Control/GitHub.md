### Independent history catalogs of git repositories
```bash
# Makes a bunch of history folders formatted by the next way: <repository>-<number_of_commit>-<commit_hash>
# Check commit_list.end for mistakes, you need simple list of commits
git clone <repository_url> <repository>
cd <repository> && git log --pretty=format:"%h" > ../commit_list && cd ..
tac commit_list > commit_list.end 
i=1; for cid in `cat commit_list.end`; do cp -r <repository> <repository>-$i-$cid; cd <repository>-$i-$cid; git checkout $cid; cd ..; ((i=i+1)); done
```
### Clone all user's repositories
```bash
# Get complete list of user's repositories in JSON file
curl -s https://api.github.com/users/<username>/repos?per_page=200 > repo.list.json
python -c "import json,sys,os;file = open('repo.list.json' ,'r');obj = json.load(file);obj_size = len(obj);cmd = 'git clone  ';[os.system(cmd + obj[x]['clone_url']) for x in range(0, obj_size)];file.close()"
# And dont forget about "space"(%20, " ") in cmd = 'git clone ', it's completely nessesary
# Another way to clone up to 200 user's repos(just in shell): 
curl -s https://api.github.com/users/keepbot/repos?per_page=200 | jq '.[] | ."clone_url"' | xargs -I '{}' git clone {}
```

### Generate new key-pair in current folder`
```bash
sh-keygen -t rsa -b 4096 -C "email@domain" -f deploy_key
```
