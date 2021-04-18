- Part 1 SW testの基礎
    - Ch. 1 SW testの必要性
    - Ch. 2 SW開発の流れとtest工程
    - Ch. 3 white box test
    - Ch. 4 black box test
- Part 2 さまざまなtest技法
    - Ch. 5 同値class test and 境界値test
    - Ch. 6 decision table test
    - Ch. 7 状態遷移test
    - Ch. 9 test技法適用chart
- Part 3 test document and monitoring
    - Ch. 10 test documentの作成
    - Ch. 11 test documentの正しい書き方
    - Ch. 12 test実施のmonitoring

# Part 1 SW testの基礎

## Ch. 1 SW testの必要性

### SW testの必要性

SW test: 次のことをして、品質の良いSWを作ること
- 欠陥を取り除き、userの要求を満たす

SW：
- computerを動作させるためのprogram
- 命令文をcomputerに実行させたい順番に並べて記述した文章

### 欠陥とは

欠陥: 次を満たす誤動作。
- 原因がSWにあり、それが特定されている

不具合: 次を満たす誤動作。
- 原因がSWにあり、それが特定されていない

### SWの品質とは

品質:
- 要求を満たすことである by Philip B. Crosby
- 誰かにとっての価値である by G. M. Weinberg

品質のよいSW: userの要求を満たし、userに価値を提供するSW

ISO/IEC 9126 品質特性規格

|品質特性|副特性|説明|
|-|-|-|
|機能性|(functionality)|必要な機能が実装されていること|
||合理目的性|使用上適切な機能が提供されていること|
||正確性|必要な精度で正しい結果が得られること|
||相互運用性|他のsystemと正しく相互作用すること|
||security|許可されていない人が、情報を見たり修正したりできないこと|
||標準適合性|機能性に関する、法律・規約・規格を遵守していること|
|信頼性|(reliability)|機能が正しく動作し続けられること|
||成熟性|故障を回避できること|
||障害許容性|障害が発生した場合でも指定された機能を維持できること|
||回復性|障害発生後、dataの復旧を含めて正常状態に戻れること|
||標準適合性|信頼性に関する、法律・規約・規格を遵守していること|
|使用性|(usability)|利用者に使いやすく魅力的であること|
||理解性|利用者が使い方を理解しやすいこと|
||習得性|利用者が習得しやすいこと|
||運用性|利用者が運用しやすいこと|
||魅力性|利用者が魅力的であること|
||標準適合性|使用性に関する、法律・規約・規格を遵守していること|
|効率性|(efficiency)|資源の量に対比して適切な性能であること|
||時間効率性|応答時間、処理時間が適切であること|
||資源効率性|実行時の資源の量、種類が適切であること(memory, DISK, 通信回路)|
||標準適合性|効率性に関する、法律・規約・規格を遵守していること|
|保守性|(maintainability)|維持、変更がしやすいこと|
||解析性|欠陥の診断、故障の追求、修正箇所の識別が行いやすいこと|
||変更性|修正がしやすいこと|
||安定性|修正により影響を受けにくいこと|
||試験性|妥当性の確認がしやすいこと|
||標準適合性|保守性に関する、法律・規約・規格を遵守していること|
|移植性|(portability)|別環境に移しやすいこと|
||環境適応性|異なる環境で修正なしに動くこと|
||設置性|指定された環境に設置しやすいこと|
||共存性|他の独立したSWと動くこと|
||置換性|同一環境で同じ目的のSWと、入れ替えて使えること|
||標準適合性|移植性に関する、法律・規約・規格を遵守していること|

求められる品質意識
1. Verification and Validation(検証と妥当性)
    - Verification: 開発仕様書の通りにSWが作成されているかを確認すること
        - 開発工程ごとの開発仕様書に対してverificationする
    - Validation: userの要求どおりにSWが作成されているかを確認すること
        - SWを動作させるだけでなく、開発仕様書の妥当性を確認する
2. 品質とuser満足度の関係
    - 狩野model: 品質model
        - user満足度と品質の関係を示したmodel

狩野modelにおける品質の分類
|品質要素|充足|不充足|
|-|-|-|
|当たり前品質|当たり前|不満|
|一元的品質|満足|不満|
|魅力的品質|満足|仕方がない|

- 当たり前品質: userの基本要求を満たす品質
    - 基本要求: userが「これだけは絶対に満たしてほしい」と考えるもの
- 一元的品質: 充足していると満足し、不充足の場合は不満に感じる機能
    - それを満たすことができればuserの評価が上がり、満たされなければ評価が落ちる
- 魅力的品質: 充足されていると満足し、不充足の場合は「仕方がない」と感じる機能

## Ch. 2 SW開発の流れとtest工程

### SW開発の流れ

Water fall型開発model: 次の工程を順に行う; 要求定義、基本設計、詳細設計、coding、test
V字model: 要求定義、基本設計、詳細設計とtestの構成要素が対応づいたmodel

|開発工程|test工程|
|-|-|
|要求定義|system test|
|基本設計|機能test, 結合test|
|詳細設計|単体test|

#### 要求定義: 顧客のneedsや要望を整理し、要求を定義すること

#### 基本設計: 要求項目を実現するために必要なSWの機能や構成を定義すること

この段階でsystem全体の基本設計書と機能仕様書が作られる。
機能仕様書：systemで実現できること、できないことが明記されている文書

要件定義といわれることもある。

#### 詳細設計: 基本設計の成果物を元に、各処理の使用を定義すること

詳細設計の範囲は、機能ごと、あるいはmoduleごとである。
module: SWの最小単位。

詳細設計では、各moduleの内部構造を定義する。
module同士が連携して動作することで、SW systemとしての機能が実現される。
内部構造: SW内部の処理の流れ。
連携方法(module間のdataの受け渡し方法)についても、詳細設計で決定する。

#### coding: 詳細設計で定義したことを元に、source codeをかくこと

### test工程の流れ

#### 単体test: moduleごとにtestすること

- 詳細設計書どおりにmoduleが動くかどうかをtestする
- codingされたSWの論理構造が適切かどうかを確認する

#### 結合test: 複数moduleを組合せて動作をtestすること

詳細設計書で定義したmodule間の連携方法が実現されているかを確認する。

#### 機能test: 組合せたmoduleを1機能としてtestすること

内部構造を確かめるのではなく、機能として正しく役割を果たしているかを確認する。

#### system test: 要求定義の内容が実現されているかを確認するtest


|工程|役割|
|-|-|
|開発|目的のSWを徐々に具体化する|
|coding|設計書をもとに、codeを書く。<br /> いくつかの欠陥が含まれている|
|test|欠陥を検出・除去することで品質を高める。|

#### W字model: 開発工程とtest工程を並行して進めるmodel

codingする前に、設計の間違いを直せる。

### さまざまなtestと分類

test工程の各工程で、確認すべき品質を明らかにし、それを充足できるtestを行う必要がある。
- 単体test
- 結合test
- 機能test
- system test

testの分類
||静的test|||動的test||||
|-|-|-|-|-|-|-|-|
|black-box test|<ul> <li>inspection</li><li>technical review</ul>|<ul> <li> technical review</li><li> 非公式review</li></ul>||機能確認test|<ul> <li> 状態遷移test</li><li>機能確認test</li></ul>|<ul> <li> 確認test</li><li> 評価test</li> <li>負荷test</li> <li> 環境test</li> <li> 機能確認test</li> <li> その他のtest</li></ul>|<ul> <li> 受入test</li><li> 運用test</li> <li> alpha test</li> <li> beta test</li></ul>|
|white-box test||walkthrough|<ul> <li>walkthrough</li> <li>非公式review</li> <li>机上debug</li></ul>|<ul> <li>制御flow test</li><li> data flow test</li></ul>|||
||要件定義|設計|実装|単体test|結合test<br />機能test|system test|userによるtest|
||開発工程|||test工程||||

test分類の３軸
- SWの内部構造に注目する/しない:
    - black-box test: SW内部の論理構造に注目して、次のものが正しく行われるかを確認するtestの総称
        - 処理や分岐命令の動作
        - data処理
    - white-box test: 入力と出力のみに注目して、SWが正しく動作するかを確認するtestの総称
- SWを動作させる/させない:
    - 静的test: SWを動作させることなく行うtestの総称
        - 開発仕様書やbuild前のsource codeの状態でtestを行う
        - 開発工程で行われる
    - 動的test: 作成したSWを実際に動作させて確認するtestの総称
        - test工程で行われる
- SW開発の工程
    - 開発工程: 開発工程では主にreviewが行われる。
        - review: 開発仕様書やsource codeの内容を確認した上で、問題点を指摘し、作成者にfeedbackする活動
    - test工程: さまざまなtestが行われる。そのtestは、SW testと呼ばれる。


### testの概要

- 開発工程
    - inspection: 公式性の高いreview。
        process, rule, 役割分担が明確であり、公式記録に残すべき重要度の高い文書に適したreview.
    - technical review: 専門知識を持つreviewerにより、技術的な問題を確認するreview。
        あらかじめ決められたreview processに沿って進められる.
    - 非公式review: 非公式に行われるreview。
        特に決まった方法はない。reveiwerが一人の時はpair reviewと言われる。
    - walkthrough: 作成者がreview対象を説明し、reviewerにcommentを求める形式で進行するreview.
    - 机上debug: SWのsource codeを目視確認し、検出したり誤りを修正する作業。
        source codeの作成者自身が一人で確認・修正することが多い
- test工程
    - 単体test
        - 機能確認test: 各moduleが詳細設計書や機能仕様書通りに動作することを確認する
        - 制御flow test: programの論理構造に沿って、命令や分岐がすべて実行されるかを確認する
        - data flow test: dataや変数が、定義 -> 使用 -> 消滅の順に行われているかを確認する
    - 統合test・機能test
        - 状態遷移test: 状態遷移図・状態遷移表に基づいて動作を確認する
        - 機能確認test: module同士の連携や複数moduleで実現される機能が、詳細設計書どおり動作することを確認する
    - system test
        - 確認test: 
        - 評価test
        - 負荷test
        - 環境test
        - 機能確認test
        - その他のtest
- userによるtest
    - 受入test
    - 運用test
    - alpha test
    - beta test


### black box testの種類とtest技法

## Ch. 3 white box test

### moduleと論理構造

### 制御flow testの実施方法

### data flow testの実施方法

## Ch. 4 black box test

### black box testの流れ

### test観点の必要性と抽出方法

# Part 2 さまざまなtest技法

##  Ch. 5 同値class test and 境界値test

### すべての値をtestすることはできない

### 同値class testとは

### 同値class testの実施方法

### 内部構造と同値classの関係

### 境界値testとは

### 境界値testの実施方法

### 境界値testの効果

### 隠れた境界値

## Ch. 6 decision table test

### decision table testの概要

### decision tableの作り方

### decision tableを見やすくする

### 3値以上の答えを持つ条件の採用

### decision table test の実施方法

### decision tableの活用方法

## Ch. 7 状態遷移test

### 状態遷移testの概要

### 状態遷移図の作り方

### 状態遷移図を用いたtest

### 状態遷移表の作り方

### 状態遷移表を用いたtest

### 状態遷移図と状態遷移表の特徴(まとめ)

## Ch. 8 組合せtest

### 組合せtestの必要性

### 2因子間網羅

### All-Pairs法と直交表の違い

### 組合せtestを実施するまでの流れ

### 組合せ表を作成する際の注意点

## Ch. 9 test技法適用chart

### test技法適用chartの概要

### test技法適用chartの使用方法

### 適用事例

# Part 3 test document and monitoring

## Ch. 10 test documentの作成

### test documentの必要性

### test documentの種類

### IEEEのtest document項目

### test実施における役割分担

## Ch. 11 test documentの正しい書き方

### test設計仕様書: 追跡性・関連性

### test設計仕様書: 定義の理由

### test設計仕様書: 記述の粒度

### test設計仕様書: 規模

### test case: 追跡性・関連性

### test case: test実施のしやすさ

### test case: 記述の粒度

### test case: format

## Ch. 12 test実施のmonitoring

### 不具合の解決と欠陥の修正手順

### 時間経過に伴う状況変化の把握

### 不具合の分類による傾向の把握

### 信頼度成長曲線を用いたmonitoring

### testの状況を把握するための指標一覧表
