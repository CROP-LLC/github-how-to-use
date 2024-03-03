# Git/GitHub講習会
本講習会では、開発にあたり必要となるGit/GitHubの基本的な役割と使い方を共有します。
細かな仕様や使い方は、開発の中で調べながら利用することを前提とします。

## そもそもGitとは
- 分散型のバージョン管理システム
    - 各開発環境に導入し、ファイルの変更履歴を記録する
    - ソースコードの変更を取り消したり、状態を複製して別のブランチで作業することができる
- 実は差分管理ではない[^1]（⁉）
    - コミットはスナップショット

### Gitの用語
| 用語 | 説明 |
| --- | --- |
| リポジトリ | ファイルやディレクトリの状態を記録する場所。<br/>**ローカルリポジトリ**：開発環境のリポジトリ<br/>**リモートリポジトリ**：GitHubなど |
| コミット | ファイルやディレクトリの状態を記録すること |
| ブランチ | 作業を分岐させること |
| マージ | ブランチの変更を取り込むこと |
| プルリクエスト | ブランチの変更を取り込むためのリクエスト |
| コンフリクト | 競合が発生した状態 |
| クローン | リモートリポジトリをローカルに複製すること |

## GitHubとは
- Microsoftが運営するGitリポジトリホスティングサービス
- リモートリポジトリのホスティング以外に、連携できるサービスが多い


### GitHub Organization
- GitHubの個人アカウントにリポジトリを作成する代わりに、組織のアカウントにリポジトリを作成することができる
- 所属メンバーの権限管理、複数人でのリポジトリ管理が容易になる

## 使ってみよう
ここからの説明は、Unix/Linux環境を前提にしています。Windowsの場合は、PowerShellを使用するか読み替えて進めてください。
### Gitの操作
1. リポジトリの作成
    ```bash
    mkdir sample-repo
    cd sample-repo
    git init
    ```
2. ファイルの追加
    ```bash
    echo "Hello, Git!" > hello.txt
    ```
3. コミット
    ```bash
    git add hello.txt
    git commit -m "Initial commit"
    ```
    > [!TIP]
    > コミットメッセージは、変更内容を簡潔に記述するとよいです。
    > どのように記述するか、チームでルールを決めておく事もあります。
4. ブランチの作成
    ```bash
    git branch develop
    git checkout develop
    ```
5. ファイルの変更
    ```bash
    echo "Hello, Git! (develop)" > hello.txt
    git add hello.txt
    git commit -m "Update hello.txt"
    ```
6. 履歴の確認
    ```bash
    git log
    ```
    > [!TIP]
    > お勧めのオプション付きコマンド
    > ```bash
    > git log --graph --name-only
    > ```
7. ブランチのマージ
    ```bash
    git checkout master
    git merge develop
    ```
    > [!WARNING]
    > マージ先のブランチでもコミットが行われている場合、マージ時にコンフリクトが発生することがあります。
    > コンフリクトが発生した場合は、手動で解消する必要があります。


### GitHub CLI （GitHubのコマンドラインツール）
GitHub CLIを使うと、GitHubの操作をコマンドラインで行うことができます。
1. GitHub上にリポジトリを作成
    ```bash
    gh repo create sample-repo --public
    ```
2. リポジトリのクローン
    ```bash
    gh repo clone sample-repo
    cd sample-repo
    ```
3. ファイルの追加
    ```bash
    echo "Hello, GitHub!" > hello-github.txt
    git add hello-github.txt
    git commit -m "Add hello-github.txt"
    ```
4. リモートリポジトリへのプッシュ
    ```bash
    git push origin main
    ```
> [!IMPORTANT]
> Gitのデフォルトブランチは`master`ですが、GitHubのデフォルトブランチは`main`です。
> 現在は`main`ブランチを使用する事が多いので、ローカルリポジトリを作成する場合には`main`ブランチを作成することをお勧めします。
> 何ならGitHub CLIを使ってリポジトリを作成するのがお勧めです。
5. ブランチの作成
    ```bash
    git branch develop
    git checkout develop
    ```
6. ファイルの変更
    ```bash
    echo "Hello, GitHub! (develop)" > hello-github.txt
    git add hello-github.txt
    git commit -m "Update hello-github.txt"
    ```
7. プッシュ
    ```bash
    git push origin develop
    ```





[^1]:https://github.blog/jp/2021-01-06-commits-are-snapshots-not-diffs/