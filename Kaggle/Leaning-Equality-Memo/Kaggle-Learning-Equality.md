source: https://www.kaggle.com/code/jamiealexandre/tips-and-recommendations-from-hosts
# About Dataset
## Topics
トピックはタイトルと関連するコンテンツからなる。またそのトピックがどのようなコンテキストにおける内容を扱っているか（トピックのタイトルが「凧型（Kite）」の場合、その親トピックを調べると「四角形の種類」となっていることから図形の幾何学構造トピックであることがわかる。

## Narrow down by Language
言語別に扱うのが良さそうだ。トピックの言語コンテンツの言語は99パーセント一致している。したがっておすすめするコンテンツを選ぶ際に、言語で選択肢を絞り込むべきだ。

## Focus on aligned and supplemental for performance
テストデータセットでは`source`チャンネルのデータはなく、`supplemental`と`alined`チャンネルのみで構成されている。したがって、`source`チャンネルのデータを上手に学習に使いつつ損失関数はそのほか2つのチャンネルのデータに対してのみ行うなどの設計が必要。

## Balance the semantics of `title`, `description` and `text`
トピックやコンテンツにはタイトル・説明・テキスト文の3つ要素がある。タイトルはすべて持っているが、説明文・テキスト文は約半数のみが持っている。また文章量はバラバラであり、意味のある文章と意味のない文章も含まれている。これらの重み配分・情報の取捨選択が必要になってくる。

## Disregard `copyright_holder` for training purposes
トレイニングデータには含まれているが、テストデータにはこの項目はない。したがって無視すること。