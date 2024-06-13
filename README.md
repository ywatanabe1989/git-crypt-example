# git-crypt-test

## Setting your GPG key for cryption

``` bash
sudo apt-get install gnupg
gpg --full-generate-key
```

Navigate like this:
``` bash
(1) RSA and RSA (default)
4096
Expiration Date: 0 (not to expire).
Real name: Yusuke Watanabe
Email address: ywatanabe@alumni.u-tokyo.ac.jp
Comment (optional):
(O)kay
```

``` bash
gpg --list-keys
```

## Adds dummy sensitive data
``` bash
echo THIS IS SENSITIVE DATA > sensitive_data.txt
```


## Cryption of files under all secrets directories
``` bash
# Installation of the git-crypt command
sudo apt-get install git-crypt

# git-crypt init
git-crypt init
git-crypt export-key ../git-crypt-key 
git-crypt add-gpg-user ywatanabe@alumni.u-tokyo.ac.jp

# Tells git-crypt about which files should be encrypted on .gitattributes
touch .gitattributes
echo sensitive_data.txt filter=git-crypt diff=git-crypt >> .gitattributes

# Commit
git add .gitattributes
git commit -m "Encrypt sensitive data"

# Checks the encryption status
git-crypt status
# not encrypted: .gitattributes
# not encrypted: .gitignore
# not encrypted: README.md
#     encrypted: sensitive_data.txt

# git push
git push

# Lock and unlock if you want
git-crypt lock
git-crypt unlock
```

## References
- https://dev.to/heroku/how-to-manage-your-secrets-with-git-crypt-56ih

# git-encrypt-secrets # .bash.d/all/030-git.sh
