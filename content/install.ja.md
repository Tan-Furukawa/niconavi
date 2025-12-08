+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'NicolNavi インストールガイド'
+++

# NicolNavi インストールガイド

## 必要なもの
- uv（Python のパッケージ管理ツール）
- Google Chrome（推奨）

## uv のインストール

### macOS / Linux
1. Terminal を開く。
2. `curl -LsSf https://astral.sh/uv/install.sh | sh` を実行する。
3. Terminal を閉じる。

### Windows（PowerShell）
1. PowerShell を開く。
2. `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"` を実行する。
3. PowerShell を閉じる。

## NicolNavi のセットアップ

1. https://github.com/Tan-Furukawa/niconavi_app を開く。
2. `Code` → `Download ZIP` をクリックし、ダウンロードした ZIP を任意の場所に展開する。

### macOS の場合
1. 展開した `niconavi_app` フォルダを右クリック → Service → New Terminal tab at Finder（などで Terminal を開く）。
2. Terminal で以下を実行する。

   ```
   chmod 777 ./run_niconavi_mac.sh
   ./run_niconavi_mac.sh
   ```

### Windows の場合
`run_niconavi_Windows.bat` をダブルクリックする。

- 必要な Python 環境が自動でインストールされます。インストール完了後、Google Chrome が自動で起動し NicolNavi が開始します。**初回は立ち上がりに最大 5 分ほどかかることがあります。Chrome 上で `This site can’t be reached`または`サイトが見つかりません` と表示されても、そのままお待ちください。**
- 次回以降も同じ手順で起動できます。2 回目以降はより早く立ち上がります。macの場合、`chmod 777 ./run_niconavi_mac.sh` のコマンドは初回のみで構いません。

## 手動での実行
- 依存関係のインストール: `uv sync`
- アプリの起動: `uv run python niconavi.py`
- アプリの URL: `http://localhost:8551/app`
