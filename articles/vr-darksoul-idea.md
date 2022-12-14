---
title: "VR版ダークソウルを開発したい"
emoji: "👓"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["個人開発", "MetaQuest", "VR", "ダークソウル", "ゲーム開発"]
published: false
---

# 概要

## メモ

基本的にはタイトルのとおりです。
収益よりも実際に自分が遊んでみたいというのが開発動機です。
プレイ機器は私が所持する Meta Quest2 をファーストターゲットとします。

- いつどこから敵が出てくるかわからないという点や、死闘感を再現するため一人称視点のプレイです
- 3D 酔いは最低限としたいですが、酔いに耐性のある人をターゲットとします（市場が狭くなることは許容します）
- 剣を開発初期の武器として、後々武器種類は拡充予定です
- パリィ後のクリティカル攻撃を快感ポイントとするため、剣以外の装備を盾にしてしまうと範囲が大きくパリィの難易度が下がってしまいます
- そのため、小刀などを相手の攻撃にジャストミートさせ、かつボタンタイミングよくボタンを押すとパリィができるようにします
- パリィ後、相手の体に複数の赤い線が表示されてそれをなぞるように斬るとクリティカルヒットとなります（赤い点で突く形も有りか）
- ザコ敵との戦闘としては、一撃で倒せるのではなくある程度一匹を倒すのに苦労し、複数に囲まれると高確率で倒される程度を目指します
- ゲーム冒頭のチュートリアルの後は、倒すのが非常に困難なボスを配置し、ボスに倒されても進めるようにすることで高難易度のゲームであることを理解してもらいます

開発方針としては以下です。

- 上記のプレイ体験が実際に楽しいと感じるかを検証するため、最初はアセットなどにはこだわらず、まず戦闘システムの実装・体験を優先します
- 考えをまとめるために企画書は作成しますが、個人での開発となるため細かい部分までは立ち入らないようにします
- また、本タイトルを最初から開発するのではなく剣戟アクション部分のみを切り出したゲームとして小さくリリースして通しの開発の練習兼反応を見ることも考えます
- 例としてはグラディエーターシュミレーターというタイトルで、3 ～ 4 戦程度の戦闘があり、その中に複数名との戦闘や獣との戦闘（動物への配慮から殺害までは至らない）、最後はボス戦があるという想定です
- 短いゲームとなるため 1,000 円程度を想定します

## 参考資料

https://www.youtube.com/watch?v=qjesqFqOSDc

Audio Shield
https://xr-hub.com/archives/9947

Beat Saber
https://www.moguravr.com/beat-saber-thorough-commentary/

Zenith: The Last City
https://www.4gamer.net/games/557/G055718/20220210166/
https://www.gamespark.jp/article/2022/01/13/115014.html

# ダークソウルの面白さのメモ

## 基本情報

- ゲームタイトル

  - ダークソウル

- メーカー

  - フロム・ソフトウェア

- 対応ハード
  - コンシューマー機全般、Steam

## ジャンル・ジャンルの面白さ

- ゲームジャンル（面白さの種類）

  - 高難易度の死闘が頻繁に発生する 3D アクション

- ゲーム目的

  - 各ステージのボスを倒すことが最大の目的

- 挑戦（面白さ）の内容

  - 初見では倒すことが難しい敵やステージが続き、何度も挑戦することでプレイヤースキルが向上してクリアできた際の喜び

## 能動的にさせる要素

- 目的は明確か

  - 最終的な目的は戦闘の準備などを行う拠点に居るサポートキャラから説明されます
  - 拠点から各ステージに行くことができ、後半の難易度の高いステージは序盤のステージをクリアすることで行けるようになります
  - 各ステージの目的は、最深部にいるボスの討伐です

- 手段は明確か

  - ボスに辿り着くまでの敵との戦闘において、攻撃手段は武器での攻撃や呪文・聖なる力を用いた奇跡などいくつかのパターンがあります
  - ただ、ゲームの最初のキャラの作成の段階で戦士や魔術師などの職業を選択するのである程度どの攻撃が得意かはわかるようになっています
  - アクションゲームにおけるお決まりの操作などは詳しく解説されませんが、これは本ゲームがある程度アクションの経験があるプレイヤーを対象にしているためです

- 自分で決められるか

  - 各ステージは基本的に一本道ですが、要所には分岐があり進んだ道が先に進む道ではなかった場合でもアイテムがあったり NPC がいることが多いです
  - 戦闘について敵は必ず倒さなければいけないわけではなく、やり過ごすこともできます
  - 自分で敵を倒すだけでなく、転がってくる大岩の下敷きにしたりドラゴンの炎に巻き込むことで倒すこともできます

- 小さな成功体験

  - ステージ内の敵は油断すると単体でもやられてしまい、複数同時に相手をすると勝つのが難しいという難易度であるため、敵を倒すごとに達成感があります
  - また、敵は至る所にいるというわけではなくある程度エリアを進むとそのエリアにいるという流れのためメリハリがあります
  - 通常の戦闘とは別に要所に何度も挑戦して攻略パターンをつかめないと進めないようになっている難所があり、クリアした際の達成感が大きくなります

- 適度な難度

  - 難易度は通常のゲームに比べてかなり高く、特にボス戦はクリアが不可能なのではないかというレベルになっています
  - ただ、ソロで何十回も試行錯誤すればコツや隠れた弱点がわかるようになっていたり、どうしてもクリアできない場合はマルチプレイをすれば殆どの場合はクリアできるようになっています
  - また、ステージを進む途中でやられてしまうと体力が少ない状態の霊体と呼ばれる形態になってしまいクリアの難易度が上がります
  - 霊体から戻るにはアイテムを使いますが、貴重なアイテムであるためやられてはいけないという緊張感が生まれます

- 評価と報酬
  - 敵を倒した際にはレベルアップに必要なソウルが入手でき、入手したソウルの量が画面に表示されるようになっています
  - 強い敵であるほど多量のソウルが手に入るようになっており、倒すインセンティブになっています
  - ボスを倒すと大量とソウルとともに、ボスの特長に応じた強力な武器と交換できるアイテムが手に入るようになっています

## クライマックス

- ボス戦
  - ボスの体力が減るとボスの形態が変わったり、分裂したり攻撃手段が増えたりします
  - また、通常ボスを倒す過程でソロであれば何十回も挑戦することになるため画面下幅いっぱいに表示されるボスの体力ゲージが少なくなってくると、今度こそ倒せるかという期待と緊張で心臓が高鳴るほどの興奮が得られます
