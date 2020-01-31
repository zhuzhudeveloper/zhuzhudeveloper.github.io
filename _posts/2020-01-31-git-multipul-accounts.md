## Git Multipul Accounts
### Get Ready
```
git config --global --unset user.name
git config --global --unset user.email
```
### Generate a pair of rsa for each account
```
cd ~/.ssh
ssh-keygen -t rsa -C "user.email"
//You can name the rsa file.
```
### Add all local rsa
```
ssh-add ~/.ssh/id_rsa_githubio (account1)
ssh-add ~/.ssh/id_rsa_githubio2 (account2)
```
### Edit config file
```
touch config
```
The content of config
```
Host github 
HostName github.com 
User zhuzhu 
IdentityFile ~/.ssh/id_rsa_githubio

Host gitlab
HostName gitlab.com
User zhuzhu
IdentityFile ~/.ssh/id_rsa_gitlab
```
### Copy the content of id_rsa_githubio.pub to setting SSH of your github account
```
vi ~/.ssh/id_rsa_githubio
```
Reference: https://segmentfault.com/a/1190000016269686
