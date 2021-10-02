# Build Guide

## 部品リスト

|部品名称|数|
|:-|:-|
|PCB|1|
|トッププレートA(アクリル グレースモーク 3mm)|1|
|トッププレートB(FR4)|1|
|ミドルプレート(アクリル マットクリア 5mm)|1|
|ボトムプレート(アクリル グレースモーク 3mm)|1|
|スペーサー(M2 6mm)|5|
|ネジ(M2 4mm)|5|
|ネジ(M2 10mm)|5|
|スイッチ用ソケット(Kailh PCB Socket)|26|
|ゴム足(小)|4|
|ゴム足(大)|2|

"Torch Edition" には以下のパーツが付属します。

|部品名称|数|備考|
|:-|:-|:-|
|バックライト&アンダーグロウ用LED(YS-SK6812MINI-E)|35|必要数:33,予備:2|

以下のパーツはキットに含まれないため、別途購入してください。

|部品名称|数|
|:-|:-|
|CherryMX互換キースイッチ|26|
|CherryMX対応キーキャップ(1u)|25|
|CherryMX対応キーキャップ(2u)|1|
|CherryMX対応スタビライザー(2u)|1|
|USB Type-Cケーブル|1|

__部品外観図(Torch Edition)__

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_parts.jpg" width="860">

## QMKセットアップ

キーボードファームウェアをProMicroへ書き込むため、QMK Firmwareのビルド環境が必要となります。  
以下のリンクを参考に、ビルド環境をセットアップしてください。

https://docs.qmk.fm/#/ja/newbs

## パーツ半田付け

以下のパーツをPCBへ半田付けします。

1. スイッチ用ソケット
2. LED
    - LED付属モデルもしくは追加購入した場合

### PCBの確認

シルクの印刷およびパーツが実装されている側が裏面、反対側が表面です。

__裏面__

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_top_view.jpg" width="860">

### スイッチ用ソケット

PCB裏面の `MX1~MX26` の記号シルクが印刷されている箇所に、スイッチ用ソケットを半田付けします。

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_socket_position.jpg" width="480">

半田付けが難しい場合、PCB表面からソケットにスイッチを差し込むことでソケットを固定した状態で半田付けすることができます。

### (Option)LED

PCB裏面のスイッチホール下およびPCB内の各所に存在するLED用ノンスルーホールにLEDをはめ込み、半田付けします。  
LEDには極性があるため、LED側面の4つのタブのうち、角が欠けているものがLED用ノンスルーホールの左下のシルクと一致するよう配置して下さい。  
すべてのLEDの表面がPCB表面を向くよう配置します。

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_backlight.jpg" width="480">

ここまでの作業が完了すると、PCB裏面は以下のような状態になっているはずです。  
LEDを取り付ける場合は、スイッチホール以外の箇所の実装漏れがないか十分確認してください。

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_solderd.jpg" width="860">

## ファームウェア書き込み

PCBのUSB Type-CコネクタとPCをUSBケーブルで接続し、GUI(`QMK Toolbox`)かCLI(`make`もしくは`qmk`コマンド)でファームウェアのビルドおよび書き込みを実行します。

- Reference
    - https://docs.qmk.fm/#/ja/newbs_building_firmware
    - https://docs.qmk.fm/#/ja/newbs_flashing

ファームウェアを書き込む際は、PCB裏面右上(USB Type-C コネクタ下)のリセットスイッチを押してマイコンをフラッシュモードにしてください。

### GUI

ファームウェアはQMK Configuratorから生成することができます。

https://config.qmk.fm/#/craftwalk/LAYOUT

ファームウェアのコンパイルおよびダウンロード後、QMK Toolboxへロードして書き込みを実行してください。  
なお、書き込みの際はMCUに `atmega32u2` を指定してください。

### CLI

__makeコマンドの場合__

```zsh
$ make contender:default:avrdude
```

__qmkコマンドの場合__

```zsh
$ qmk compile -kb contender -km default
$ qmk flash -kb contender -km default -bl avrdude
```

## 組み立て

組み立て前に、以下アクリルパーツの保護紙を剥がしてください。

- トッププレートA
- ミドルプレート
- ボトムプレート
    - ロゴ部分の保護紙は剥がしづらいため、ピンセットなどの利用をおすすめします。剥がす際に誤ってプレートに傷をつけないよう注意してください

### トッププレート&ミドルプレート取り付け

トッププレートA/トッププレートB/ミドルプレート/PCBの順で重ね合わせて、以下のようにトッププレートから10mmのネジ、PCB裏面から6mmのスペーサーで固定してください。

<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_top_plate.jpg" width="860">
<img src="https://github.com/sotoba/craftwalk/blob/images/craftwalk_back_view.jpg" width="860">

### ボトムプレート取り付け

PCB裏面にボトムプレートを取り付け、6mmのネジで固定してください。

### キースイッチ&キーキャップ取り付け

お好みのキースイッチ、キーキャップをPCB表面から取り付けてください。

### (Option)ゴム足取り付け

ボトムプレートのお好みの位置にゴム足を取り付けてください。取り付け位置によっては打鍵時に基板が傾き不安定になってしまう可能性があるため、取り付け前にゴム足を台紙から剥がさず台紙をカットして、安定して打鍵できるゴム足の配置決めをしてから取り付けてください。
