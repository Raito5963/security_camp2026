# Q.1 (応募のモチベーションについて)
後で記入。全体の内容と照らし合わせて3つほど

# Q.2 (これまでの経験について)
## (1) Web アプリケーションの設計・開発経験
Next.jsを使用して、さまざまなWebアプリケーションを開発したことがあります。
1. [単語帳アプリ](https://study-go.aokiju.com) (Study GO) <br />
私が高校3年生の春に開発した単語帳アプリです。<br />
1,2年生の頃、テスト勉強のためにGoogleスプレッドシートに単語と意味を書き連ねて、関数を組んでフラッシュカードを作っていましたが、非常に使いにくかったたのが開発のきっかけです。<br />
スプレッドシートの時よりも操作性を向上させ、データをCSVで取り込めるようにしました。
<br />もっと機能を紹介する。スタックも書く

2. [AI予定帳](https://planner.aokiju.com) (Command Planner)<br />
高校を卒業後に作成したスケジュールアプリです。<br />
GeminiAPIを利用して何か面白いことができないかなと考えていたところ、「予定帳にAIを取り込んだら面白いのでは？」と思い、開発を開始しました。<br />
基本的な機能は既存の予定帳アプリと同じで、予定を記入したりタスクを追加することができます。プロンプトバーに予定を入力するとAPIがGeminiを呼び、自動で予定を入力してくれます。たとえば、「次の16時から土曜日バイト」とか「今月末までにレポート提出」と入力すれば、最適な予定やタスクを追加してくれます。
<br />もっと機能を紹介する。スタックも書く

3. アンケートアプリ (FEEDO) <br />
高校生の時に参加した起業家育成プロジェクト及び高校三年生の頃の課題研究で開発したAIを導入したアンケートアプリです。詳しい内容は後述しますが、このアプリ開発で初めてチームでの開発を行い、自分はフロントエンドを担当しました。
<br />もっと機能を紹介する。スタックも書く

4. ToDoアプリ <br />
API連携の練習で作成しました。現在は停止中です。
<br />もっと機能を紹介する。スタックも書く

5. 掲示板アプリ (gaga friends)<br />
StartupWeekend 静岡 8thで開発したニッチな趣味の人とつながれる掲示板です。現在は停止中です。
<br />もっと機能を紹介する。スタックも書く

6. 会議議事録アプリ (Gymee) <br />
知人の起業を目指している同年代の人に頼まれて開発しました。<br />
基本的な機能はボイスレコーダーですが、会議を終了したときに録音したデータを基にAPIを使用しGeminiで分析、会議における評価を行います。
<br />もっと機能を紹介する。スタックも書く

## (2) パブリッククラウド技術の利用・構築経験
1. Github <br />
制作物はすべてこちらに保管しています。
[Raito5963](https://github.com/Raito5963)
2. Firebase <br />
開発でDBが必要になった時に初めて使用したDBです。
3. Supabase <br />
最近の開発でDBを使用するときはこれを使います。
4. Vercel <br />
自分が開発したWebサイトやWebアプリはすべてこれで公開しています。

## (3) 一般のプログラミングの経験やチームでの開発経験
### a.プログラミング言語
私が経験したことがあるプログラミング言語と、その用途です。
| 言語 | 用途 |
| ---- | ---- |
| TypeScript | Web開発 |
| Python | CTF, レーシングアシスタントAI, ルービックキューブなど |
| C | 高校の授業で学習。まだ使用したことはない。 |
| C# | 高校の授業で学習。デスクトップアプリやUnityで利用。 |
| C++ | 高校の部活で学習。競技プログラミングで利用。 |

### b.チーム開発
高校三年生の課題研究の際に私を含めた4人グループで前述のAIを導入したアンケートアプリを開発しました。私はフロントエンドを担当しました。

## (4) コンテナ技術の利用経験
コンテナ技術はアプリケーションを実行するために必要なプログラムやライブラリをパッケージとしてまとめ、どこでも同じように動かせるようにする技術であるということは理解していますが、利用経験はありません。コンテナ技術の代表例として実行環境(コンテナエンジン)ではDocker、管理運用面(コンテナオーケストレーション)ではK8s(Kubernetes)があることも存じております。

# Q.3 (あなたの興味・関心について)

# Q.4 (Webに関する脆弱性・攻撃技術の検証)
## 7 - Next.js, cache, and chains: the stale elixir

今回の脆弱性はCVE-2024-46982で登録されています。以下、CVEで表記をすることがあります。

### (1) 選んだ理由
普段Next.jsを使用してWeb開発を行っているから。

### (2) 事例の概要
| 項目 | 詳細 |
| ---- | ---- |
| CVE | CVE-2024-46982 |
| CVSS | 7.5 |
| Product | Next.js |
| Versions | >= 13.5.1, < 13.5.7 または >= 14.0.0, < 14.2.10 |

CVE-2024-46982はNext.jsにおけるキャッシュポイズニングの脆弱性。本来キャッシュ不可のSSR(Server Side Rendering)ページを誤ってキャッシュ可能と判断してしまうNext.js内部の挙動によるもの。<br />
HTTPリクエストを細工することでPagesRouter内の非動的なSSRのキャッシュを汚染することが可能。ただし、AppRouterには影響しない。<br />
以下のすべての条件を満たす場合に影響を受けます。
1. Versionが上記の範囲内であること。
2. PagesRouterを使用していること。
3. 非動的なSSRルートを使用していること。

上記を満たすNext.jsアプリケーションでは以下のような悪用が報告されている。
- DoS<br/>
キャッシュ汚染により、対象ページのHTMLではなく無意味なJSONオブジェクトが返されてしまい、利用者ページ内容を閲覧できなくなる。攻撃者が定期的にキャッシュを汚染し続ければ該当ページは事実上ダウンした状態になる。
- SXSS(ストアドクロスサイトスクリプティング)<br />
SSRページがユーザのリクエスト情報を埋め込んでいる場合、その部分にスクリプトを仕込んでキャッシュさせることで悪意のあるスクリプトを含んだHTMLを配信できる。一度キャッシュに載るだけで、次にそのページにアクセスしたユーザのブラウザで実行されてしまう。
- 機密情報の漏洩<bt />
SSRページがログインユーザの固有データを表示する場合、キャッシュ汚染によってほかのユーザにデータが表示されてしまう恐れがある。管理者が閲覧されるしたページが汚染されると、不特定多数にデータが漏洩する可能性がある。
- その他副次被害<br>
汚染により、HTTPステータスコードまで汚染される例も発生している。攻撃リクエストで500 Internal Server Error(サーバー側で予期せぬ問題が発生し、リクエストを処理できなかったことを示すステータス)を発生させてキャッシュさせることで以降もそのページがそのエラーを返すといった現象も確認されている。

手法は後述しますが、攻撃難易度は低くかつ結果は深刻であるため、CVSSは7.5の高深刻度に分類されている。

### (3) 攻撃手法の詳細
> できればダミーサイト作って実験したい
> →既に修正済みだと思われるので何とか考える

CVE-2024-46982の詳細を説明する前に説明するために重要な2つの関数の役割を理解する必要がある。2つの関数にはどちらもターゲットページに情報を送信するという重要な共通点がある。
#### getServerSideProps - SSR
> getServerSideProps is a Next.js function that can be used to fetch data and render the contents of a page at request time. (Next.js)

リクエストを行ったユーザのデータ(Cookie, header, URLパラメータ)などの要素に基づいてリクエスト時のみに利用可能なデータを送信する。

##### コード例
```typescript
import type { InferGetServerSidePropsType, GetServerSideProps } from 'next'
// 型の定義(Githubデータに含まれている要素を定義)
type Repo = {
  name: string
  stargazers_count: number
}

// サーバでのデータ取得
/*
このページをリクエストするたびに必ずサーバ上で動く。
fetchでNext.jsのリポジトリ情報を取得。
returnでrepoがPageコンポーネントに自動的に渡される。
satisfiesはNext.jsのSSR用関数のルールに従っていることを証明している。
*/
export const getServerSideProps = (async () => {
  const res = await fetch('https://api.github.com/repos/vercel/next.js')
  const repo: Repo = await res.json()
  // Pass data to the page via props
  return { props: { repo } }
}) satisfies GetServerSideProps<{ repo: Repo }>

// 画面の表示
/*
repoにgetServerSideProps()で取得したデータが入る。
InferGetServerSidePropsTypeはgetServerSideProps()が何を返すかを自動で読み取りrepoに型を付けてくれる。
pタグでGithubのリポジトリのスター数を出力。
*/
export default function Page({
  repo,
}: InferGetServerSidePropsType<typeof getServerSideProps>) {
  return (
    <main>
      <p>{repo.stargazers_count}</p>
    </main>
  )
}
```

#### getStaticProps - SSG(静的サイト生成)
> If you export a function called getStaticProps (Static Site Generation) from a page, Next.js will prerender this page at build time using the props returned by getStaticProps. (Next.js)

ビルドプロセス中にすでに利用可能なデータ(ユーザリクエストに関連しないデータ)を送信することを可能にする関数。性質上、公開キャッシュされることを目的としている。

##### コード例
```typescript
import type { InferGetStaticPropsType, GetStaticProps } from 'next'
// 型の定義(Githubデータに含まれている要素を定義)
type Repo = {
  name: string
  stargazers_count: number
}
// ビルド時の仕込み
/*
getServerSidePropsと異なり、ビルド時のみに実行される。
アクセスした時点ですでにHTMLが出来上がっているので高速で表示できる。
APIサーバに負荷がかからない。
*/
export const getStaticProps = (async (context) => {
  const res = await fetch('https://api.github.com/repos/vercel/next.js')
  const repo = await res.json()
  return { props: { repo } }
}) satisfies GetStaticProps<{
  repo: Repo
}>
// 画面の表示
/*
ビルド時に取得したrepoデータ使い表示する。
*/
export default function Page({
  repo,
}: InferGetStaticPropsType<typeof getStaticProps>) {
  return repo.stargazers_count
}
```

#### データ取得
以下のようなコードはリクエストのユーザーエージェントを取得し、ページに渡す。
```typescript
export async function getServerSideProps(context: GetServerSidePropsContext) {
  const userAgent = context.req.headers['user-agent'];
  return {
    props: {
      userAgent, 
    },
  };
}
```
上記2つの関数のいずれかを使用する場合、Next.jsではデータ取得のために特定のルートを使用する。
`/_next/data/{buildID}/targeted-page.json`
- buildID: ビルドごとに生成される一意の識別子。
- targeted-page: データが取得されるページの名前。
pagePropsレスポンスは、送信データを含むJsonである。
> 上記コードの実行結果の画像を張る

#### 攻撃手法 - キャッシュポイズニングを利用したDoS攻撃
1. キャッシュキーの盲点を突く<br />
多くのキャッシュシステム(CDNなど)は、効率化のためにURLのパラメータを無視してデータを保存する設定になっている。
- リクエストA: `example.com/?__nextDataReq=1`
- リクエストB: `example.com`
キャッシュサーバーから見るとこの2つは同じページの世急だと認識されることを前提として攻撃を行う。
2. ポイズニング<br />
攻撃者はあえてパラメータ付きのURL(パラメータA)を送る。すると、Next.jsのサーバは`__nextDataReq`を認識し、HTMLではなくJSONデータ(pageProps)の生データ
を返す。(後述)
3. キャッシュの書き換え<br />
キャッシュサーバは、サーバから送られてきたJSONデータを受け取るが、パラメータは無視するため、`example.com`の正しいデータとして保存してしまう。
4. 発動<br />
その後、一般ユーザが普通に`example.com`(リクエストB)にアクセス。キャッシュサーバは保存したデータ(JSON)をHTMLの代わりに返してしまう。その結果、本来であればHTMLページが表示されるが、これによりJSONデータが表示される。ユーザはページを表示できなくなり、キャッシュが削除されるまでサービス停止と同等の状態に陥る。

##### 補足
Next.jsの内部([server/base-server.ts](https://github.com/vercel/next.js/blob/canary/packages/next/src/server/base-server.ts))にリクエストによってHTMLを返すかJSONを返すか判定するロジックがある。以下はそのロジックを抜粋したもの。
```typescript
// Next.js /server/base-server.ts:2123
if(
    hasFallback ||
    staticPath?.includes(resolvedUrlPathname) ||
    // this signals revalidation in deploy environments
    // TODO: make this more generic
    req.headers['x-now-route-matches']
){
    isSSG = true
} else if (!this.renderOpts.dev) {
    isSSG ||= !! prerenderManifest.routes[toRoute(pathname)]
}
```
通常、Next.jsはリクエストに対して以下のように振る舞う。
- SSR: リクエストごとに内容が変化するので、キャッシュさせない(Cache-Control: private)
- SSG: 内容が固定なので、キャッシュさせる(Cache-Control: s-maxage=...)

上記のロジックにある`req.headers[x-now-route-matches]`は本来、デプロイ環境で再検証を行うための内部的な信号だが、外部からこのヘッダーを送り付けると、コード上の`isSSG = true`が強制的に発動する。これにより、サーバは静的だと勘違いし、本来付与してはいけないs-maxage(キャッシュの有効期限)を付与してしまう。<br />
さらにパラメータとして`__nextDataReq=1`を加えると、[server/base-server.ts](https://github.com/vercel/next.js/blob/canary/packages/next/src/server/base-server.ts)の`handleNextDataRequest`(686行~775行)メソッドが稼働する。`isSSG`の判定と組み合わさることでサーバはSSGページ用のJSONデータを生成し、それをキャッシュしてよいというヘッダーをつけて返信してしまう。


### (4) その他事例に関して感じたこと・気が付いたこと
### 出典
- [Rachid Allam - zhero; Next.js, cache, and chains: the stale elixir](https://zhero-web-sec.github.io/research-and-things/nextjs-cache-and-chains-the-stale-elixir)
- [れおりん(@reoring) - Qiita; Next.jsのキャッシュ機構と CVE-2024-46982 技術詳細レポート](https://qiita.com/reoring/items/7b5a48022d5918a16ac5)
- [CVE-2024-46982
](https://www.cve.org/CVERecord?id=CVE-2024-46982)
- [Next.js; getStaticProps](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-static-props)
- [Next.js; getServerSideProps](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-server-side-props)
