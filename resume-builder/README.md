# 職務経歴書・履歴書 作成ツール

ブラウザで動く職務経歴書・履歴書の作成ツールです。  
入力内容はブラウザ内で完結し、サーバーに送信されません。

## 起動方法

### Docker Compose（推奨）

```bash
docker compose up -d
```

ブラウザで http://localhost:8080 を開く。

### Docker のみ

```bash
docker build -t resume-builder .
docker run -d -p 8080:80 resume-builder
```

### 停止

```bash
docker compose down
```

## 使い方

1. 上部タブで **職務経歴書** / **履歴書** を切り替える
2. 各項目を入力（職歴は「職歴を追加」で複数追加可）
3. **プレビュー** で確認
4. **PDFを生成** ボタンで HTML ファイルをダウンロード
5. ダウンロードした HTML をブラウザで開き、`Ctrl+P`（印刷）→「PDFに保存」を選択

## 構成

```
resume-builder/
├── index.html        # アプリ本体（単一ファイル）
├── nginx.conf        # nginx 設定
├── Dockerfile
├── docker-compose.yml
└── README.md
```
