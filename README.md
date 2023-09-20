# consumer_preference
Consumer Preference Research, Flower and Plants Japan. Year 2023  

[概要] 花の消費選好調査 2023年  
● 農林水産省 2023年度持続的生産強化対策事業のうち「ジャパンフラワー強化プロジェクト推進事業」の一環として、「花の消費動向調査」を実施（国産花き生産流通強化推進協議会）  
● 目的　花きの消費実態、物流逼迫を受け、無駄や負荷の少ない花の流通システム改革の一歩として、需給のミスマッチを回避することが求められる。そこで、花の規格とアップサイクルに関する消費選好を探る。花の価格高騰の中、値付けが課題となりつつあるため、自宅用の花について、生活者の心理的な価格受容性を調べる。花の日持ち保証販売、各種サステナブル認証の認知や評価、環境配慮など生産プロセス情報へのニーズについても、情報提供を行う。  
● レポジトリでは、報告書および、花の消費選好調査で使用した、データ取得及び解析のためのコードを公開  
● 調査概要 2023年8月13日(火)～10月14日(水)実施、全国のインテージモニター 20～50 代男女　500名回答、ネット調査）　経時データのうち、2018年以前のデータは、MPSジャパン㈱提供  
● 引用例　青木恭子（2023）「花の消費選好」国産花き生産流通強化推進協議会、MPSジャパン発行  
Source: Aoki, Kyoko. The consumption of flowers and plants in Japan 2023. Council for Japanese Flower Production and Distribution Enhancement.    

This research was funded by the Ministry of Agriculture, Forestry and Fisheries, Japan.  

[コード]  
●政府統計API経由でデータ取得　家計調査から、メタデータ取得、、統計の項目の情報とコード品目分類を参照、消費支出、花、植物・園芸用品の経年データ取得（JSON形式）、世帯構成ごとに抽出・csvファイル書き出し  

●時系列　SLT（Seasonal and Trend decomposition using Loess）モデル　　データから、トレンドと周期成分を分けて取り出し、描画   
 ローカル回帰平滑化法（Loess）を使用 Loessは、局所的な近傍データの重み付き平均を計算、滑らかな曲線をデータに適合させる手法
 時系列データを季節成分、トレンド成分、残差成分に分解: 季節調整やトレンドの把握、季節パターンの特定
 季節性の除去: データから季節成分を推定・除去　ローカルな回帰スムージング（Loess）を用いて季節成分を推定　各データ点の周囲のデータを参照してスムージング　データの局所的な特徴を反映  
 トレンドの推定: 季節成分を除去したデータに対して、トレンド成分を推定　トレンド推定には、ローカルな回帰スムージング（Loess）を使用、描画
 残差の計算: 季節成分とトレンド成分を元のデータから除去  
 
●コンジョイント分析 

●価格受容性分析　PSM

