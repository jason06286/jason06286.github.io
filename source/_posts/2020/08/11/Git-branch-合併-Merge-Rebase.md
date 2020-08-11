---
title: Git branch 合併 Merge Rebase
tags: git
category: git
abbrlink: 33161
date: 2020-08-11 14:49:28
---
# 分支
在開發中我們會有許多版本，像是開發版、測試版，測試功能都正常，才會合併到上線版。
> 分支就像是影分身術的概念，而我們會透過 `git `的指令，來取需要分身的部分。 
```
新增分支：git branch 分支名稱
查看分支：git branch 
```
> `HEAD` 表示目前在哪裡，預設是指向 `master`

![](/images/git02/git1.png)
```
切換分支：git checkout 分支名稱
刪除分支：git branch -d 分支名稱 、-D 是強制刪除
還原上個版本：git reset HEAD^
```
> `HEAD` 代表目前位置 
> `HEAD^` 代表 HEAD 往前一個版本，`HEAD^^` 代表 HEAD 往前二個版本  
> `HEAD~1 `代表 HEAD 往前一個版本，`HEAD~4 `代表 HEAD 往前四個版本 
 
![](/images/git02/git2.png)
![](/images/git02/git3.png)
![](/images/git02/git4.png)
# 分支合併
## Merge
在使用 `merge` 合併分支的時候，`git` 預設會以 `fast-forward` 的模式進行，那什麼是 `fast-forward` 和 `no-fast-forward` 呢？
#### fast-forward
```
git merge 分支名稱
```
![](https://www.maxlist.xyz/wp-content/uploads/2020/05/merge_fast_foard.gif)
[Gif 來源：CS Visualized](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1#merge)
#### no-fast-forward
```
git merge 分支名稱 --no-ff
```
![](https://www.maxlist.xyz/wp-content/uploads/2020/05/merge_no_fast_forward.gif)
[Gif 來源：CS Visualized](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1#merge)

可以很清楚的看到同樣都是 `merge`，使用` no-fast-forward` 的模式，會長出小耳朵，可以讓成員在日後很清楚辨識不同的 `Commit` 歷程，但小耳朵過多會造成混亂，所以會需要 fast-forward 用來 `merge` 些較不重要的 `Commit`，像是零碎的 `bug fix`，保持 `Commit` 的乾淨。
> 重要的合併用 `git merge 分支名稱 --no-ff`
> 不重要的合併用 `git merge 分支名稱`
### 衝突
當同時修改同一個檔案的同一行code，就會發生衝突，
因為` git` 無法知道哪個才是正確的內容，
這時就需要雙方溝通，看要用誰的code。

假設我們在 `cat `分支修改了 `index.html` 的內容如下：
![](/images/git02/git5.png)
然後在 `dog` 分支剛好也修改了 `index.html`，內容如下：
![](/images/git02/git6.png)
這時候進行合併，發現因為第 9 行重複，所以產生了衝突，
此時狀態，已被放置至暫存區。
選要用哪個內容，在跑過一次 `Commit` 流程，就解決衝突了。
![](/images/git02/git7.png)
![](/images/git02/git8.png)
## Rebase
從字面上來看，「rebase」是「re」加上「base」，翻成中文大概是「重新定義分支的參考基準」的意思。

#### 合併版本
![](https://www.maxlist.xyz/wp-content/uploads/2020/05/git_rebase.gif)
[Gif 來源：CS Visualized](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1#merge)
#### 修改歷史 commit 紀錄
![](https://www.maxlist.xyz/wp-content/uploads/2020/05/git_rebase_i.gif)
[Gif 來源：CS Visualized](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1#merge)

#### 使用 Rebase 來合併分支
優點:很自由可以自己決定歷史順序
缺點:有時候恍神失智，忘了自己 `Rebase` 到哪，
不小心弄壞了還不知道怎麼 `reset` 回來 (¬_¬)，
發生衝突時會停在一半，對不熟悉 `Rebase` 的人來說是個困擾
#### 使用時機
通常在還沒有推（`Push`）出去但感覺得有點亂（或太瑣碎）的 `Commit`，可以先使用 `Rebase` 分支來整理完再推出去。但如同前面提到的，`Rebase` 等於是修改歷史，修改已經推出去的歷史可能會對其它人帶來困擾，所以對於已經推出去的內容，非必要的話請盡量不要使用 `Rebase`。
#### 技術總結:
> 創立 `branch` 用 `git branch 分支名稱`
> 切換 `HEAD` 位置 `git ckeckout 位置`
> 合併到主要版本用 `git merge 分支名稱 --no-ff`
> 整理 `commit` 點 可以用 `git rebase` 和 `git merge`

### 參考文章
[為你自己學 Git](https://gitbook.tw/)
### 練習 Git 小遊戲
[Learn Git Branching](https://learngitbranching.js.org/?locale=zh_TW)


