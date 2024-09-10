
## command
> 新建纯版本库 `git init --bare`
> 创建远程分支 `git remote add origin [username]@[address]:~/gitRepository/gitProject.git`
> 本地分支链接远程分支 `git branch -u origin/[branch]`
> 从svn clone `git svn clone [svnRemote]`
> 合并两个分支 `git pull [remote] [branch] --allow-unrelated-histories`

## Ubuntu新连接到Github

- 在Ubuntu中添加已存在秘钥

    `nano ~/.ssh/config`

    *config*
    `IdentityFile ~/.ssh/gitHubKey`
- 在github中添加公钥

    `github->settings->SSH Keys`
- 设置用户名
    ```bash
    git config --global user.email [email]
    git config --global user.name [name]
    ```
- 校验秘钥是否能正常连接github

    `ssh -vT git@github.com`
    `ssh -T git@[address] -p [port] -i [privateSSH]`

```bash
# 生成PPK私钥
sudo apt install putty-tools
puttygen keyname -o keyname.ppk
```