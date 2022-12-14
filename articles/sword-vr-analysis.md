---
title: "剣戟VRゲームの分析"
emoji: "⚔"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["個人開発", "Meta Quest", "VR", "死にゲー", "ゲーム開発"]
published: true
---

# 概要

今後 VR の死にゲーを開発したいと考えており、まず参考として他の VR ゲームがどのようなものなのかを参考までにプレイしたのでまとめました。

イメージとしては、剣戟のアクションの難易度が高いゲームを想定しているため、剣戟が細かそうなゲームを選定しました。

# 現状の剣戟 VR ゲームの分析

## Swordsman

https://www.oculus.com/experiences/quest/4478419005520485/

https://www.youtube.com/watch?v=CiAwMr7BQBo

- 良い点

  - 相手の剣や体に剣が触れた際に自分のコントローラが震えてわかるようになっています
  - ダメージを受けると画面が暗くなってわかるようになっていて、明るくなると回復していることが分かります
  - 敵にダメージを与えた際に敵がうめき声をあげるため、剣にぶつかったときと区別ができます
  - 複数の敵が出てくるとぐっと難易度が上がります

- 自作で省みたい点

  - 相手の剣に自分の剣があたってしまう効果範囲が広く、なかなか敵にダメージを与えられません
  - 敵が自分を攻撃できる条件がよくわからないため、気づかないうちにやられてしまいます
  - 単調な敵の出現の繰り返しのため、飽きがすぐ来ます
  - チュートリアルが無いため、敵をどのような流れで倒すのか全くわからず何回も死ぬことになります

## Zenith: The Last City

https://www.oculus.com/experiences/quest/3594982710558708

https://www.youtube.com/watch?v=na1q8XVpuoo

キャラ作成時に近距離攻撃と遠距離攻撃を選択することができ、近距離攻撃を試しました。

- 良い点

  - 左手のスティックで移動している際に、頭を向けてる方向に動くことができます
  - 右手のボタンを押すとダッシュができて、移動がラクです
  - ダッシュが連続でできないようになっており、危なくなってもすぐに敵から離れられないため、緊迫感があります
  - 左手の甲に目的地が表示された地図が表示されているのがわかりやすかったです
  - 攻撃がヒットした際にダメージが表示されるため、どんな攻撃が効くのかがわかりやすかったです
  - 連続して剣を振ると大きなダメージが与えられないようになっているため、単調な攻撃になりません

- 自作で省みたい点

  - 右手のスティックを動かして視点移動した際に際に視点が変わる幅が大きいため、戦闘では使いにくいです
  - 剣を振らなくても当たり判定があるので、斬るのではなくくすぐるような動きになります

## ALTAIR BREAKER

https://www.oculus.com/experiences/quest/4599090550122539/

https://www.youtube.com/watch?v=zobp2bL-SnY

- 良い点

  - 両手を頭上に挙げてトリガーボタンを押すことでグライダーが出現し、離れたところに移動することができ、ジャンプも兼ねています
  - チュートリアルが非常に丁寧で操作方法がしっかり把握できました
  - 目の前に表示されたパネルをタッチすると決定できる UI がわかりやすかったです
  - 移動方法や攻撃方法のチュートリアルがとても丁寧でした

- 自作で省みたい点

  - 敵の動きが激しいため、自分と重なって前が見えなくなったり視界から消えてストレスになります
  - ステージ内に離れ小島のようなところがあり、そこに敵が出現すると遠いところまで行かなければならないのでストレスになります
  - 爽快感につながるはずの打ち上げアクションがなかなか発生しないため、フラストレーションになります
  - 手を結構ひねらないと盾が正面を向かないため、違和感がありました

## Blade & Sorcery: Nomad

https://www.oculus.com/experiences/quest/2031826350263349/

サンドボックスモードにおいて、他のステージに移動できることに気づかなかったため、後ほど再度遊びたいと思います
以下の動画が概要の把握のために良かったです。

https://www.youtube.com/watch?v=raVBa1SWvVg

- 良い点

  - 右手のボタンを押してしゃがみながら近づくことで、背後からサイレントキルができます
  - ボタンを押すことで離れたところの武器を引き寄せることができるため、かがむ必要がなく体に負担があります
  - 引き寄せは武器だけでなく、縄に下がっているランタンを引き寄せることで縄を引き寄せて対岸に渡ることができます
  - 腰のあたりで武器を離すことで武器をしまうことができ、再度腰のあたりでつかみを行うことで武器を再度持つことができ、色々な武器を持てます
  - 腰のあたりだけでなく背中にも持つことができるようです
  - 剣だけでなく、メイスや槍や弓のように多彩な武器があります
  - 強く武器を振るとダメージが多くなるようになっており、強く武器を振る動機が生まれていました

- 自作で省みたい点

  - 崖登りの際になかなか崖をつかめず、崖を登るのが難しいです

## Battle Talent

https://www.oculus.com/experiences/quest/4410602018966965/

https://www.youtube.com/watch?v=rnhaeCoSDRk

今のところ最も作りたいゲームのイメージに近いものでした。

- 良い点

  - 敵の攻撃パターンが左右の攻撃だけでなく、身長の低いゴブリンが足元を狙ってきたり爆弾を投げてきたりと多彩であるため食らってしまうかもしれないというドキドキがあります
  - 敵が複数出てきて囲まれると、やられてしまうかもしれないという死闘感があります
  - プレイヤーのヒットポイントが低いため、すぐにやられてしまい緊張感があります
  - 攻撃を当てた際に振動があり、リアル感があります
  - ダンジョンでは角から敵が出てくる緊張感があります
  - 首を斬ると、うまくあたると首が飛んで一撃で相手を倒せるため攻撃を工夫する余地があります
  - 武器を投げて遠くの敵を攻撃することができます
  - 敵の攻撃に強く武器を当てるとパリィをすることができるため、防御に工夫が出ます
  - 武器に耐久力があり、無限に攻撃を受け続けたりできず緊迫感があります
  - 逆手持ちができるため、守るように武器を構えることができて盾がいらないです
  - 両腕を腕を軽く振ると走れるので
  - つかんでトリガーを引くと能力値が上がるアイテムがダンジョン内にあり、
  - 腕を振りかぶってジャンプすると高く飛べるなど、現実に沿った動きができます
  - 両手持ちができ、両手持ちをすると攻撃の威力が上がります
  - 武器を腰などにしまった際に振動があるため、しっかりしまえていることを見ないでも確認できます

- 自作で省みたい点

  - 剣戟 VR 全般なのですが、武器を握りっぱなしにしていると指が痛くなってくるため一度押すと離しても武器を持ち続けられると指が痛くなくなると考えます
  - 大勢に囲まれた際に素早くその場を離れられないため、大勢に囲まれたときはすぐに囲まれてやられてしまいます

## レジェンダリーテイルズ

https://store.steampowered.com/app/1465070/_/

かなり良さそうなのですが、Meta Quest 2 に対応していないためプレイができません。
下記の動画で把握することができそうです。

https://www.youtube.com/watch?v=QQx1rx7MHc0

- 良い点
  - 3 人称視点は周りを見渡せて戦いやすいです
  - パリィが敵の攻撃に対して直角に当てる必要があり、難易度が高くなっています

## Vader Immortal: エピソード I

https://www.oculus.com/experiences/quest/2108775495884888

https://www.youtube.com/watch?v=jc3ej0tc3a8

- 良い点

  - 戦闘時の迫力がとにかくすごく、呼吸が浅くなるほどの緊張感があります。自分が求めていたのはこれだと感じました。
  - リアルより少し下の視点になるように調整されているようで、敵が見上げるように巨大になるので圧迫感を感じることができました
  - 戦闘時は自分が足を動かさなくて良い工夫がされていました。例えば敵が目の前に立ってライトセーバーを振ってくるので、それを何度か受けてからこちらが攻撃をできるようになっています
  - 敵の遠距離攻撃であるブラスターはライトセーバーをピッタリと合わせることで敵に弾き返し、敵を倒せるようになっています。止めて当てないといけなかったり、少しでも外してしまうとダメージを受けるなどシビアになっています
  - 複数の敵が立ちはだかることで難易度が上がるようになっていました。視界外に敵がいる際も攻撃前に敵が声や音を出してくれるので親切でした
  - これまで両手を使う剣戟ゲームを多く遊んできましたが、今作のように片手だけで剣を動かすアクションでも意外と満足感がありました（左手は今後フォースを使うために空いているのかもしれないですが）
  - 腰に下げるアイテムがライトセーバーとギミックを動かすための道具の 2 種類でシンプルであることも良かったです
  - サポートキャラが操作するべき内容を説明してくれるので、チュートリアルを設ける必要がなくなっていました
  - Quest2 で設定している境界が狭いとゲーム起動時に警告が表示されて親切でした。実際、警告が出ている状態でプレイすると壁に手があたってしまったりしました
  - VR 酔い対策のため、デフォルトの移動方法がテレポートになっていました。（スティック移動もあり）確かに VR 酔いが少なく、意外とすぐに慣れました
  - テレポート移動の際に立つべき場所にカーソルを合わせるとカーソルの表示が変わるため、どこに進むべきかわかりやすかったです
  - サポートキャラが先に移動してくれるため、どこに移動するべきか迷わずに進めました
  - ライトセーバーで壊して進むギミックは楽しかったです
  - 登りの動作が非常にスムーズで本当に登っている浮遊感を感じました。一回の上りでかなり上がれるため、何度も繰り返さないで良い点も良かったです
  - 上り動作が縦だけでなく、横にも動けるので単調にならず本当の上りゲーのようでした
  - 高いところから見下ろしたときの景色が作り込まれており、景色を楽しむことができました
  - 扉を開けるためのギミックが動かすだけで楽しくかつある程度わかりやすいようになっていました
  - ギミックを完了せずに困っているとサポートキャラが次に何をするべきかを言葉で説明してくれるため、迷いませんでした
  - 字幕が視線の少し下に表示され、視線の邪魔にならず読むことができました
  - ストーリーの展開がとてもアツく、没入感がすごかったです
  - 一時間程度でコンパクトにクリアできるようになっており、最後までいくことでカタルシスを感じられました。人によっては少々物足りないと思うかもしれないですが、あくまで 1 章という位置づけなのでこの後も遊べます

- 自作で省みたい点

  - 音がなっても視界の外の敵は気づくのが意外と難しく、方向付きの警告を表示するなど工夫が必要かもしれません。また、視界外の敵は緊迫感をストレスが上回る可能性があり、視界の中に収まる方が良いかもしれません
  - ほぼ無いのですが、ゲーム開始後に移動方法の説明などがなかったため移動方法に困惑したため自作では開始後にチュートリアルを入れます
  - はしごを登りきった際に、はしごを離しても登れないことがありました。自作では頂上あたりではしごを離すと登りが完了しているようにしようと思います

## ソード・オブ・ガルガンチュア

https://www.oculus.com/experiences/quest/3064046640291676/

敵攻撃時のエフェクトや必殺技が参考になります。方向性としては ALTAIR BREAKER と同様という理解のため、プレイは行いませんでした。
ただ、敵の攻撃を跳ね返す際の所定の方向に斬らなければ行けないのは難易度を上げるのに良さそうです。

## Until You Fall

https://www.oculus.com/experiences/quest/2567459230020142/

戦闘時の攻撃方法の指示の参考になります。ただ、剣戟がかなり大きめのアクションのため他の作品を参考にすることしました。

# まとめ

全体として、ストーリーが濃厚な作品が少ないように見受けられたので自身が開発する際はその点で努力したいと考えました。
