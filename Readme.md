
# ハッカソンなのにエッチングで基板を量産する

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2687.jpg" height=400px>


2018/12/15・16に秋葉原UDXで行われた[Yahoo HackDay2018](https://hackday.jp/) に誘われたので参加することになり、当日初対面の方たちと話し合った結果、エッチングで基板を作り、24時間で設計から量産を行う事になった。

## どんな基板を作ったの？
ESP8266を搭載し、会場を飛び交っているSSIDの数と信号強度をLEDで視覚化するというモジュールを複数作ることにした。秋葉原に行くと本当にビックリするくらいWiFiが使えないし、ものすごい数のSSIDがカウントできる。複数のモジュールをばら撒いておいて『おっ、この辺がWiFi空いている』とか『信号強度からしてここが発信源だ！』みたいな事ができそうな気がした。

## 設計
Eagleで回路図を引いた後、別なメンバーがKiCadでPCBパターンを設計した。特にどちらでも問題ないと思う。

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2673.jpg" height=200px>

エッチングでのパターンはPCBメーカーに出すのと異なり、いくつか『こうしたほうがいい』ポイントがある。

+ できるだけ太く
+ できるだけ黒く
+ できるだけ角を丸く

ラフに言うと、エッチング液（塩化第二鉄）が銅を溶かしてパターンを浮かび上がらせるので、あまり細いとパターンが切れてしまう恐れがあり、余白もベタで塗っておけば溶かす量が減るので早く仕上がり、角があるとそこに液が十分に回らないと溶かしきれない事がある。このあたりは何度かやってみると感覚が分かってくる、としか言えないが、『DIPでピン間1本通すのがギリかな』とか『線幅は0.5mm以上にしたほうが失敗が少ないかな』と感じている。
ただ今回、『HackDay2018』とロゴは目立つようにしたかったため、あえてポジでエッチングした。かっこいい。


<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2674.jpg" height=200px>

## パターンを印刷
千石電商B1にて、[サンハヤト製クイックポジ感光基板NZ-E43K（ガラスコンポジット1.0t×100×150）](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=556R-5TE6)と 
[エッチング液](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=538T-35HW)を購入した。サンハヤトの感光基板はサイズとともに材質として紙フェノール・ガラスエポキシ・ガラスコンポジット・フレキシブルがあるが、今回は基板厚みが1mmでカッターなどで加工しやすいガラスコンポジットにした。（紙フェノールは安価だけどハンダ付けの際にパターンが剥がれる事が多く、ガラスエポキシはキレイだけど超硬いので加工が大変（個人的感想です））
秋葉原から30分くらいにある自分の事務所から[ブラザー製インクジェットプリンタDCP-J567N](https://www.brother.co.jp/product/printer/inkjet/dcpj567n/index.aspx)と[インクジェット対応OHPシート](https://www.amazon.co.jp/dp/B003Z9LDRW/)を持ち込み、設計したパターンを面付けして印刷した。
####ここでポイント：印刷した際のインク麺が基板に密着するように、左右反転して印刷すること。

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2674.jpg" height=200px>

## 感光
プリント基板の感光には紫外線が必要で、蛍光灯や太陽光でも感光は可能なのだが安定したキレイなパターンを得る為に[専用ライト](https://www.amazon.co.jp/dp/B00ZZQAGJO/)を使用した。またパターンを感光基板に密着させることが大前提なので、こちらも[バキューム式のクランプ](https://www.amazon.co.jp/dp/B00ZZQAFF4/)を使用した。もしあなたがエッチングで基板を作る事を今後も考えているなら、この2つはオススメ。注意するべきは感光マスクの出来と焼き付ける露光時間で、感光マスクについてはしっかり光を遮ってエッジがクッキリしていることが必要。（同じOHPシートを2枚印刷して重ねても良い）。露光時間は基板の製造経過時間を確認して[こちら] (https://www.sunhayato.co.jp/dcms_media/other/NZ-expProfile.pdf)のグラフから確認することをオススメする。
<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2677.jpg" height=200px>

## 現像
こちらは[スプレー式の現像液](https://www.amazon.co.jp/dp/B011IJRP2C/)を利用した。現像には液の温度や濃度などが重要だが、スプレー式は比較的寒い時期でも問題なくすばやく現像できる。ただし強力なのでモタモタしているとパターンが無くなってしまうので、状態をよく見ながら進める必要がある。垂直に立てた基板にたっぷりとスプレーし、泡が基板全体を覆いつつどんどんと下に流れて行くようにする。キレイに感光できているならクッキリとパターンが浮かび上がるのですかさず基板を水洗いして現像を止める。

## エッチング
#### ！！注意！！エッチング液は絶対に未処理で捨てない！
#### あと洋服に付くと絶対落ちないので奥様／母親にすごく怒られる！！
サンハヤトのエッチング液には厚手のビニール袋が入っていて、こちらを使うのがポイント。今回は持ち込んだ電気ポットで80℃前後のお湯を作り、エッチング液を入れた厚手のビニールを湯煎して温める。お湯の中に10分も漬けると十分熱くなるので基板（入れる前に基板の角をヤスリで丸めておく）を入れ、袋を激しく揺する。常に新しいエッチング液が基板に触れ続けるようなイメージで袋を揺すりながら、時々エッチングの状態を確認する。温度やパターンにもよるが3分位でエッチングが終了する。袋から基板を引き上げ、十分にエッチング液を拭き取ってからアルコールを使って感光レジストを除去するとピカピカの銅箔パターンが現れる。キレイ。
ただこのままだと酸化してハンダが乗りづらくなるので、フラックスをスプレーして十分に乾かす。これでOK。

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2681.jpg" height=200px>

## 実装
せっかくなので表面実装部品をリフロー実装する。今回はクリーム半田ディスペンサを使ってクリーム半田を載せ、ホットエアマシンを使ってリフローしていった。メタルマスクが無くても、リフロー炉が無くてもリフローが出来る。
<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2688.jpg" height=200px>
<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_2690.jpg" height=200px>

## デモ

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_demo1.jpg" height=200px> <img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_demo2.jpg" height=200px>


##スライド
![Wifi警察](https://speakerdeck.com/krfatos/wi-fibasutazu-hackday2018?slide=5)


## 最後に
参加者の方にも『馬鹿じゃないの？』とコメントされたが、
https://twitter.com/shigezo/status/1075191497497047040
仲間うちに指摘されたのは「あの場あの時間でエッチングから実装までやったのは驚異的だし素晴らしいんだけど、審査員にその価値わかる人いなかったね」という点。ただ基板発注するのとは訳が違うんだけど、日頃からハードウェア関わってる人はそこ笑ってくれた。痛快だったぜ。#hackday2018

<img src="https://github.com/NaohiroIIDA/EthinginHackathon/blob/master/image/IMG_demo3.jpg" height=200px>