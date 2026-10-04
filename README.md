# template-codesandbox-react19

Vite + React 19 + TypeScript のスターターテンプレートです。
CodeSandbox の Synced Template として利用することを想定しています。

## ローカルでの使い方

```bash
npm install
npm run dev
```

| コマンド          | 内容                         |
| ----------------- | ---------------------------- |
| `npm run dev`     | 開発サーバーを起動           |
| `npm run build`   | 型チェックと本番ビルド       |
| `npm run preview` | ビルド結果をローカルで確認   |
| `npm run lint`    | ESLint を実行                |

## CodeSandbox でテンプレートとして開く

このリポジトリを GitHub に push したあと、次の URL を開くと Synced Template が作成されます。

```text
https://codesandbox.io/p/sandbox/github/<owner>/<repo>
```

GitHub 側に push するたびに、テンプレートは次回アクセス時に自動で最新の内容に更新されます。
テンプレート自体は CodeSandbox 上では編集できないため、変更はこのリポジトリへの commit で行ってください。

テンプレートのタイトルや説明、タグは `.codesandbox/template.json` で設定しています。
テンプレート検索に公開したい場合は `published` を `true` にしてください。

### ブラウザ Sandbox として開くための設定

CodeSandbox は `vite` が依存関係にあると自動で VM Sandbox (Devbox) と判定します。
`sandbox.config.json` の `template` を `create-react-app-typescript` にすることで、
ブラウザ Sandbox として開かれるように上書きしています。

ブラウザ Sandbox では Vite 本体は動かず、CodeSandbox 内蔵のバンドラが `index.html` と
`src/main.tsx` を起点にビルドします。そのため次の点に注意してください。

- `vite.config.ts` の設定はブラウザ Sandbox では無視されます (ローカル開発では有効です)。
- `import.meta.env` など Vite 固有の機能はブラウザ Sandbox では使えません。
- VM Sandbox として開きたい場合は `sandbox.config.json` を削除してください。
