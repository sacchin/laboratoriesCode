# 概要
研究室時代のPlanKeeper関連のソースコードです。
日常的に蓄積したライフログをマイニングすることで、ユーザの移動特性を生成します。
上記の移動特性を利用することで、ユーザの行動をサポートするタイミングを高度化することが目的です。

# 構成
PlanKeeperが必要とするコンポーネントは以下の通りです。(説明するために、githubの一覧にないものも含んでいます。) 
* Android Logger Client（ALC）
  * クライアントアプリケーション
  * モバイル端末のGPSや加速度センサなどの情報を一定間隔でサーバに送信するコンポーネントです。
  * 同じ端末内のアプリケーションと協調するために、即自的な通知を端末内に送出します。
* LifelogMinigModule
  * サーバサイドアプリケーション
  * 蓄積されたライフログを定期的にマイニングし、行動特性を作成するコンポーネントです。
* CreatePlanServlet
  * サーバサイドアプリケーション
  * マイニングされた行動特性と、外部サービスを利用することで、移動プランを作成するコンポーネントです。
  * PlanKeeperからの要求に応える形で、移動プランを提供します。
* PlanKeeper
  * クライアントアプリケーション
  * 移動プランをサーバから取得し、ALCからの通知をもとにユーザの行動をサポートするタイミングを図るコンポーネントです。
  * サポートをするべきタイミングを検知したときに、同じ端末内のアプリケーションと協調するために、通知を端末内に送出します。
* TPOApplicationAPI
  * クライアントアプリケーション
  * 実際にサービスを提供するコンポーネントを作成する手助けとなるコンポーネントです。
  * これを利用することで、PlanKeeperで検知されたタイミングを取得し、イベント駆動で動作するアプリケーションを簡単に作成できます。
* DropInSiteMaker
  * サーバサイドアプリケーション
  * たくちゃん作であるコンポーネントです。
  * ユーザが立ち寄った場所を推定します。
* BehavioralRecognitionMaker
  * サーバサイドアプリケーション
  * nikenさん作であり、ずっきーが改良したコンポーネントです。
  * 移動中の移動手段を推定します。
# 雑多なコメント
* Android Studioが出る前のソースコードであるため、最新の環境でビルドは通らないと思います。
  * 再利用できるところとできないところを判断して、参考にしてください。（※言われるまではないと思いますがｗ）
* 察していただいていると思いますが、DropInSiteMakerとBehavioralRecognitionMakerは最新ではありません。
  * また、当人に最新版の在り処を聞いたほうがいいと思います。
* 最後に
  * 整理されていない + テストコードがない + ビルドが通らない + 動作検証していないと最悪の状態で渡してしまい申し訳ない！
