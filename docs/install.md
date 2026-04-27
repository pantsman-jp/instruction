## Git と Python のインストール

## 目次

1. [これは何](#1-これは何)
2. [前提条件](#2-前提条件)
3. [Git のインストールと設定](#3-git-のインストールと設定)  
    3.1. [インストール](#31-インストール)  
    3.2. [初期設定](#32-初期設定)
4. [Python のインストール](#4-python-のインストール)

## 1. これは何

Windows パッケージ マネージャー (`winget`) を使用して、開発に必要な `Git` および `Python` を効率的にインストール・設定する手順を説明します。

## 2. 前提条件

以下の環境および準備が必要です。
- **OS**: Windows 10 (1809以降) または Windows 11
- **ユーザー環境**: 日本語やスペースを含まない英数字のみのアカウント名
- **権限**: 管理者権限が使用可能であること
- **GitHub**: アカウント（無料）を所有していること

## 3. Git のインストールと設定

### 3.1. インストール

ターミナル（PowerShell または コマンド プロンプト）を開き、以下のコマンドを実行してください。

```PowerShell
winget install --id Git.Git --override "/VERYSILENT"
```

インストール完了後、設定を反映させるために**ターミナルを一度閉じてから再度開き**、以下を実行して確認します。

```PowerShell
git --version
```

`git version ...` と表示されれば正常にインストールされています。

### 3.2. 初期設定

Gitで使用するユーザー情報を登録します。以下のコマンドの `"` 内を自身の情報に書き換えて実行してください。

```PowerShell
git config --global user.name "GitHub ユーザー名"
git config --global user.email "GitHub 登録メールアドレス"
```

次に、GitHub との通信を安全に行うための SSH キーを作成します。

```PowerShell
ssh-keygen -t ed25519 -C "GitHub 登録メールアドレス"
```

保存場所等の確認が3回出ますが、すべて何も入力せずに `Enter` を押してください。
生成された公開鍵を以下のコマンドで表示し、出力された文字列をすべてコピーします。

```PowerShell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

#### GitHub への登録手順

1. [GitHub](https://github.com/) にログインします。
2. 右上のアイコンから `Settings` を選択します。
3. 左サイドメニューの `SSH and GPG keys` をクリックします。
4. `New SSH key` を押し、`Title` に PC名などを入力、`Key` 欄にコピーした文字列を貼り付けて `Add SSH key` を押します。

最後に、接続テストを行います。

```PowerShell
ssh -T git@github.com
```
`Hi ユーザー名! You've successfully authenticated...` と表示されれば成功です。

#### （推奨）メールアドレスの秘匿設定

公開リポジトリに個人のメールアドレスを出したくない場合は、GitHub の noreply アドレスを使用します。

1. [GitHub Email Settings](https://github.com/settings/emails) で「Keep my email addresses private」を有効にします。
2. 表示されている `ID+username@users.noreply.github.com` 形式のアドレスをコピーします。
3. 以下のコマンドを実行します。

```PowerShell
git config --global user.email "コピーしたアドレス"
```

## 4. Python のインストール

2026-04-27 での安定版である Python 3.14 系をインストールします。

```PowerShell
winget install --id Python.Python.3.14 -e --source winget
```

インストール後、新しいターミナルを開き以下のコマンドでバージョンを確認してください。

```PowerShell
python --version
```

---
Copyright (c) 2025-2026 [@pantsman](https://github.com/pantsman-jp)
