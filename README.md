( `ver.20200610` )

# Git道場
- Git を体で覚えて、使えるようになろう！
- という会です 
- スライドは https://esa-pages.io/p/sharing/4916/posts/122/3580bfa74e806586e642-slides.html

## 今日の目的
- Git の基本が使えるようになること
  - （Git に限りませんが）
  - よく使う道具は、体で覚えちゃうと便利:)
  - 反復練習、超重要！
 - 知ってる・わかってる <-> できる・使える
     - ぜんぜん違う

## よく使う道具
- 使用頻度が高いもの、毎回調べる？
  - → 覚えてしまうと使う回数分お得！
  - → ex. 掛け算九九, 円周率...etc.
- 開発リズム・開発効率があがる！
- 今回は Git

## どうして Git？
- バージョン管理システムは、開発の基礎
  - 今自分の書いたコードの差分
  - 過去に書かれたコードが、何をしたかった
  - 過去のある時点（たとえばバグが混入した時点）に戻れる
  - 他の人が書いたコードを取り入れやすい
- ...などがわかり、使えるとすごく便利

## どうして Git道場？
- 本やリファレンスで覚えるのがむずかしい
    - 写経もいいけど、ペアプロで覚えるのがオススメ
    - 教えたり、教わったりすると覚えやすい
- 反復練習で Git に慣れる
    - 使えるまでやれば使える:)

## どんなことをやるのか
- 【心】Git とは〜？
- 【技】今日覚えるコマンド
- 【体】体で覚えるまでコマンドを打つ！

# 心
- Gitとは
- バージョン管理システム（VCS: Version Control System)
    - 変更履歴を管理するシステム
    - Git の他にも CVS, Subversion, Mercuriarなどがある

## 分散管理
- 数年前は Subversion など中央管理が主流だった
  - 中央管理リポジトリにアクセスできないと使えない
  - ...など、不便なところがあった
- → Git の利点: 
    - ローカルでコミットできる、ブランチが切りやすい
    - ...など、開発しやすくて便利になった:)

## ローカルリポジトリとリモートリポジトリ
- ローカルは自分のもの
    - 基本好きにする。だって自分のだもん
- リモートはみんなのもの
    - みんなが使いやすいようにする。自分だけが使うわけじゃないからね
      - master ブランチに強制 push しない（共有済みコードの歴史を書き換えない）など、ある程度のお作法が必要

## Git と GitHub
- それぞれ違うもの
- Git: バージョン管理システム
- GitHub: 開発プラットフォーム
    - Git を使ってコードやファイルを管理するサービス
    - issue立てたり、コードレビューしたり、タスク管理したり…
    - 他にも GitLab , BitBucket などの類似サービスがある


# 技

## 今日使うコマンド一覧
```
git clone
git commit
git add
git status
git push
git pull
git pull --rebase
git rebase
```

## 今日の作業の流れをざっくり

```
$ git clone git@github.com:dic-git-dojo/【X-team】.git
$ cd 【X-team】

# エディタで編集
# 「編集〜コミット」を5回繰り返す
# コンフリクトするようにコミットすること
# コンフリクトは、チーム内のメンバーが同じ行を編集することで起こります。
$ git add Numbers.txt
$ git commit -m 'コミットメッセージ...'

# 順次pushしていきます。（一番最初にpushした方はコンフリクトは起こりません。）
$ git push origin master

# コンフリクトしたら
$ git pull #( もしくは `git pull --rebase` )
# git pullはmergeをします。git pull --rebaseはリベースをします。

# コンフリクトを解消
$ git add Numbers.txt
$ git rebase --continue
# (コンフリクト解消まで、 git add と git rebase --continue 繰り返す）
# (git rebase --continueを繰り返す回数は、ターミナルで確認ができます。)
```

## 意識したいこと
- commit はこまめに
- commit メッセージを書く
- （実際の開発現場でもするように）
- （個人開発でも複数人開発でもちゃんと書いてあると、後世の人がハッピー）

## commit はこまめに！
- テキスト書いてるときにこまめ保存する感覚
  - 動いたら commit、一段落ついたら commit
  - commit の整理は後からできる
    - 複数の commit を一つにするのは簡単
    - 一つの commit を複数に分けるのは難しい


## コマンドざっくり解説
- リファレンス: https://git-scm.com/docs
- `git clone`
    - リモート環境（今回は GitHub）から手元（ローカル）に持ってくる
    - .git ディレクトリはありますか？
    - どんなファイルが入っていて、ファイルの中身はどうなっていますか？
- `git add [ファイル名]`
    - 指定したファイルを Git の commit 対象にする
- `git commit -m ‘コミットメッセージ’`
    - コミットメッセージはなんのため？
    - → 意思の疎通、未来へのメッセージ
    - なぜ書いたのかが残っていると後で便利:)
- `git push origin master`
    - リモート環境（今回は origin master ）に、ローカル環境での作業をアップして共有する
    - 作業した行が被っているとコンフリクトすることがある
- `git pull`
    - 内部では `git fetch` + `git merge` が実行される
    - `git pull --rebase` のときと比べてコミットツリーはどうなりますか？
- `git pull --rebase`
    - 内部では git fetch + git rebase が実行される
    - `git pull` のときと比べてコミットツリーはどうなりますか？
- `git rebase --continue`
    - コンフリクトを解消し、add した後、rebase 作業を続ける
- `git status`
    - 今の状態を把握する
    - あれ？って思ったら git status を打って状況確認


# 体    

## 確認
- 自分のチーム決まってる？
  - チームリポジトリのコラボレータに入ってる？
  - https://github.com/dic-git-dojo/A-team/settings/collaboration
  - https://github.com/dic-git-dojo/B-team/settings/collaboration
  - https://github.com/dic-git-dojo/C-team/settings/collaboration


## やること
- 3-4人のチームで `Numbers.txt` ファイルを編集し合う
- commit メッセージを書く
  - commit メッセージで意思疎通ができるように書く
  - 何をしたのか、1年後の自分が読んでもわかるように書く
- コンフリクトするように commit してください〜

## では、スタート
- 気になること、困ったら手を上げてください〜 :hand: 
- 基本の流れ clone → commit を5回 → push 
  - コンフリクトで push できなかったら
      - `git pull` か `git pull --rebase` してコンフリクトを解消して git add 
- 途中 GitHub で Network graph を見てみると面白い
  - `https://github.com/dic-git-dojo/【X-team】/network`
  - 各メンバーの commit がどんな風になったか見れる

# 最後に
- ちょっと Git が使えそうな気持ちになれました(?_?)
  - 使えば使うほど、使えるようになるので、使っていきましょう:)
- 今日だけでは、Git が使いこなせるようにはなりません＞＜
  - 一気にできなくてOK。できるまで何度も繰り返して体で覚える
  - 使えると便利なものから一つずつ
  - 知ってるコマンド5個よりも、使えるコマンド1個の方が開発効率が上がります:)
  - Git は、とても便利な開発道具なので、便利に使っていきましょう:)


# おまけ

## 今日は使わなかったけどよく使う Git コマンド
- `git init`
  - 対象ディレクトリを Git 管理下にする
  - clone してきたものには不要
  - .git ディレクトリができる
  - ↑にはどんなファイルが入ってますか？
- `git add -p [ファイル名]`
    - ファイル内のコミットしたい箇所を指定して add
    - GUI だと便利:)
- `git commit --amend`
    - 一つ前のコミットを訂正する
- `git push -f [リモート名] [ブランチ名]`
- `git checkout [ブランチ名]`
- `git rebase`
- `git rebase -i HEAD~3`
    - HEAD から 3 commit 前の状態戻る
- `git rebase --abort`
    - リベースを中止する
- `git rebase --skip`
    - 対象 commit をスキップする（commit を捨てる）
- `git merge [ブランチ名]`
- `git log`
- `git fetch [リモート名]`
- `git branch`
    - ブランチ一覧
- `git stash save [stash名]`
-  `git stash pop`
-  `git stash list`
- `git remote add [ブランチ名] [URL]`
- `git diff`
    - 差分表示


## Git GUI アプリ
- https://git-scm.com/downloads/guis
- いろいろ使ってみて、使いやすいものを選ぼう
- アプリの裏側では、git コマンドが走ってる
- どんなコマンドが走るのか把握できてたほうが便利
- 櫻井は、git add や git commit だけ GUI を使ってます:)

## リファレンス、書籍など
- Pro Git: とりあえずコレがバイブル
    - Web: https://git-scm.com/book/ja/v2
    - PDF: https://progit-ja.github.io/
- [LearnGitBranching](http://k.swd.cc/learnGitBranching-ja/): gitのブランチを手を動かしながら学べて便利！
- [Gitによるバージョン管理](http://www.amazon.co.jp/dp/4274068641): Git道場の主催者の方々によって書かれていて、実際の開発現場での使われ方が載っていたはず

