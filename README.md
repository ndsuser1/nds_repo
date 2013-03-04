nds_repo
========

# 1. Github の最初のページに何か書かれてる。そのとおりにやってみる。

    $ git clone https://github.com/ndsuser1/nds_repo.git
    $ touch README.md
    $ git init
    $ git add README.md
    $ git commit -m "first commit"
    $ git remote add origin https://github.com/ndsuser1/nds_repo.git
    $ git push -u origin master

# 2. ファイル A B C を追加する。

とりあえず、touch コマンドで空のファイルを作る。

    $ touch A B C

リポジトリに追加しないで、ステータスを見ると

    $ git status
    # On branch master
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #       A
    #       B
    #       C
    nothing added to commit but untracked files present (use "git add" to track)

リポジトリに追加（add）して、

    $ git add A B C

同じようにステータスを見ると

    $ git status
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #       new file:   A
    #       new file:   B
    #       new file:   C
    #

それじゃあ、この add してステージされたファイルを commit しましょう。

    $ git commit -m 'add some files'
    [master c6c669d] add some files
    Your name and email address were configured automatically based
    on your username and hostname. Please check that they are accurate.
    You can suppress this message by setting them explicitly:
        git config --global user.name "Your Name"
        git config --global user.email you@example.com
    After doing this, you may fix the identity used for this commit with:
        git commit --amend --reset-author

名前とメアドを設定して、やり直しもできると丁寧なお言葉を頂きました。

では、グローバルなオプションはそのままにして、このリポジトリのみで使う
名前とメアドを設定しておく。

    $ git config user.name "YAMADA, Taro"
    $ git config user.email yamada.t@example.com

commit のやり直し。作成者の名前も変更するために --reset-auther も付ける。
それから、push する。

    $ git commit -m 'add some files' --amend --reset-author
    $ git push

# 3. ブランチとマージで遊ぶ

ブランチを作るには、チェックアウトを使う。

    $ git checkout -b topic

ブランチ topic のファイル A に「こんにちは」と書く、そしてステータスを見ると、

    $ git status
    # On branch topic
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   A
    #
    no changes added to commit (use "git add" and/or "git commit -a")

まだステージしてない (add してない)、コミットと同時に add でいいなら -a が使える、
と教えてくれているので、そのとおりにやってみる。

    $ git commit -m 'modify A' -a

新しいブランチでコミットしてプッシュすると、

    $ git push
    Everything up-to-date

git は、この時点では master をプッシュすると思っていたので、
master は全部更新されているよ（プッシュするものはないよ）と教えてくれる。
なにもやってくれない。

普通は、チャートを見るためにプッシュするなんてしないから、
もっともな話ですね。全部、プッシュしましょう。

    $ git push --mirror
    Counting objects: 5, done.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 325 bytes, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/ndsuser1/nds_repo.git
     * [new branch]      topic -> topic
     * [new branch]      origin/master -> origin/master

次は、マージしましょう。master をチェックアウトして、
ステータスを見ると、変更前の状態にあることが分ります。

    $ git checkout master
    $ git status
    # On branch master
    nothing to commit (working directory clean)

じゃあ、topic をマージしましょう。

    $ git merge topic
    Updating f8f801e..42e4d20
    Fast-forward
     A | 1 +
     1 file changed, 1 insertion(+)

マージの後、add するのかな、という話もありましたが、
ステータスを見ると、コミットするものもない。

    $ git status
    # On branch master
    # Your branch is ahead of 'origin/master' by 1 commit.
    #
    nothing to commit (working directory clean)

しかし、コミットしてよ、言われると思ったので、
一応、コミットしてみると、上と同じメッセージが出てくる。
もし、topic に問題があって、マージできないときはマージしないでおこう。

    $ git commit
    # On branch master
    # Your branch is ahead of 'origin/master' by 1 commit.
    #
    nothing to commit (working directory clean)

最後に master をプッシュしておく。

    $ git push
    Username for 'https://github.com': 
    Password for 'https://ndsuser1@github.com': 
    Total 0 (delta 0), reused 0 (delta 0)
    To https://github.com/ndsuser1/nds_repo.git
       f8f801e..42e4d20  master -> master
