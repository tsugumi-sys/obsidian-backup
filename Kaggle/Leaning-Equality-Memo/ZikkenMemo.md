
メモ
- EDA e.t.c
	- 兄弟や親トピックのコンテンツから単純にランダムに取り出す方法はうまくいかない（public score: 0.018）。ランダムに取り出す部分が良くないと思われる。
	- [こちら](https://www.kaggle.com/code/tubotubo/lecr-tfidf-inference)を参考に[言語別でモデルを作成するパターン](https://www.kaggle.com/code/tsugumi7878/learning-equality-baseline?scriptVersionId=115262243)で提出。結果は改善せず。
	- [こちら](https://www.kaggle.com/code/tubotubo/lecr-tfidf-train)の結果から、予測する数は5から10が良さげ。実際にK近傍法モデルで、作成するクラスターの数を12と5でそれぞれ結果を出すと、5の方が結果が良かった。
	- Sentence-transformersで単純なコンテンツとトピックの類似度の上位5個を出すだけで0.23くらいになった。おそらく正解データは単純なテキストの類似度を基にレコメンドする候補を決定している可能性が高い。ただしまた別の観点でも選んでいると考えられる（0.25はだいたい5個に1個正解がある）。
- text similality approach
	- NA: 単純にコンテンツのタイトルだけでなくテキスト文も含めて精度が上がるかどうか？i
		- DONE: 単純に結合した場合、精度は若干落ちる。Descriptionに不正なデータが入っており、ノイズになっている可能性がある。
	- NA: テキストのクリーンを行っても精度はあまり改善せず。
		- DONE:
	- NA: トピックの関連するコンテンツのタイトルも含めて関連度合い出したらどうか？
		- DONEコンテンツのツリー文字列とトピックのツリー文字列の類似度で計算はスコアがた落ちだった。
	- NA: 言語別VSすべてのコンテンツで学習させた場合。
		- そこまでスコアは変わらない。単純な類似度では判断できない推薦コンテンツがありそうだ。
	- NA: target topicのコンテンツと他のコンテンツとの関連度合いを計算し、平均を取る。このスコアの上位5個を推薦リストとする。
		- スコア完全せず。これは、Correlationsの中身テスト環境で変わらないため。
	- NA: TF-IDFやBM25などの他の類似度計算方法を試してみる。
		- 
- KNNベース
	- NA: 言語別コンテンツで学習させた場合とすべてのコンテンツで学習させた場合どっちがスコアが高い。
		- DONE: 言語別コンテンツは0.22, すべてのコンテンツは0.19。
	- DONE: ベースライン（TFIDFとTruncatedSVD）は0.12くらい。
	- NA: sentence-transformerでエンベッドしたベクトルを用いて、言語別のコンテンツタイトルにKNNをフィットさせた場合.
		- DONE: 0.23　単純なタイトルのcos_simとほぼ同じ結果となった。
- 教師あり学習アプローチ
	- 方針
		- KNNである程度コンテンツをグループ化する。
		- グループに含まれるコンテンツがcorrelations.csvに含まれている場合は、1それ以外は0としてラベルを作成する。
		- 作成したラベルと特徴量（トピックのタイトルとコンテンツのタイトルなど）を用いて教師あり学習データを作成する。
		- 教師あり学習モデルを学習させる。（CVもここで適用する。）
		- 学習済みモデルを用いて予測値を出す。
	- NA；CVなしかつ、シンプルなKNNClassifierでモデルを学習。特徴量はトピックとコンテンツのタイトル。
	- NA；CVあり（213tubo）、KNNClassifier.
	- NA; CV, BertClassifier?
- まずトピックの類似度から関連トピックを絞り、かつその関連コンテンツからさらに類似度で絞るとどうなるか？