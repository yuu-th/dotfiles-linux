# yuuth-home-desk

このマシン全体に効く指示。**詳細な運用ルールは `~/bootstrap/CLAUDE.md` にある。**
ソフトの導入・システム設定・再構築に関わる話になったら、まずそれを読むこと。

## 応対

**日本語で応対する。**

## 環境

Ubuntu 26.04 LTS / niri 26.04 + DankMaterialShell（Wayland）/ NVIDIA GTX 1050 Ti（VRAM 4GB）/
HHKB Hybrid（US 配列）/ モニタ 1920x1080 × 2（片方は KVM で MacBook と共有）/ ロケール `en_US.UTF-8`

## 絶対に守ること

- **導入経路は apt / mise / OCI コンテナ / Flatpak の 4 つだけ。増やさない**
- `curl | sh` で個別ツールを入れない（mise の導入のみ例外）
- `sudo pip` / `sudo npm -g` を使わない
- 手で `/usr/local/bin` にバイナリを置かない
- **PPA を足したら / ポートを開けたら `~/bootstrap/LEDGER.md` に記録する**
- `~/.config/niri/dms/*.kdl` は DMS の自動生成物。**編集しない**
- 設定ファイルを変えたら `chezmoi add` して commit する。**git 管理下にない設定は存在しないものと見なす**

## 秘密情報

- dotfiles リポジトリ `yuu-th/dotfiles-linux` は **public**。**秘密情報を絶対に入れない**
- `~/.claude.json` は OAuth トークンを含む。**chezmoi に入れない**（`.chezmoiignore` で除外済み）
- このマシンは**ディスク暗号化なし**、**SSH 鍵にパスフレーズなし**（本人承知の判断）。
  平文で置く機密ファイルを増やさない

## sudo について

Claude の実行環境には **tty が無い**。sudo は tty 単位で認証をキャッシュするため、
ユーザーが別のシェルで `sudo -v` しても**共有されない**。sudo が必要な作業は次のどちらかにする。

1. ユーザーに `! <command>` で実行してもらう
2. スクリプトにまとめて `sudo bash <script>` を 1 回だけ依頼する

## 進め方

判断が要る場面以外は止めずに進める。ただし次は必ず止めて相談する。

- 想定と実機が食い違ったとき
- 削除・上書き・起動不能につながりうる操作
- 方針に反する選択をせざるを得ないとき

**問題が起きる前に仕組みを増やさない。**必要になってから作る。
