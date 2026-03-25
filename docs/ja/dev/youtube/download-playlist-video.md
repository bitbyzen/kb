# プレイリスト動画を自動ダウンロードする方法

ChatGPTの回答は以下のとおり。

---

## ■ 目的

プレイリストに追加された動画を自動でダウンロードして、参考用ライブラリを作る。

---

## ■ 必要なもの

* yt-dlp（exe or インストール）
* プレイリストURL

---

## ■ 基本コマンド（完成版）

```bash
yt-dlp \
--download-archive archive.txt \
--format "bv*+ba/b" \
--merge-output-format mp4 \
--match-filter "!is_short & duration > 180" \
--write-thumbnail \
--write-info-json \
-o "videos/%(uploader)s/%(upload_date)s_%(title).80s.%(ext)s" \
PLAYLIST_URL
```

---

## ■ 何ができるか

* プレイリストの動画をすべてダウンロード
* 2回目以降は「新しい動画だけ」取得
* 高画質で保存（mp4）
* 投稿者ごとにフォルダ分け
* サムネ・メタデータも保存

---

## ■ 重要オプション

* `--download-archive archive.txt`
  → DL済み動画を記録（重複防止）

* `--match-filter "!is_short & duration > 180"`
  → Shorts除外 + 3分以上のみ

* `-o`
  → 保存形式（整理用）

---

## ■ 自動化（どちらか）

### Mac / Linux（cron）

```bash
crontab -e
```

例（3時間ごと）

```bash
0 */3 * * * /path/to/script.sh
```

---

### Windows

タスクスケジューラ

* トリガー：1時間 or 数時間ごと
* 実行：.bat ファイル

---

## ■ フォルダ構成例

```
videos/
  channelA/
    20260301_video-title.mp4
  channelB/
    20260302_video-title.mp4
archive.txt
```

---

## ■ 運用メモ

* プレイリストは用途別に分けると便利

  * ネタ用
  * 編集参考
  * サムネ研究
* 初回だけ大量DLになるので注意
* 定期実行すれば放置で増える

---

## ■ 最低限の流れ

1. yt-dlpを配置
2. コマンドをスクリプト化
3. cron or タスクスケジューラに登録

→ 完全自動で動画収集
