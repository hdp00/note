# Git

## command
> 本地分支链接远程分支 `git branch -u origin/name`

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