# YouTube_analysis

## Overview
YouTubeの登録者数について，(1)ではその他の要因との関係性を主成分分析(PCA)にて分析し，(2)ではチャンネル登録者数の遷移を時系列データとして，fbprophetを用いて分析および予測します．

## Description
それぞれのnotebookの内容を説明する，
### (1)`PCA_for_YouTube.ipynb`
チャンネル登録者数が、他のどのような要因と関係しているのか、また他の要因どうしの関係にも着目し，PCAを適用し考察を行った．  
`youtube_data.xlsx`には2019/2/18時点でYouTube Japanにおけるチャンネル登録者数が上位50位の各チャンネルについて以下の様な項目を含むレコードが記述されている．
|columns(en)            |ja                  |
|:----------------------|:-------------------|
|ID                     |ランキング            |
|Num_of_sub             |チャンネル登録者数     |
|Total_views            |総再生回数            |
|Num_of_mov             |動画本数             |
|Rate_of_high           |高評価率             |
|Num_of_day_over_million|100万人突破日数       |
|Num_of_10million_mov   |1000万再生突破本数    |
|Num_of_day_since_est   |チャンネル開設からの日数|  


データを標準化後，scikit-learnのPCAライブラリを利用し，累積寄与率が70~80%となる第3主成分までを用いてbiplotにより可視化を行った．以下は第1,2主成分を軸に二次元上に各データと元の軸を射影したものである．  
チャンネル登録者数には，因子負荷量上で最も近い総再生回数と関係があるといえる．次に，動画本数が近い関係にある．一方で，対極にあるものは存在せず，他の要素は関係性が弱い。また，100万人突破日数とチャンネル開設からの日数は因子負荷量上で近い．これは，古いYouTuberほど登録者100万人までに日数を要したということであり，現在のYouTubeの繁栄を裏付けている．また，今回の考察結果は上位50チャンネルのデータであるため，一般的な知見とは異なっている可能性があることに注意されたい．

<img src="https://user-images.githubusercontent.com/55009777/105423997-d6dcc680-5c89-11eb-8ad0-9d4a7ce82fa9.png" width="500px">

### (2)`subscribers_transition_analysis_with_fbprophet.ipynb`
簡単に状態空間モデルによって時系列データの分析を行うことができるfbprophetを利用して，チャンネル登録者数の遷移について分析，予測を行う．  
`subsc_data.xlsx`には[HikakinTV](https://www.youtube.com/user/HikakinTV)の2013/1/1~2019/3/1における2週間ごとのチャンネル登録者数の増加数をまとめている．  
以下は，全体のトレンドと月効果，およびそれらの効果を考慮した一年先までの予測である．トレンドから，2017年ごろよりYouTuberという言葉が広まり，利用者数が増加していることがわかる．月効果からは，春夏冬にそれぞれピークを迎えていて，これは学生の休暇期間と重なり，利用者数が一時的に増加していると考えられる．有名YouTuberの登録者数の遷移を見ることでYouTube全体の繁栄や傾向を見るこたができた．

<img src="https://user-images.githubusercontent.com/55009777/105426441-7c923480-5c8e-11eb-81c4-b0fa0e000031.png" width="500px">

<img src="https://user-images.githubusercontent.com/55009777/105426447-8025bb80-5c8e-11eb-915e-f231299a0a1e.png" width="500px">

## Requirements
- fbprophet
- jpholiday

## Note
今回使用した`youtube_data.xlsx`と`subsc_data.xlsx`は公開しておりません．  
お手数ですが，[YouTube Data API](https://developers.google.com/youtube/v3)を利用して作成していただく必要があります．
