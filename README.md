# Git 檔案狀態
* Untracked files (未追蹤的檔案) 
* Changes not staged for commit (檔案的修改未加入暫存區，不會包含在下一次提交)
* Changes to be committed (已加入暫存區，準備在下一次提交包含的檔案變更)
* Ignored (被<code>.gitignore</code>忽略的檔案)

Note. 從版本控制中移除文件
``` shell
$ git rm --cached <file>
```

## git checkout 常見用法
* 切換分支: 切換到指定的分支，將工作目錄的內容改為該分支的狀態。
``` shell
$ git checkout <branch_name>
```
*<code>git switch</code>: 專門用於切換分支的指令。

*注意: 切換分支前需確保工作目錄乾淨，如果有未提交的變更，切換分支可能導致衝突

* 建立並切換到新分支: 在當前分支的基礎上，建立並切換到新分支。
``` shell
$ git checkout -b <new_branch_name>
```

* 切換提交 (分離HEAD狀態): 檢視某次提交的內容，而不切換到某個分支。
``` shell
$ git checkout <commit_hash>
```
*注意： 在分離 HEAD 狀態中進行的更改，不會與任何分支關聯，需手動建立新分支或提交。

* 還原工作目錄中的檔案: 將工作目錄中的檔案還原為最新提交或指定版本。
``` shell
# 還原到最新提交版本
$ git checkout -- <file_name>

# 從特定提交中提取檔案，覆蓋當前版本
$ git checkout <commit_hash> -- <file_name>
```

## git restore 常見用法
是用來還原檔案內容或撤銷變更的指令。該指令能處理工作目錄和暫存區的檔案。
``` shell
# 還原單檔案至 HEAD
$ git restore <file_name>

# 還原整個工作目錄
$ git restore .

# 把檔案從暫存區移出
$ git restore --staged <file_name>

# 還原檔案至特定提交
$ git restore --source <commit_hash>
```

## git reset 常見用法
將 HEAD 指向之前的某次提交，並選擇參數影響暫存區和工作目錄的內容。
``` shell
git reset <commit_hash>
```

| 參數 | 描述 | 適用情境 |
| :-: | :-: | :-: |
| <code>--soft</code> | 回退到指定的提交，保留暫存區和工作目錄的變更。 | 適合修改最近的提交內容。 |
| <code>--mixed</code>(default) | 回退到指定的提交，清空暫存區，保留工作目錄的變更。 | 適合重組暫存區內容。|
| <code>--hard</code> | 回退到指定的提交，清空暫存區與工作目錄的變更。 | 適合徹底放棄當前進度。 |
| <code>--keep</code> | 類似 --hard，但保留未追蹤的檔案變更。 | 適合回退部分進度但保留新檔案。 |

## git clean 常見用法
是用來清理工作目錄中未追蹤檔案的指令，適合用於刪除未納入版本控制的檔案或目錄，幫助保持工作目錄的整潔。
``` shell
# 刪除所有未追蹤的檔案和目錄
$ git clean -f -d
```
| 參數 | 描述 |
| :-: | :-: |
| <code>-f</code> | 強制執行清理操作（<code>git clean</code> 默認不執行任何動作）。 |
| <code>-n</code> | 模擬清理，顯示將被刪除的檔案和目錄。 |
| <code>-d</code> | 包括未追蹤的目錄 |
| <code>-x</code> | 包括<code>.gitignore</code> 中忽略的檔案 |