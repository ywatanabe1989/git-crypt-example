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

## Cryption of files under all secrets directories
``` bash
sudo apt-get install git-crypt
```

``` bash
git-crypt init
git-crypt export-key ../git-crypt-key 
git-crypt add-gpg-user <YOUR_GPG_USER_ID>
# sudo apt-get install git-crypt && git-crypt add-gpg-user ywatanabe@alumni.u-tokyo.ac.jp

<!-- git-encrypt-secrets # .bash.d/all/030-git.sh -->
cat .gitattributes
# ### git-crypt-secrets start ###
# ./.bash.d/secrets/** filter=git-crypt diff=git-crypt
# ./.ssh/secrets/** filter=git-crypt diff=git-crypt
# ### git-crypt-secrets end ###
git-crypt unlock
```

## References
- https://dev.to/heroku/how-to-manage-your-secrets-with-git-crypt-56ih
