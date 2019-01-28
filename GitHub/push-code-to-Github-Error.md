## *Question: Push code to github with error msg*

```
> git push -u origin master
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

---

## Ans: local ssh key need sync with github
主要問題是本機上的ssh key需上傳至github

Step1. Test to connect github

```
chcs-iMac:test chc$ ssh -T git@github.com
git@github.com: Permission denied (publickey).
```
Step2. Generate ssh key

```
chcs-iMac:test chc$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/chc/.ssh/id_rsa):
/Users/chc/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/chc/.ssh/id_rsa.
Your public key has been saved in /Users/chc/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:LElTJlLHVDVTQtMMIboGVMUfonbv75dhq93YZRTAPDI chc@chcs-iMac.local
The key's randomart image is:
+---[RSA 2048]----+
|    ..++*++o%B.  |
|     o =..oE.O+  |
|      + .. oo... |
|     . =o.. .   .|
|      o.S. .    .|
|       o    .  + |
|           .  . *|
|            . .*+|
|             +=oo|
+----[SHA256]-----+
```

Step3. Check ssh key and cpoy it

```
chcs-iMac:test chc$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDDq3+WR8xzA880ghwlfEAxqm8PnQ2WJWzlcfWm+h+F9ty6+8XagTi4Q+Yi3jCRwuEzcxhxI9bjZrBUZalpQihgNuG1DkMYlo3QSrLCioDYrUouNrQh1WY1ty/SuErj0XpR4QSpZgKkyOD8wrDDZmhSEV0Yupw0XBYB4LBGkP3qLr9nUlm6IS3osXeaSEO/7iGIUSiKlWG0nLXzEvsK3LPRDjNttmZ7ai1YUpPLBmCLcS2crpJEziQ40xgphpDOvWY2jrTPKAZWO3LbXowg6hsymrWunh/IJO+WDho/G14vFio+cyO0O/u8g2AhEMZqGxqac/ngq3mhAQYzzB7jyu12 chc@chcs-iMac.local
```

Step4. Go to your github settings  --> SSH and GPG keys  --> Paste ssh key on here

Step5. Test to connect github again. 

```
chcs-iMac:test chc$ ssh -T git@github.com
Hi chcgpx! You've successfully authenticated, but GitHub does not provide shell access.
```

Step6. Push code to Github again

```
chcs-iMac:test chc$ git push -u origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 213 bytes | 213.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:chcgpx/test.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

Step7. Done!
