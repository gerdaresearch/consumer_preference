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
コンジョイント分析は、消費者の選好を理解し、最適な商品やサービスを開発するための市場調査手法。属性（規格、スタイル、日持ちなど）と水準を設定し、それら（スペック）を組み合わせた商品プロファイル群から、消費者に選好を評価してもらう　店頭での選択状況に近い形で、特性の重要度を明らかにするもの。実験計画法。
手順　　
1．属性と水準の設定  
製品やサービスに関連する属性（特性や特徴、ここではスタイル、日持ちなど）と水準（選択肢）を決定  
2. 選好の評価  
回答者に、異なる属性水準を組み合わせた商品群を提示し、好みを選択してもらうか、魅力度に応じ順位をつけてもらう　この調査では1～3位の順位
※ 組合せは直交表に従い割付　最小限の選択肢数（8通り）で済む（全組合せは4属性×2水準で16通り）
3. 解析  
(1) 前処理　選択商品群（コンジョイント・カード）の番号が、ローデータに整数値で格納されている　3位まで順位があるため、行単位でデータ処理できる形に整型　1人のIDで1～3位分3行作り、属性水準とつなげたデータフレームを作る     属性ごとに水準を0,1のダミー変数に変換（例 アップサイクル＝１、非アップサイクル（通常品）＝０）、カテゴリーデータを説明変数とした重回帰分析  
(2) 商品ごとに選好をスコア化（1位3点～3位1点）平均スコアを目的変数として重回帰分析（数量化Ⅰ類）  
(3) 各属性の部分効用値を計算　部分効用値は、それぞれの属性水準が、選好にどれだけ影響を与えるかを示す　属性の重要度は、各水準の部分効用値の絶対値合計が、全体に占める比率　値が大きいほど、商品選択で重要　  
(4) 全体効用値を計算  属性水準の部分効用値を足し合わせ、各商品の選好度を推測    
段階ごとに出力する形で、やや冗長なコードになっているが、確認しながら進めることに重点を置いた  



