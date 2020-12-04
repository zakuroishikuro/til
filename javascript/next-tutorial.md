- import Link from 'next/link'
  - 内部リンクのときだけ付ける。外部リンクにはつけない。
  - Linkの中にaタグを入れる。classNameとかはaタグのほうにつける。

- import Head from 'next/head'
  - ページごとのtitleなどは`head`タグでなくNextで用意されてる`Head`タグに書く

- CSS-in-JS
  - styled-jsxがデフォルト
    - ```
      <style jsx>{`
        * {
          color: red;
        }
      `}</style>
      ```
    - 大かっことバッククォートで囲む

  - CSSモジュール
    - CSSファイルをReactコンポーネントの中でインポート出来るようになる
    - ユニークなクラス名を自動生成してくれる
    - 自動でコード分割してくれるのでCSSが最小限になる
    - ファイル名は`foo.module.css`の形式にしなければいけない

- pages/_app.js
    - すべてのページに共通するトップレベルのコンポーネント
    - グローバルなスタイリング等はここに記入。それ以外では不可能。
    - _app.jsを新しく作成したときは開発サーバの再起動が必要

- プリレンダリング
  - Next.jsは静的生成(Static Generation)とSSRを切り替え可能
  - 可能ならばいつでも静的生成推奨
  - 「このページをユーザーのリクエストに **先立って** プリレンダリングすることはできるだろうか？」
    - yes -> 静的生成
    - no -> SSR

- getStaticProps, getServerSideProps
  - プリレンダリングするページ内に外部データを読み込むときに使う
  - get **Static** Propsは静的生成、get **ServerSide** PropsはSSRで使う
  - ページでgetStaticPropsを作成するとその戻り値がexport default functionの関数に渡される
  - サーバサイドでのみ実行される
  - プリレンダリングする必要がない場合は普通にクライアントサイドレンダリングすればいい

- SWR
  - データフェッチ用のReactフック
  - クライアントサイド側でデータ取得する際にはこれを使うことが推奨される
  - キャッシング、再検証、フォーストラッキング、インターバルを開けた再フェッチなどに対応

- getStaticPaths (動的ルーティング)
  - ページのファイル名を `[hoge].js` という形式にし、getStaticPathsで以下のようなオブジェクトを返す
  - ```js
    {
      paths: [
        { params: {hoge: "foo"} },
        { params: {hoge: "bar"} },
      ],
      fallback: false
    }
    ```
  - `fallback`
    - falseなら、return されてないパスが404になる
    - trueなら、そのページのfallbackバージョンを提供する 

  - /foo/[...bar]
    - `/foo/a`, `/foo/a/b/`, `/foo/a/b/c` などすべてにマッチ
    - その場合はbarを配列で返さなきゃいけない

  - APIルート
    - ```js
      export default (req, res) => {
        res.status(200).json({ text: 'Hello' })
      }
      ```
    - getStaticProps, getStaticPathsから呼ぶべきではない。
      普通にサーバサイドで直接実行するコードを書くこと。
    - フォーム入力等で使うのが良い例