# 遠端儲存庫基本操作


## 檢查遠端儲存庫設定
``` shell
$ git remote -v
```

## 連結遠端儲存庫
``` shell
$ git remote add origin <remote_git_repository_url>
```
上面指令中的<code>origin</code>是一個遠端儲存庫URL的 "代稱"，不一定要叫<code>origin</code>，想要取其他名稱也可以。例如:
``` shell
$ git remote -v
origin  https://github.com/xinxi5639/git-command-test.git (fetch)
origin  https://github.com/xinxi5639/git-command-test.git (push)
```
``` shell
$ git remote rename origin origin-github
$ git remote -v
origin-github   https://github.com/xinxi5639/git-command-test.git (fetch)
origin-github   https://github.com/xinxi5639/git-command-test.git (push)
```
所以實際上<code>origin</code>的用意，就只是針對遠端儲存庫取個名字而已。

而且實際上一個本地端分支也只會搭配一個遠端儲存庫分支，換言之我們只會使用 "一次" 這個指令來對網址命名，以及建立本地端與遠端儲存庫的連線。也因為這個原因，一般約定俗成好像都叫做<code>origin</code>，並不會因為不同專案而取不同名稱。

## 將local端的分支推到遠端儲存庫
``` shell
$ git push -u origin <local_branch_name>:<remote_branch_name>
```
<code>-u</code>,<code>--set-upstream</code>, 設定本地分支與遠端分支的關聯，後續本地端執行git push/pull時，Git就會知道要推送或拉取到哪一個遠端分支。

<code><local_branch_name>:<remote_branch_name></code>, 本地端與遠端分支名稱可以不同，不過一般會讓兩邊分支名稱相同，方便維護。

這邊本地端分支名稱使用<code>local/branch</code>，要推送commit到遠端分支名稱為<code>remote/branch</code>的分支下，命令如下:
``` shell
$ git push -u origin local/branch:remote/branch
```

如果本地端與遠端分支名稱相同時，可以簡化命令如下:
``` shell
$ git push -u origin <branch_name>
```

只要設定過本地端分支與遠端分支的關聯，之後要推送或拉取時，只需要執行簡化的命令:
``` shell
$ git push
$ git pull
```
