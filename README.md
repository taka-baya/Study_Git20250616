# Git勉強会 - コマンド一覧とガイド

**GitHub勉強会用 完全ガイド**

## 目次
1. [はじめに](#はじめに)
2. [基本的なLinuxコマンド](#基本的なlinuxコマンド)
3. [Git基本コマンド](#git基本コマンド)
4. [ブランチ操作](#ブランチ操作)
5. [リモートリポジトリ操作](#リモートリポジトリ操作)
6. [履歴とログ](#履歴とログ)
7. [実践的なワークフロー](#実践的なワークフロー)
8. [トラブルシューティング](#トラブルシューティング)

## はじめに

このガイドは、Gitを使った開発を学ぶための勉強会用資料です。基本的なコマンドから実践的な使い方まで、段階的に学習できるようにまとめています。

## 基本的なLinuxコマンド

Gitを使う前に、基本的なコマンドライン操作を覚えましょう。

### ディレクトリ操作

#### `pwd` - 現在のディレクトリを表示
```bash
pwd
# 出力例: /Users/username/Documents/projects
```
**用途**: 現在いる場所を確認したい時に使用

#### `ls` - ディレクトリの内容を表示
```bash
# 基本的な使用法
ls

# 詳細情報も表示
ls -l

# 隠しファイルも表示
ls -a

# 詳細情報と隠しファイルを両方表示
ls -la

# ファイルサイズを人間が読みやすい形式で表示
ls -lh
```
**用途**: フォルダ内のファイルやディレクトリを確認

#### `cd` - ディレクトリを移動
```bash
# 指定したディレクトリに移動
cd project-folder

# 一つ上のディレクトリに移動
cd ..

# ホームディレクトリに移動
cd ~
cd

# 前回いたディレクトリに戻る
cd -

# 絶対パスで移動
cd /Users/username/Documents
```
**用途**: 作業するディレクトリを変更

### ファイル操作

#### `mkdir` - ディレクトリを作成
```bash
# ディレクトリを作成
mkdir new-project

# 複数階層のディレクトリを一度に作成
mkdir -p projects/web-app/src
```

#### `touch` - 空のファイルを作成
```bash
touch README.md
touch index.html style.css script.js
```

#### `cp` - ファイルやディレクトリをコピー
```bash
# ファイルをコピー
cp file1.txt file2.txt

# ディレクトリを再帰的にコピー
cp -r folder1 folder2
```

#### `mv` - ファイルやディレクトリを移動・リネーム
```bash
# ファイルをリネーム
mv old-name.txt new-name.txt

# ファイルを別のディレクトリに移動
mv file.txt ../other-folder/
```

#### `rm` - ファイルやディレクトリを削除
```bash
# ファイルを削除
rm file.txt

# ディレクトリを再帰的に削除（注意して使用）
rm -rf folder-name

# 削除前に確認
rm -i file.txt
```

## Git基本コマンド

### 初期設定

#### ユーザー情報の設定
```bash
# グローバル設定（全リポジトリで使用）
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# ローカル設定（現在のリポジトリのみ）
git config user.name "Your Name"
git config user.email "your.email@example.com"

# 設定確認
git config --list
git config user.name
git config user.email
```

### リポジトリの作成と初期化

#### `git init` - 新しいリポジトリを初期化
```bash
# 現在のディレクトリをGitリポジトリとして初期化
git init

# 新しいディレクトリを作成してリポジトリを初期化
git init my-project
```

#### `git clone` - 既存のリポジトリをクローン
```bash
# HTTPSでクローン
git clone https://github.com/username/repository.git

# SSHでクローン
git clone git@github.com:username/repository.git

# 特定のディレクトリ名でクローン
git clone https://github.com/username/repository.git my-project
```

### 基本的な変更管理

#### `git status` - 現在の状態を確認
```bash
git status

# 短縮形式で表示
git status -s
```
**用途**: 変更されたファイル、ステージングエリアの状態を確認

#### `git add` - ファイルをステージングエリアに追加
```bash
# 特定のファイルを追加
git add filename.txt

# 複数のファイルを追加
git add file1.txt file2.txt

# 全ての変更を追加
git add .
git add -A

# 対話的に追加
git add -i

# パッチ単位で追加
git add -p
```

#### `git commit` - 変更をコミット
```bash
# コミットメッセージを指定してコミット
git commit -m "コミットメッセージ"

# エディタでコミットメッセージを作成
git commit

# ステージングとコミットを同時に行う（追跡済みファイルのみ）
git commit -am "コミットメッセージ"

# 前回のコミットを修正
git commit --amend

# 前回のコミットメッセージを修正
git commit --amend -m "新しいコミットメッセージ"
```

### ファイルの比較

#### `git diff` - 変更の差分を表示
```bash
# ワーキングディレクトリとステージングエリアの差分
git diff

# ステージングエリアと最新コミットの差分
git diff --staged
git diff --cached

# 特定のファイルの差分
git diff filename.txt

# 特定のコミット間の差分
git diff commit1 commit2
```

## ブランチ操作

### ブランチの基本操作

#### `git branch` - ブランチの管理
```bash
# ブランチ一覧を表示
git branch

# リモートブランチも含めて表示
git branch -a

# 新しいブランチを作成
git branch feature-branch

# ブランチを削除
git branch -d feature-branch

# 強制的にブランチを削除
git branch -D feature-branch

# ブランチ名を変更
git branch -m old-name new-name
```

#### `git checkout` - ブランチの切り替え
```bash
# ブランチを切り替え
git checkout feature-branch

# 新しいブランチを作成して切り替え
git checkout -b new-feature

# 特定のコミットをチェックアウト
git checkout commit-hash

# ファイルの変更を取り消し
git checkout -- filename.txt
```

#### `git switch` - ブランチの切り替え（新しいコマンド）
```bash
# ブランチを切り替え
git switch feature-branch

# 新しいブランチを作成して切り替え
git switch -c new-feature

# 前のブランチに戻る
git switch -
```

#### `git restore` - ファイルの復元（新しいコマンド）
```bash
# ワーキングディレクトリのファイルを復元
git restore filename.txt

# ステージングエリアから取り消し
git restore --staged filename.txt
```

### マージとリベース

#### `git merge` - ブランチをマージ
```bash
# 現在のブランチに他のブランチをマージ
git merge feature-branch

# マージコミットを作成せずにマージ（Fast-forward）
git merge --ff-only feature-branch

# 必ずマージコミットを作成
git merge --no-ff feature-branch
```

#### `git rebase` - ブランチをリベース
```bash
# 現在のブランチを指定したブランチにリベース
git rebase main

# 対話的リベース
git rebase -i HEAD~3

# リベースの続行
git rebase --continue

# リベースの中止
git rebase --abort
```

## リモートリポジトリ操作

### リモートリポジトリの管理

#### `git remote` - リモートリポジトリの設定
```bash
# リモートリポジトリ一覧を表示
git remote

# 詳細情報も表示
git remote -v

# リモートリポジトリを追加
git remote add origin https://github.com/username/repository.git

# リモートリポジトリのURLを変更
git remote set-url origin https://github.com/username/new-repository.git

# リモートリポジトリを削除
git remote remove origin
```

### データの同期

#### `git fetch` - リモートの変更を取得
```bash
# 全てのリモートブランチの情報を取得
git fetch

# 特定のリモートから取得
git fetch origin

# 特定のブランチのみ取得
git fetch origin main
```

#### `git pull` - リモートの変更を取得してマージ
```bash
# 現在のブランチに対応するリモートブランチから取得してマージ
git pull

# 特定のリモートとブランチを指定
git pull origin main

# リベースでプル
git pull --rebase
```

#### `git push` - ローカルの変更をリモートに送信
```bash
# 現在のブランチをリモートにプッシュ
git push

# 初回プッシュ時（上流ブランチを設定）
git push -u origin main

# 特定のブランチをプッシュ
git push origin feature-branch

# 全てのブランチをプッシュ
git push --all

# タグもプッシュ
git push --tags

# 強制プッシュ（注意して使用）
git push --force
git push --force-with-lease  # より安全な強制プッシュ
```

## 履歴とログ

### コミット履歴の確認

#### `git log` - コミット履歴を表示
```bash
# 基本的なログ表示
git log

# 一行で表示
git log --oneline

# グラフ形式で表示
git log --graph

# 全てのブランチのログを表示
git log --all

# 統計情報も表示
git log --stat

# 差分も表示
git log -p

# 最新のn件のみ表示
git log -n 5

# 特定の期間のログ
git log --since="2024-01-01" --until="2024-12-31"

# 特定の作者のログ
git log --author="username"

# コミットメッセージで検索
git log --grep="fix"
```

#### `git show` - 特定のコミットの詳細を表示
```bash
# 最新コミットの詳細
git show

# 特定のコミットの詳細
git show commit-hash

# 特定のファイルの特定のコミットでの状態
git show commit-hash:filename.txt
```

## 実践的なワークフロー

### 一般的な開発フロー

```bash
# 1. リポジトリをクローン
git clone https://github.com/username/project.git
cd project

# 2. 新機能用のブランチを作成
git checkout -b feature/new-feature

# 3. ファイルを編集後、変更をステージング
git add modified-file.txt

# 4. コミット
git commit -m "Add new feature functionality"

# 5. リモートにプッシュ
git push -u origin feature/new-feature

# 6. メインブランチに戻る
git checkout main

# 7. 最新の変更を取得
git pull origin main

# 8. 機能ブランチをマージ
git merge feature/new-feature

# 9. リモートにプッシュ
git push origin main

# 10. 不要になったブランチを削除
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

### プルリクエスト作業フロー

```bash
# 1. フォークしたリポジトリをクローン
git clone https://github.com/your-username/forked-repo.git

# 2. 元のリポジトリをupstreamとして追加
git remote add upstream https://github.com/original-owner/original-repo.git

# 3. 最新の変更を取得
git fetch upstream
git checkout main
git merge upstream/main

# 4. 新しいブランチで作業
git checkout -b fix/bug-fix

# 5. 変更をコミット
git add .
git commit -m "Fix critical bug in authentication"

# 6. フォークにプッシュ
git push origin fix/bug-fix

# 7. GitHubでプルリクエストを作成
```

## トラブルシューティング

### よくある問題と解決方法

#### コミットを取り消したい
```bash
# 最新のコミットを取り消し（変更は保持）
git reset --soft HEAD~1

# 最新のコミットを取り消し（変更も破棄）
git reset --hard HEAD~1

# 特定のコミットまで戻る
git reset --hard commit-hash
```

#### ファイルの変更を取り消したい
```bash
# ワーキングディレクトリの変更を取り消し
git checkout -- filename.txt

# ステージングエリアから取り消し
git reset HEAD filename.txt

# 新しいコマンド（推奨）
git restore filename.txt
git restore --staged filename.txt
```

#### マージコンフリクトの解決
```bash
# 1. コンフリクトが発生したファイルを確認
git status

# 2. ファイルを編集してコンフリクトを解決

# 3. 解決したファイルをステージング
git add resolved-file.txt

# 4. マージを完了
git commit
```

#### 間違ったブランチにコミットしてしまった
```bash
# 1. 現在のブランチから最新のコミットのハッシュをコピー
git log --oneline -1

# 2. 正しいブランチに移動
git checkout correct-branch

# 3. コミットを取り込む
git cherry-pick commit-hash

# 4. 元のブランチに戻って不要なコミットを削除
git checkout wrong-branch
git reset --hard HEAD~1
```

### 便利なエイリアス設定

```bash
# よく使うコマンドのエイリアスを設定
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'

# 使用例
git st    # git status と同じ
git co main    # git checkout main と同じ
git br    # git branch と同じ
```

## 参考資料

- [Pro Git Book](https://git-scm.com/book/ja/v2) - 公式ドキュメント
- [GitHub Docs](https://docs.github.com/ja) - GitHub公式ドキュメント
- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials) - 実践的なチュートリアル

## 練習課題

1. **基本操作**: 新しいリポジトリを作成し、ファイルを追加・コミット・プッシュしてみる
2. **ブランチ操作**: 機能ブランチを作成し、変更をコミット後、mainブランチにマージする
3. **コンフリクト解決**: 意図的にコンフリクトを発生させ、解決する練習をする
4. **履歴の修正**: コミットメッセージの修正やコミットの取り消しを練習する

---

このガイドを参考に、実際にコマンドを試しながら学習を進めてください。分からないことがあれば、`git help [command]` でヘルプを確認することもできます。