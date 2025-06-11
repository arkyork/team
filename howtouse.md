
##  なぜ GitHub を使うの？

* コードを置く "倉庫" と、議論する "掲示板" を 1 か所で運用できる
* 誰が・いつ・何を変更したか履歴が残るので、ミスしても元に戻せる
* Pull Request（PR）・Issue でレビュー&タスク管理ができる

##  最低限そろえておく設定

1. **リポジトリ作成** : README を自動生成し、`main` ブランチをデフォルトにする
2. **Collaborator** : *Settings → Collaborators* でメンバーを *Write* 権限以上で追加
3. **ブランチ保護** : *Settings → Branches* で `main` を *Require a pull request before merging* に設定（直接 push 防止）
4. **.gitignore** : キャッシュファイルや \*.ipynb などを除外

### 3. 作業の基本リズム（メンバー共通）

1. **必ずやっておきたいこと**

   ```bash
   git checkout main      # 必ず main に戻る
   git pull               # リモートの最新を取得
   ```
2. **機能ブランチを切る**

   ```bash
   git switch -c feature/ログインフォーム   # 命名規則は種類/概要
   ```
3. **開発する** : ファイルを編集・保存（失敗しても main には影響なし）
4. **変更をコミット**

   ```bash
   git add .
   git commit -m "add: #12 ログイン画面を作成"
   ```

   * メッセージ書式 : `<種別>: #Issue番号 要約`
   * 種別は `add / fix / update / remove` の 4 つ
5. **リモートへプッシュ**

   ```bash
   git push -u origin feature/ログインフォーム
   ```
6. **Pull Request を作成**

   * タイトル : `[feature/ログインフォーム] ログイン画面を作成`
   * 説明欄 : 何をしたか / 確認してほしい点 / Close したい Issue 番号
   * Reviewer を必ず指定
7. **レビュー＆修正**

   * `Files changed` タブでコメント → `Approve` か `Request changes`
   * 指摘を直したら再 push で自動更新
8. **マージ**（Squash & Merge 推奨）

   * レビュー OK → **Squash and merge** でコミット履歴を 1 つにまとめて main へ
9. **ローカル main を更新**

   ```bash
   git checkout main
   git pull --rebase
   ```

### 4. よく使う Git コマンドまとめ
| 状況                      | コマンド                                         |
| ----------------------- | -------------------------------------------- |
| いまどこのブランチにいるか確認したい      | `git branch`                                 |
| 途中変更を一時退避したい            | `git stash`                                  |
| 最新の main を作業ブランチに取り込みたい | `git pull --rebase`              |
| 間違えて違うブランチで作業した         | `git checkout ●●` → ブランチ切り直し |
| コミットをやり直したい             | `git commit --amend`                         |


### 5. まとめ

1. まず main に戻り最新化 → ブランチを切る
2. 小さくコミット・小さく PR でレビューしやすく
3. マージは Squash & Merge、一括でコミット整理
4. トラブルは stash / rebase / .gitignore で早めに対処
