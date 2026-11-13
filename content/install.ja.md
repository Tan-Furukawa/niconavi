+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'NicolNavi インストールガイド'
+++

# NicolNavi インストールガイド

[GitHub Releases](https://github.com/Tan-Furukawa/niconavi_app/releases) から、お使いの環境に合ったファイルをダウンロードしてください。

## Windows

`NicoNavi-Setup.exe` をダウンロードして実行し、インストーラーの案内に従ってください。

## Linux（x86_64 AppImage）

`NicoNavi-<version>-x86_64.AppImage` をダウンロードし、Terminal で実行権限を付けて起動します。

```bash
chmod +x NicoNavi-*-x86_64.AppImage
./NicoNavi-*-x86_64.AppImage
```

## Python（macOS・その他の環境）

[uv](https://docs.astral.sh/uv/) と Git をインストールし、Terminal または PowerShell で次を実行します。この方法は Windows と Linux でも利用できます。

```bash
git clone https://github.com/Tan-Furukawa/niconavi_app.git
cd niconavi_app
uv sync --frozen
uv run python niconavi.py
```
