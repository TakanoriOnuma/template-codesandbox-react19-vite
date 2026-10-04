# template-codesandbox-react19-vite

> **注意: このリポジトリは検証用の記録として残しているもので、テンプレートとしての採用は見送りました。**
>
> Vite + React 19 のプロジェクトを CodeSandbox のブラウザ Sandbox テンプレートとして
> 一から用意できるかを検証した結果、以下の制約があり実用には向かないと判断しました。
>
> - `vite` が依存関係にあると自動で VM Sandbox (Devbox) と判定されるため、
>   `sandbox.config.json` でブラウザ Sandbox に強制する必要がある。
> - ブラウザ Sandbox では Vite 本体は動かず、CodeSandbox 内蔵のバンドラが使われる。
>   `vite.config.ts` や `import.meta.env` など Vite 固有の設定・機能は無視される。
> - エディタ上で Vite 向けの型定義 (`vite/client` など) や `tsconfig` のプロジェクト参照が
>   解決されず、import に対する型エラーが多数表示される。プレビュー自体は動作する。
> - 最初に Devbox として開かれた Synced Template は、あとからブラウザ Sandbox に
>   切り替えてもテンプレート本体のプレビューが 503 のままになる (fork 先では正常に動く)。
>
> 本命のテンプレートは、CodeSandbox が提供している既存のブラウザ Sandbox テンプレートを
> ベースに React 19 へアップグレードする方針で別途作成します。

Vite + React 19 + TypeScript のスターターテンプレートです。
CodeSandbox の Synced Template として利用することを想定して作成しました。

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
https://codesandbox.io/p/sandbox/github/TakanoriOnuma/template-codesandbox-react19
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

### Synced Template の ID は最初の判定で固定される

Synced Template の ID は `owner/repo` のパスごとに最初にアクセスした時点で発行され、
そのときの判定 (ブラウザ Sandbox か VM Sandbox か) がプレビュー用ホストに紐づきます。
最初に Devbox として開かれたあとで `sandbox.config.json` を追加しても、
テンプレート本体のプレビューは VM 側を向いたまま 503 を返し続けました。

新しいリポジトリで Synced Template を作る場合は、最初に URL を開く前に
`sandbox.config.json` を push しておいてください。
