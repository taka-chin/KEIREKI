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

## 生成物の Git 管理

出力された HTML/PDF には氏名、住所、連絡先、職歴などの個人情報が含まれます。生成した履歴書・職務経歴書、確認用画像、一時ファイルは Git にコミットしないでください。ローカルで保管する場合は、リポジトリ外のダウンロード先や一時フォルダを使用してください。

テンプレートとして共有する PDF/HTML/TXT を追加する場合は、実在の個人情報や応募先情報を含めず、サンプルデータだけにしてください。

### 職務経歴書テンプレート

職務経歴書では PDF、HTML、TXT テンプレートをアップロードできます。PDF をアップロードした場合は、PDFを直接編集せず、同じ用途の白黒A4レイアウトで出力します。

HTML または TXT テンプレートでは以下のプレースホルダーを使用できます。

```html
{{today}}
{{name}}
{{nameKana}}
{{birthday}}
{{phone}}
{{email}}
{{address}}
{{contacts}}
{{summary}}
{{works}}
{{skills}}
```

例:

```html
<h1>職務経歴書</h1>
<p>{{today}}</p>
<h2>{{name}}</h2>
<section>{{summary}}</section>
<section>{{works}}</section>
<section>{{skills}}</section>
```

## 構成

```
resume-builder/
├── index.html        # アプリ本体（単一ファイル）
├── nginx.conf        # nginx 設定
├── Dockerfile
├── docker-compose.yml
└── README.md
```
