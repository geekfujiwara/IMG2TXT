# IMG2TXT
画像からテキストを生成するアプリです。以前Azure OpenAI に接続するアーキテクチャで作成していましたが、AI Builder がファイル入力に対応したためAI Builder で画像入力を受け付けるアプリを作成しました。

> [!Note]
> Azure OpenAI のリソースを作成する必要なく、ソリューションをインポートすれば利用することができます。

https://github.com/user-attachments/assets/1d9bcdd1-2735-4392-ad12-2c4df5605668

動画で紹介したように、例えば以下のような使い方があります。画像をインプットすることができるため、見ているものを生成AIと共有して、「この画像からこんなことをして」というお願いができます。

* 食事からカロリー計算と健康に対するアドバイスをする
* 現場作業の画像からKYT (危険予知トレーニング) を提案する
* 請求書から情報を抽出する
* レシートから情報を抽出する
* ラベルに貼られている情報を抽出する
* 不動産登記簿謄本から情報を抽出する



## アプリの説明
アプリはとてもシンプルで、AI Builder がキャンバスアプリに接続されているだけです。ぜひカスタマイズしてご利用ください。

![image](https://github.com/user-attachments/assets/4eaca24c-18f5-4581-8332-ea6dcf56e16f)

AI Builder には以下のようなプロンプトが設定されています・・・というか何も書かれていません。

![image](https://github.com/user-attachments/assets/5a6baf80-98f3-4257-8b22-ec5e3c5764a9)


## 前提条件

* AI Builder を搭載したPower Apps アプリの利用にはPower Apps Premium ライセンスが必要です。トライアルまたは開発者プランの提供もあります。
* AI Builder のライセンスは、ユーザーのベースライセンスの他にクレジットの消費があります。クレジットはPower Apps Premium ライセンスに付属しますが、不足する場合は購入することができます。

## ソリューションのインポート方法

[ソリューションをダウンロード](https://github.com/geekfujiwara/IMG2TXT/releases/tag/IMG2TXT)します。

ソリューションからインポートを選択します。

![image](https://github.com/user-attachments/assets/f6c3c511-08f3-4459-90b7-5a111b52ee26)

Zip形式のままファイルをアップロードし、ウイザードに従ってインポートします。

![image](https://github.com/user-attachments/assets/7384422e-0920-4e8b-9610-5c95cbcae5b3)

このまま進めます。

![image](https://github.com/user-attachments/assets/ebfa00fc-d78d-4e04-844a-4a6a05a94283)

インポートが完了したらマネージドのタブにあるソリューションを開きます。

![image](https://github.com/user-attachments/assets/676c9270-3ac3-4e9e-9f37-05fb2325393d)

すべてのカスタマイズを公開します。

![image](https://github.com/user-attachments/assets/aa28a9f9-22fd-4d87-94aa-05d7d635a868)

インポートが完了しました。

## アプリの使い方

アプリを開きます。

![image](https://github.com/user-attachments/assets/3ccc8347-37ff-4264-8b52-8c0ad67a651b)

解析したい画像を追加します。アップロードした画像を確認したい場合はプレビューを拡大することができます。

![image](https://github.com/user-attachments/assets/183ca4eb-e1a9-4107-a119-14e83fa24ff1)

戻す場合はもう一度クリックします。

![image](https://github.com/user-attachments/assets/11aad10a-75c1-4b6a-b2e1-7206f9bb9fda)

実行ボタンをクリックします。すると画像を説明してくれました。

![image](https://github.com/user-attachments/assets/b046fcc2-5270-44b9-860e-22b038735731)

プロンプトを変えてみます。

```
画像に写っているオブジェクトを抽出してJSON形式の配列で出力してください。
```

このように出力されました。

![image](https://github.com/user-attachments/assets/23e0d08a-c4db-4a4f-b45d-0ee9c60df52b)


```json
[
    {
        "object": "lion",
        "location": "right side, sitting under a tree next to a telescope"
    },
    {
        "object": "telescope",
        "location": "middle right, mounted on a tripod"
    },
    {
        "object": "tree",
        "location": "right side, lion sitting under it"
    },
    {
        "object": "tree",
        "location": "left side, in the background"
    },
    {
        "object": "zebra",
        "location": "middle, walking on the field"
    },
    {
        "object": "zebra",
        "location": "middle, jumping in the air"
    },
    {
        "object": "zebra",
        "location": "middle, flying in the air"
    },
    {
        "object": "field",
        "location": "covers the entire ground area"
    },
    {
        "object": "mountains",
        "location": "background, far distance"
    },
    {
        "object": "clouds",
        "location": "background, in the sky"
    }
]
```

## プロンプトの紹介

* この画像に写っている項目の説明をしてください。更に続けて、カロリー計算をしてください。必要であれば、不足する栄養についてのアドバイスを提供してください。
* この状況に関するKYTの情報を提供してください。
* この画像から情報を抽出してください。



## FAQ

Q: 回答してくれない。その結果にはお答えできませんというような回答が返ってくることがある。

A: プロンプトを変えてみましょう。生成AI が受け付けやすいプロンプトを検証してみましょう。また、JSON形式に出力するには、出力結果変更の機能を利用することを推奨します。
