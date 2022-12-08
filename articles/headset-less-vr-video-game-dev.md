---
title: "XR Device Simulatorを用いたヘッドセットをできるだけ着けないVRゲーム開発方法"
emoji: "👓"
type: "teck" # tech: 技術記事 / idea: アイデア
topics: ["個人開発", "Meta Quest", "VR", "ゲーム開発"]
published: true
---

「Unity ゲーム開発者ギルド Advent Calendar 2022」の 12/15 の記事です。
とりあえず書き終わったので公開してて、12/15 になったらカレンダーに反映予定です。
ギルド入ってすぐですが、色んな話ができてすごく楽しいです。

https://adventar.org/calendars/7428

# 宣伝

最初に宣伝です。
本記事は執筆中のの技術書『#VR 剣戟ゲーム開発入門』の内容を抜粋しています。
技術書典及び BOOTH で発売予定なのですが、完成ファイルがないとページ作成ができないようでリンク貼れてないです。

そういうのが出るのだな～と心に留めておいてください。
以下本題です。

# ヘッドセットをできるだけ着けないで VR ゲームを開発する

VR に限らず開発を行うにあたっては、開発スピードを少しでも上げるために様々な効率化を行っておく必要があります。
特に時間がかかる作業から取り掛かることが重要です。VR ゲームの開発においては、VR ヘッドセットのつけ外しの時間が意外に時間がかかる作業です。

この記事では各種セットアップ方法は各記事に任せ、セットアップ後に行うと開発がし易い設定を解説します。VR 剣戟ゲームを想定した内容ですが、他のジャンルでも応用が効くはずです。
そのため、VR ヘッドセットをつけないでも簡単な動作確認ができるように設定をしましょう。

各種 VR ヘッドセットの Unity でのセットアップについては以下の記事をご参照ください。

https://framesynthesis.jp/tech/unity/xr/

未検証ですが、以降の XR Device Simulator を使えば VR ヘッドセットがなくても理論上 VR ゲームの開発は可能です。

ただ、実際の操作感を確かめたりは難しく何より VR ヘッドセットを着けてテストプレイするほうが楽しいので、最初は VR ヘッドセット無しで開発を開始したとしても、
ゆくゆくは購入すると良いでしょう。

## キャプチャの中で使用しているアセット

キャプチャは開発中のゲームのものを使用しているため以下のアセットを使用しています。
それ以外のアセットやただの四角形でも試すことはできますので、特に以下のアセットの配置方法などは本記事では解説しません。

■ ステージ
https://assetstore.unity.com/packages/3d/environments/dungeons/decrepit-dungeon-lite-33936

■ 武器
https://assetstore.unity.com/packages/3d/props/weapons/wakizashi-short-sword-144679

■ 敵
https://assetstore.unity.com/packages/3d/characters/humanoids/fantasy/skeleton-warrior-1-222338

## XR Device Simulator の活用

セットアップ方法やデフォルトの操作方法は以下の記事を参照してください。

https://xrdnk.hateblo.jp/entry/2021/02/12/200000

XR Device Simulator のセットアップが終わったら、インスペクタウィンドウのアイコンの横のチェックボックスをオンにして、XR Device Simulator を有効化しましょう。

![XR-Device-simulator-001](/images/headset-less-vr-video-game-dev/XR-Device-simulator-001.png)

下記のように設定を変更することで、武器を持った際に握りっぱなしにすることができます。

![XR-Device-simulator-002](/images/headset-less-vr-video-game-dev/XR-Device-simulator-002.png)

![XR-Device-simulator-003](/images/headset-less-vr-video-game-dev/XR-Device-simulator-003.png)

次に、以下のように LeftHand Controller の Rotate Anchor Action 及び
Translate Anchor Action の Use Reference のチェックボックスをオフにしてください。
こうすることで、武器を握りながら移動する際に武器が回転したり移動したりしなくなります。
RightHand Controller も同様に設定してください。

![XR-Device-simulator-007](/images/headset-less-vr-video-game-dev/XR-Device-simulator-007.png)

設定が終わりましたら、ゲームを再生してください。
武器を握るには、まず T キーを押すことで左コントローラの向きを変えるモードに切り替えてから、少しマウスを動かして
手の位置を調整します。その後に R キーを押して左コントローラの向きを変えるモードに切り替えます。
その状態でマウスを動かすと左コントローラの向きが
変わるので、武器に向きを合わせて G キーを押すと武器を握れます。
T キーを押した際に左コントローラの向きを表すレーザーが表示されない場合は、何度か押してみてください。

![XR-Device-simulator-004(コントローラの向きを変える)](/images/headset-less-vr-video-game-dev/XR-Device-simulator-004.png)

![XR-Device-simulator-005(武器にコントローラを合わせる)](/images/headset-less-vr-video-game-dev/XR-Device-simulator-005.png)

![XR-Device-simulator-006(武器を握る)](/images/headset-less-vr-video-game-dev/XR-Device-simulator-006.png)

その状態で WASD キーを押すと、キャラクターを移動することができます。
QE キーを押すと、視点を動かすことができます。
本来は左コントローラの操作に切り替えるための Shift キーを押しながらキーを押す必要があるのですが、
T キーを押したことにより一時的に左コントローラの操作になっているため、Shift キーを押す必要がありません。

以下の設定を行うことで、武器を掴みっぱなしにできるので操作が楽になります。

![XR-Device-simulator-008](/images/headset-less-vr-video-game-dev/XR-Device-simulator-008.jpg)

以下の設定を行うことで、最初から手に武器を持っている状態となるため効率的に開発できます。
ゲームを再生すると武器で視界が塞がられるため、T キーで位置を動かすようにしましょう。
左が終わったら右も同様に行います。

![XR-Device-simulator-009](/images/headset-less-vr-video-game-dev/XR-Device-simulator-009.jpg)

![XR-Device-simulator-010](/images/headset-less-vr-video-game-dev/XR-Device-simulator-010.jpg)

# 最後に

XR Device Simulator の機能をまだまだ使いこなせていないと思うので、もしこういった使い方をしているよというのがあれば以下までご連絡ください。

https://twitter.com/_mathken
