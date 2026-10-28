# VV Reporter スキル

vvsayコマンド（VOICEVOX）を使用して、作業の進捗状況や結果を音声で報告するClaudeスキルです。
読み上げキャラクターに合わせた口調で報告します。

## インストール

### 前提条件

- [vvsay CLI](https://github.com/petamorikei/voicevox-cli)がインストールされ、`vvsay --setup` で VOICEVOX CORE を導入済みであること
- vvsay の設定ファイル `~/.config/vvsay/config.toml` で `default_preset` が設定されていること

```bash
vvsay --list-presets   # (default) の付いたプリセットのキャラクターで読み上げます
```

### Claude Codeへの追加

`~/.claude/skills/`ディレクトリにコピー：
```bash
rsync -av --exclude='.git' --exclude='.DS_Store' . ~/.claude/skills/vv-reporter/
```

## 使い方

スキルをインストールすると、Claudeが作業中に自動的にvvsayコマンドで音声報告を行います。

```bash
# 使用例（ずんだもんの場合）
vvsay --bg --queue "ビルドを開始するのだ"
vvsay --bg --queue "テストが完了したのだ"
```

- `--queue` により、報告は呼び出した順に、重ならずに読み上げられます。
- キャラクターを変えるときは、vvsay の `default_preset` を変更します。スキルは読み込み時に vvsay の設定からキャラクターを調べ、そのキャラクターの口調ファイルを使います。

## キャラクターと口調

`characters/` に口調ファイルがあるキャラクター：

ずんだもん、四国めたん、春日部つむぎ、雨晴はう、波音リツ、冥鳴ひまり、九州そら、玄野武宏、白上虎太郎、青山龍星、もち子さん

それ以外のキャラクターは汎用の丁寧な口調（`characters/_generic.md`）で報告します。

口調ファイルは、[VOICEVOX 公式のキャラクター紹介](https://voicevox.hiroshiba.jp/dormitory/)と[キャラクターの呼称表](https://voicevox.hiroshiba.jp/dormitory/call_names/)を根拠にしています。
公式に語尾の指定がないキャラクターは、公式の人物像に合わせて報告用の口調を決めており、各ファイルにその旨を記載しています。

### キャラクターを追加する

`characters/<vvsay --list-narrator に表示される名前>.md` を作成します。既存のファイルと同じく、公式設定（出典付き）・報告での口調・例を書いてください。

## ファイル構成

```
vv-reporter/
├── SKILL.md                  # スキル定義（読み込み時に現在のキャラクターの口調を埋め込む）
├── README.md                 # このファイル
├── LICENSE                   # MITライセンス
├── scripts/voice-profile.sh  # vvsay の設定からキャラクターを調べ、口調ファイルを出力
└── characters/               # キャラクターごとの口調ファイル
    ├── _generic.md           # 専用ファイルがないときの汎用口調
    └── ずんだもん.md など
```

## ライセンス

[MIT License](LICENSE)

VOICEVOX の各キャラクターには、それぞれの利用規約があります。生成した音声を公開する場合は、各キャラクターの規約に従ってください。
