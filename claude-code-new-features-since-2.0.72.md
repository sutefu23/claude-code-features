---
layout: default
title: "Claude Code 新機能一覧（2.0.72以降）"
---

[< サマリーに戻る](../)  

# Claude Code 新機能一覧（2.0.72以降）

2.0.73 〜 2.1.76 で追加（Added）された機能のみを抜粋。
Fixed / Improved の内容は含みません。

---

## 2.1.76

- MCP elicitation サポート — MCP サーバーがタスク実行中に構造化入力をインタラクティブダイアログ（フォームフィールドやブラウザ URL）で要求可能に
- `Elicitation` / `ElicitationResult` フックを追加。レスポンス送信前にインターセプト・オーバーライド可能
- `-n` / `--name <name>` CLI フラグでセッション起動時に表示名を設定可能
- `worktree.sparsePaths` 設定を追加。大規模モノレポで `claude --worktree` 使用時に必要なディレクトリのみを git sparse-checkout でチェックアウト可能
- `PostCompact` フック追加。コンパクション完了後に発火
- `/effort` スラッシュコマンドでモデルのエフォートレベルを設定可能
- セッション品質サーベイ — エンタープライズ管理者が `feedbackSurveyRate` でサンプルレートを設定可能

## 2.1.75

- Opus 4.6 で 1M コンテキストウィンドウをデフォルト有効化（Max, Team, Enterprise プラン）
- `/color` コマンドでプロンプトバーの色を設定可能
- `/rename` 使用時にプロンプトバーにセッション名を表示
- メモリファイルに最終更新タイムスタンプを追加
- フック確認プロンプトにフックソース（settings/plugin/skill）を表示

## 2.1.74

- `/context` コマンドにアクション可能な提案を追加 — コンテキスト消費の多いツール、メモリ肥大化、容量警告を特定し最適化ヒントを提示
- `autoMemoryDirectory` 設定でオートメモリの保存ディレクトリをカスタマイズ可能

## 2.1.73

- `modelOverrides` 設定でモデルピッカーのエントリをカスタムプロバイダーモデル ID（Bedrock 推論プロファイル ARN 等）にマッピング可能
- OAuth ログインや接続チェックで SSL 証明書エラー（企業プロキシ、`NODE_EXTRA_CA_CERTS`）が発生した場合のガイダンスを追加

## 2.1.72

- `/copy` で `w` キーを押すと選択内容をファイルに直接書き出し可能（SSH 環境で便利）
- `/plan` に説明引数を追加（例: `/plan fix the auth bug`）でプランモードに入り即座に開始
- `ExitWorktree` ツールで `EnterWorktree` セッションから離脱可能
- `CLAUDE_CODE_DISABLE_CRON` 環境変数でセッション中のスケジュール済みクロンジョブを即停止
- `lsof`, `pgrep`, `tput`, `ss`, `fd`, `fdfind` を bash 自動承認許可リストに追加
- `.git` サフィックスなしのマーケットプレイス git URL をサポート（Azure DevOps, AWS CodeCommit）

## 2.1.71

- `/loop` コマンドで定期的にプロンプトやスラッシュコマンドを実行可能（例: `/loop 5m check the deploy`）
- セッション内のクロンスケジューリングツールを追加
- `voice:pushToTalk` キーバインディングで音声アクティベーションキーを `keybindings.json` で再バインド可能（デフォルト: space）
- `fmt`, `comm`, `cmp`, `numfmt`, `expr`, `test`, `printf`, `getconf`, `seq`, `tsort`, `pr` を bash 自動承認許可リストに追加

## 2.1.69

- `/claude-api` スキルで Claude API と Anthropic SDK を使ったアプリケーション構築をサポート
- 空の bash プロンプト（`!`）で Ctrl+U により bash モードを終了可能
- インタビュー質問のオプション選択でテンキーをサポート
- `/remote-control` と `claude remote-control` にオプションの name 引数を追加
- 音声 STT で10の新言語をサポート（合計20言語）— ロシア語、ポーランド語、トルコ語、オランダ語、ウクライナ語、ギリシャ語、チェコ語、デンマーク語、スウェーデン語、ノルウェー語
- エフォートレベル表示（例: "with low effort"）をロゴとスピナーに追加
- `--agent` 使用時にターミナルタイトルにエージェント名を表示
- `sandbox.enableWeakerNetworkIsolation` 設定（macOS のみ）で MITM プロキシ使用時に `gh`, `gcloud`, `terraform` 等の TLS 証明書検証を許可
- `includeGitInstructions` 設定（および `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 環境変数）でビルトインのコミット・PR ワークフロー指示をシステムプロンプトから削除可能
- `/reload-plugins` コマンドでセッション再起動なしにプラグイン変更を反映
- macOS / Windows での Claude Code Desktop 提案の起動時プロンプトを追加（最大3回表示、却下可能）
- `${CLAUDE_SKILL_DIR}` 変数でスキルが自身のディレクトリを SKILL.md コンテンツ内で参照可能
- `InstructionsLoaded` フックイベント — CLAUDE.md や `.claude/rules/*.md` がコンテキストに読み込まれた時に発火
- フックイベントに `agent_id`（サブエージェント用）と `agent_type`（サブエージェントおよび `--agent` 用）を追加
- ステータスラインフックコマンドに `worktree` フィールド（name, path, branch, original repo directory）を追加
- `pluginTrustMessage` でプラグインインストール時の信頼警告に組織固有のコンテキストを付加可能
- Team プラン OAuth ユーザーにもポリシー制限取得（リモートコントロール制限等）を拡大
- `strictKnownMarketplaces` に `pathPattern` を追加し、ファイル/ディレクトリマーケットプレイスソースの正規表現マッチングをサポート
- プラグインソースタイプ `git-subdir` で git リポジトリ内のサブディレクトリを指定可能
- `oauth.authServerMetadataUrl` 設定で MCP サーバーのカスタム OAuth メタデータ検出 URL を指定可能

## 2.1.63

- `/simplify` と `/batch` バンドルスラッシュコマンドを追加
- `ENABLE_CLAUDEAI_MCP_SERVERS=false` 環境変数で claude.ai MCP サーバーの利用をオプトアウト可能
- HTTP フック追加 — シェルコマンドの代わりに URL に JSON を POST し JSON を受信可能
- MCP OAuth 認証時の手動 URL ペーストフォールバックを追加
- `/copy` ピッカーに「Always copy full response」オプションを追加

## 2.1.59

- `/copy` コマンドでコードブロックがある場合にインタラクティブピッカーを表示し、個別のコードブロックまたは全レスポンスを選択可能

## 2.1.51

- `claude remote-control` サブコマンドで外部ビルド用のローカル環境サーブを全ユーザーに提供
- npm ソースからプラグインをインストール時のカスタム npm レジストリと特定バージョンピニングをサポート
- `CLAUDE_CODE_ACCOUNT_UUID`, `CLAUDE_CODE_USER_EMAIL`, `CLAUDE_CODE_ORGANIZATION_UUID` 環境変数を追加

## 2.1.50

- LSP サーバーの `startupTimeout` 設定をサポート
- `WorktreeCreate` / `WorktreeRemove` フックイベントを追加
- エージェント定義で `isolation: worktree` をサポート
- `claude agents` CLI コマンドで設定済みエージェントを一覧表示
- `CLAUDE_CODE_DISABLE_1M_CONTEXT` 環境変数で 1M コンテキストウィンドウを無効化可能

## 2.1.49

- `--worktree` (`-w`) フラグで隔離された git worktree で Claude を起動可能
- Ctrl+F キーバインディングでバックグラウンドエージェントを終了（2回押し確認）
- `ConfigChange` フックイベント — セッション中に設定ファイルが変更された時に発火

## 2.1.47

- Stop / SubagentStop フック入力に `last_assistant_message` フィールドを追加
- `chat:newline` キーバインディングアクションで設定可能なマルチライン入力
- ステータスライン JSON の `workspace` セクションに `added_dirs` を追加

## 2.1.46

- claude.ai MCP コネクターを Claude Code で使用可能に

## 2.1.45

- Claude Sonnet 4.6 をサポート
- `--add-dir` ディレクトリからの `enabledPlugins` と `extraKnownMarketplaces` 読み込みをサポート
- `spinnerTipsOverride` 設定でスピナーのヒントをカスタマイズ可能
- SDK に `SDKRateLimitInfo` / `SDKRateLimitEvent` 型を追加

## 2.1.42

- 対象ユーザー向けに Opus 4.6 エフォートコールアウトを1回限り表示

## 2.1.41

- 別の Claude Code セッション内での Claude Code 起動を検出・防止するガードを追加
- OTel イベントとトレーススパンに `speed` 属性を追加
- `claude auth login`, `claude auth status`, `claude auth logout` CLI サブコマンドを追加
- Windows ARM64 (win32-arm64) ネイティブバイナリをサポート

## 2.1.33

- `TeammateIdle` / `TaskCompleted` フックイベントをマルチエージェントワークフロー向けに追加
- `Task(agent_type)` 構文でスポーン可能なサブエージェントを制限可能
- エージェントに `memory` フロントマターフィールドを追加（`user`, `project`, `local` スコープ）
- プラグイン名をスキル説明と `/skills` メニューに表示

## 2.1.32

- リサーチプレビューのエージェントチーム機能を追加（`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` が必要）
- メッセージセレクターに「Summarize from here」を追加し部分的な会話要約が可能

## 2.1.31

- 終了時にセッション再開のヒントを表示
- 日本語 IME からの全角スペース入力をチェックボックス選択でサポート

## 2.1.30

- Read ツールに PDF の `pages` パラメータを追加（例: `pages: "1-5"`）
- MCP サーバーの事前設定済み OAuth クライアントクレデンシャルをサポート（`--client-id`, `--client-secret`）
- `/debug` コマンドで現在のセッションのトラブルシューティングを支援
- 読み取り専用モードで追加の `git log` / `git show` フラグをサポート
- Task ツールの結果にトークン数、ツール使用回数、所要時間のメトリクスを追加
- 設定に reduced motion モードを追加

## 2.1.29

（Added 項目なし）

## 2.1.27

- ツール呼び出しの失敗・拒否をデバッグログに追加
- `--from-pr` フラグで特定の GitHub PR 番号または URL にリンクされたセッションを再開可能

## 2.1.23

- `spinnerVerbs` 設定でスピナーの動詞をカスタマイズ可能

## 2.1.21

- オプション選択プロンプトで日本語 IME からの全角数字入力をサポート

## 2.1.20

- vim ノーマルモードでカーソル移動不可時に矢印キーでヒストリナビゲーション
- ヘルプメニューに外部エディタショートカット（Ctrl+G）を追加
- プロンプトフッターに PR レビューステータスインジケータを追加
- `--add-dir` で指定した追加ディレクトリからの `CLAUDE.md` 読み込みをサポート（`CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1` が必要）
- `TaskUpdate` ツールでタスクの削除が可能に

## 2.1.19

- 環境変数 `CLAUDE_CODE_ENABLE_TASKS` を `false` に設定で旧システムを一時的に維持可能
- カスタムコマンドで `$0`, `$1` 等のショートハンドで個別の引数にアクセス可能

## 2.1.18

- カスタマイズ可能なキーボードショートカットを追加。コンテキスト別のキーバインディング、コードシーケンス、ワークフローのパーソナライズが可能。`/keybindings` で開始

## 2.1.16

- 依存関係トラッキング等の新機能を含む新タスク管理システムを追加

## 2.1.15

- npm インストールの非推奨通知を追加

## 2.1.14

- bash モード（`!`）でヒストリベースのオートコンプリートを追加 — 部分コマンドを入力して Tab で補完
- インストール済みプラグインリストに検索機能を追加
- プラグインを特定の git コミット SHA にピン留め可能

## 2.1.10

- `Setup` フックイベントを追加（`--init`, `--init-only`, `--maintenance` CLI フラグ経由でトリガー）
- ログイン時にブラウザが自動で開かない場合に 'c' キーで OAuth URL をコピー可能

## 2.1.9

- `auto:N` 構文で MCP ツール検索の自動有効化しきい値を設定可能（N はコンテキストウィンドウの割合 0-100）
- `plansDirectory` 設定でプランファイルの保存先をカスタマイズ可能
- AskUserQuestion の「Other」入力フィールドで外部エディタ（Ctrl+G）をサポート
- Web セッションから作成されたコミットと PR にセッション URL アトリビューションを追加
- `PreToolUse` フックが `additionalContext` をモデルに返却可能
- `${CLAUDE_SESSION_ID}` 文字列置換でスキルが現在のセッション ID にアクセス可能

## 2.1.7

- `showTurnDuration` 設定でターン所要時間メッセージを非表示に可能
- パーミッションプロンプト承認時にフィードバック提供が可能
- タスク通知にエージェントの最終レスポンスをインライン表示

## 2.1.6

- `/config` コマンドに検索機能を追加
- `/doctor` に Updates セクションを追加
- `/stats` コマンドに日付範囲フィルタリングを追加（`r` キーで切り替え）
- サブディレクトリのファイル操作時にネストされた `.claude/skills` ディレクトリからスキルを自動検出
- ステータスライン入力に `context_window.used_percentage` / `context_window.remaining_percentage` フィールドを追加
- Ctrl+G でエディタ起動失敗時のエラー表示を追加

## 2.1.5

- `CLAUDE_CODE_TMPDIR` 環境変数で内部一時ファイルの保存ディレクトリをオーバーライド可能

## 2.1.4

- `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` 環境変数でバックグラウンドタスク機能を無効化可能

## 2.1.3

- `/config` にリリースチャネル（`stable` / `latest`）トグルを追加
- 到達不能なパーミッションルールの検出と警告を追加（`/doctor` および保存後に警告表示）

## 2.1.2

- ターミナルにドラッグしたイメージにソースパスメタデータを追加
- OSC 8 対応ターミナル（iTerm 等）でツール出力のファイルパスをクリック可能なハイパーリンクに
- Windows Package Manager (winget) インストールをサポート
- プランモードで Shift+Tab で「auto-accept edits」を素早く選択
- `FORCE_AUTOUPDATE_PLUGINS` 環境変数でメインの自動アップデーターが無効でもプラグインの自動更新を許可
- SessionStart フック入力に `agent_type` を追加

## 2.1.0

- スキルのホットリロードを自動化 — `~/.claude/skills` や `.claude/skills` で作成・変更したスキルがセッション再起動なしで即座に利用可能
- スキルフロントマターの `context: fork` でフォークされたサブエージェントコンテキストでのスキル・スラッシュコマンド実行をサポート
- スキルに `agent` フィールドでエージェントタイプを指定可能
- `language` 設定で Claude の応答言語を設定可能（例: `language: "japanese"`）
- `respectGitignore` を `settings.json` でプロジェクト単位で @-mention ファイルピッカーの動作を制御
- `IS_DEMO` 環境変数で UI からメールと組織を非表示（配信・録画用）
- Bash ツールパーミッションでワイルドカードパターン `*` をサポート（例: `Bash(npm *)`, `Bash(git * main)`）
- Ctrl+B で bash コマンドとエージェントの両方を統一的にバックグラウンド化
- MCP `list_changed` 通知をサポート — 再接続なしで MCP サーバーのツール・プロンプト・リソースを動的に更新可能
- `/teleport` と `/remote-env` スラッシュコマンドを追加（claude.ai サブスクライバー向け）
- `Task(AgentName)` 構文で特定のエージェントを無効化可能
- エージェントフロントマターでフックをサポート（PreToolUse, PostToolUse, Stop）
- スキル・スラッシュコマンドフロントマターでフックをサポート
- 新しい Vim モーション: `;`, `,`, `y`, `yy`/`Y`, `p`/`P`, テキストオブジェクト（`iw`, `aw` 等）, `>>`, `<<`, `J`
- `/plan` コマンドショートカットでプロンプトから直接プランモードに入る
- 入力の任意の位置で `/` を入力するとスラッシュコマンドのオートコンプリートをサポート
- `--tools` フラグでインタラクティブモードで使用可能なビルトインツールを制限
- `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` 環境変数でファイル読み取りトークン上限をオーバーライド
- フックで `once: true` 設定をサポート
- フロントマターの `allowed-tools` フィールドで YAML スタイルリストをサポート
- プラグインからのプロンプトおよびエージェントフックタイプをサポート
- iTerm2 で Cmd+V による画像ペーストをサポート
- ダイアログのタブ切り替えに左右矢印キーナビゲーションを追加
- Ctrl+O トランスクリプトモードでリアルタイムの思考ブロック表示
- バックグラウンド bash タスク詳細ダイアログにファイルパスを追加
- Skills をコンテキストビジュアライゼーションで別カテゴリとして表示

## 2.0.74

- LSP（Language Server Protocol）ツールで go-to-definition, find references, hover documentation 等のコードインテリジェンス機能を追加
- `/terminal-setup` で Kitty, Alacritty, Zed, Warp ターミナルをサポート
- `/theme` で ctrl+t で構文ハイライトのオン/オフ切り替え
- テーマピッカーに構文ハイライト情報を追加
- macOS で Alt ショートカットがターミナル設定により動作しない場合のガイダンスを追加

## 2.0.73

- クリック可能な `[Image #N]` リンクで添付画像をデフォルトビューアーで開く
- alt-y yank-pop で ctrl-y yank 後にキルリング履歴を巡回
- プラグイン発見画面に検索フィルタリングを追加
- `--session-id` と `--resume` / `--continue` + `--fork-session` を組み合わせたカスタムセッション ID をサポート
