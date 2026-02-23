+++
date = '2026-02-23T20:01:22Z'
draft = false
title = 'Nec Ix2207'

tags = ['ネットワーク機器', 'NEC', 'IX2207', 'NetMeister']
categories = [ 'ネットワーク機器' ]
+++

最近、中古でNECのIX2207を購入しました。
NetMeisterというのでクラウド管理できるらしいので、試しに登録してみました。
まずは、NECの[NetMeisterのサイト](https://www.nw-meister.jp/service/login)にアクセスして、アカウントを作成します。

### Webサイトでのアカウント作成

右下の新規ユーザーアカウント作成をクリックして、必要な情報を入力します。

![ログイン画面画像](https://image.blog.pokapy.com/Login.png)

メアド、パスワード、名前、会社名、電話番号を入力して、利用規約に同意してメール送信をクリックします。
今回は個人利用なので、会社名は適当なものを入力しました。

![アカウント作成画面画像](https://image.blog.pokapy.com/Register.png)

メールに送られてきた認証コードを入力して、アカウントを作成します。

アカウントが作成できたら、ログインして、今度はグループを作成します。
先ほどと同様に右下の新規グループ登録をクリックして、必要情報を入力します。

![グループ選択画面画像](https://image.blog.pokapy.com/GroupSelect.png)

※に従ってそれぞれ入力して、登録ボタンを押下。
グループIDとパスワードはあとで必要になるので、覚えておきましょう。

![グループ作成画面画像](https://image.blog.pokapy.com/GroupRegister.png)

後は先ほど作ったグループを選択して、ようやくダッシュボード画面に入ることができました。

![ダッシュボード画面画像](https://image.blog.pokapy.com/Dashboard.png)

### デバイスの登録

今度は購入したIX2207を登録してみます。
CLIにアクセスして、以下のコマンドを実行します。

```bash
Router# conf t
Router(config)# nm ip enable
Router(config)# nm account <グループID> password plain <グループパスワード>
```

これで、デバイスの登録は完了です。
ダッシュボードに戻って、デバイスが登録されていることを確認

出来ませんでした・・・。

もしかしたらファームウェアが古すぎるのかも？

```
Router(config)# show version
NEC Portable Internetwork Core Operating System Software
IX Series IX2207 (magellan-sec) Software, Version 9.7.15, RELEASE SOFTWARE
Compiled Mar 13-Tue-2018 18:15:04 JST #2 by sw-build, coregen-9.7(15)
```

ファームウェアのバージョンは9.7.15でした。
今の最新が10.8.43なので、かなり古いですね。
ファームウェアをアップデートして、再度挑戦してみようかと思います。

[ファームウェアダウンロードページ](https://jpn.nec.com/univerge/ix/Download/ix2207/index.html)

上記のページから、最新のファームウェアをダウンロードして、アップデートを試みました。

```bash
Router# conf t
Router(config)# software-update tftp://<IP_ADDRESS>/ix2207-boot-18.1-gate-ms-10.8.43.rap
... 省略 ...
Router(config)# reload
```

再読み込み後、もう一度試してみると...

```
Router(config)# show nm information
NetMeister Client:
  Result      : Success (20000)
  Last Request: 2026/02/24 06:38:45
  Next Request: 2026/03/01 18:13:19 (remain 473668 sec)
```

お、成功してそう！
ダッシュボードに戻ってみると、無事にデバイスが登録されていました。
![ダッシュボード画面画像](https://image.blog.pokapy.com/Dashboard02.png)

これで、NetMeisterを使ってクラウド管理できるようになりました。
これホームゲートウェイにしようかなーと思っているので、色々と設定をいじってみようと思います。

### まとめ

- NECのIX2207をNetMeisterに登録するには、まずアカウントとグループを作成する必要がある。
- デバイスの登録はCLIから行う。
- ファームウェアが古いと登録できない可能性があるので、最新のファームウェアにアップデートすることをおすすめします。

参考資料

- https://souiunogaii.hatenablog.com/entry/nec-ix2215-netmeister
- https://note.com/noblehero0521/n/n090b1ae46af5
