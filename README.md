nds_repo
========

書かれたとおりにやってみる。

    $ git clone https://github.com/ndsuser1/nds_repo.git
    $ touch README.md
    $ git init
    $ git add README.md
    $ git commit -m "first commit"
    $ git remote add origin https://github.com/ndsuser1/nds_repo.git
    $ git push -u origin master

ここで A B C を作る。（とりあえず、touch コマンドで空のファイルを）

    $ touch A B C

まだ、リポジトリには追加していない。

    $ git status
    # On branch master
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #       A
    #       B
    #       C
    nothing added to commit but untracked files present (use "git add" to track)

リポジトリに追加（add）して、同じようにステータスを見ると

    $ git add A B C
    $ git status
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #       new file:   A
    #       new file:   B
    #       new file:   C
    #

それじゃあ、stage されたファイルを commit しましょう。

    $ git commit -m 'add some files'
    [master c6c669d] add some files
    Your name and email address were configured automatically based
    on your username and hostname. Please check that they are accurate.
    You can suppress this message by setting them explicitly:
        git config --global user.name "Your Name"
        git config --global user.email you@example.com
    After doing this, you may fix the identity used for this commit with:
        git commit --amend --reset-author

名前とメアドを設定して、やり直しの機会をもらったので、
グローバルなオプションは変更せず、このリポジトリに設定しておく。

    $ git config user.name "YAMADA, Taro"
    $ git config user.email yamada.t@example.com

で、やり直し、作成者の名前も変更して、push する。

    $ git commit -m 'add some files' --amend --reset-author
    $ git push
