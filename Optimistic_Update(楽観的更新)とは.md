# Optimistic Update (楽観的な更新) とは

Optimistic Update(楽観的な更新)では、UIは、サーバーから実際の確認を受け取る前に変更が正常に完了したかのように動作します。エラーではなく、最終的に確認を取得することが楽観的です。これにより、より応答性の高いユーザーエクスペリエンスが可能になります。

![](./images/optimistic_update/overview.png)

# Optimistic Update 具体例

* GMailで送信した直後は一定期間後は取り消しできる
* Twitterのいいねボタンは いいね 直後は先にUIを更新してから非同期で更新をかけている

# Optimistic Update 実現方法

ReactQueryやReactApolloなどはオプティミスティックUIを簡単に実現するための機能を提供しています。

# 参考資料

* [楽観的なUIを備えたより良いUX](https://ichi.pro/rakkanteki-na-ui-o-sonaeta-yori-yoi-ux-259535728674360)
* [React Query で optimistic-update な UI を実装してみる](https://tech.studyplus.co.jp/entry/2021/05/18/100000)