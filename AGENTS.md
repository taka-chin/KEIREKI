# Repository Guidelines

## Project Structure & Module Organization

このリポジトリは、nginx で配信する小規模な静的な職務経歴書・履歴書作成ツールです。

- `resume-builder/index.html`: HTML、CSS、JavaScript を含むアプリ本体。
- `resume-builder/nginx.conf`: コンテナで使う nginx 設定。
- `resume-builder/Dockerfile`: nginx イメージを作成し、アプリを配置する定義。
- `resume-builder/docker-compose.yml`: ローカル起動用の Compose 設定。
- `resume-builder/README.md`: 利用者向けの起動方法と使い方。

新しいアプリコードは、分割する明確な理由がない限り `index.html` に近い形で追加してください。画像やフォントなどの静的ファイルを追加する場合は `resume-builder/assets/` を使い、ルーティングやキャッシュの変更が必要なときだけ `nginx.conf` を更新します。

## Build, Test, and Development Commands

コマンドは `resume-builder/` で実行します。

- `docker compose up -d`: ビルドして `http://localhost:8080` で起動します。
- `docker compose down`: ローカルコンテナを停止します。
- `docker build -t resume-builder .`: Docker イメージを手動でビルドします。
- `docker run -d -p 8080:80 resume-builder`: 手動ビルドしたイメージを起動します。

軽微な静的変更は `index.html` をブラウザで直接開いて確認できますが、最終確認は Docker 経由で行い、nginx 設定も含めて動作を見てください。

## Coding Style & Naming Conventions

追加のビルドツールは、必要性が明確な場合だけ導入します。`index.html` の既存スタイルに合わせ、CSS は 2 スペース相当のインデント、CSS クラスは kebab-case、JavaScript の関数名は役割が分かる名前にします。共通の色や余白は `:root` の CSS カスタムプロパティへまとめます。UI 文言は日本語を維持し、短く具体的に書いてください。

## Testing Guidelines

この checkout には自動テストはありません。変更後は、職務経歴書・履歴書のタブ切り替え、フォーム入力、職歴の複数追加、プレビュー表示、HTML/PDF 生成フローを手動確認してください。スマートフォン幅とデスクトップ幅の両方でレイアウトを確認します。コンテナ関連を変更した場合は、`docker compose up -d` で起動し、`http://localhost:8080` が表示されることを確認してください。

## Commit & Pull Request Guidelines

現在の履歴は `initial commit` から始まっています。今後のコミットメッセージは、`feat: add export validation` や `fix: correct preview layout` のように、変更目的が分かる短い形式を推奨します。Pull Request には変更概要、UI 変更時のスクリーンショット、手動テスト結果、Docker/nginx への影響を記載してください。関連 Issue がある場合はリンクします。

## Generated Files & Git Management

アプリから出力した履歴書・職務経歴書の HTML/PDF、確認用スクリーンショット、一時レンダリング結果は原則として Git 管理しません。これらは個人情報を含む可能性が高いため、必要な場合はローカルの `tmp/` や OS のダウンロード先に置き、PR に含めないでください。テンプレートとして共有するファイルだけを追加する場合も、サンプル個人情報や実在の連絡先が残っていないことを確認してください。

## Security & Configuration Tips

入力された履歴書データはブラウザ内で完結する設計です。ネットワーク送信、解析タグ、外部スクリプトを追加する場合は、プライバシーへの影響を明記してください。生成した履歴書、個人情報、秘密情報、ローカル環境ファイルはコミットしないでください。
